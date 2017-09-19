+++
author = "Joan Tolos"
categories = ["Gradle", "Refactoring", "Git"]
date = "2017-09-16"
description = "Dealing with order on Gradle tasks"
featured = "pic01.jpg"
featuredalt = ""
featuredpath = "/img/gradleTask/"
linktitle = ""
title = "One task to rule them all"
type = "draft"
+++

Trying to learn a little bit more about how Gradle deals with tasks and how to execute them in an specific order.

# The problem

I was asked for help on a project dealing with Gradle task and what is seemed like a simple _ordering task_ problem. The set up is the following:

{{< img-post path="/img/gradleTask/" file="gradleTaskLayout.png" alt="Module layout" type="center" >}}

This is a simplification of the project layout, where names have been changed. We have a module that creates files and another module that consumes the files. The restrictions are:

* Both the production and consumption of the files must work as an standalone Java program
* The producer creates a larger number of files but the consumer will one consume the **selected** file that satisfies the following rules:
  * The name of the file starts with a certain string.
  * The latests modified file that matches the first rule.

# The Gradle solution

The idea is to have three gradle tasks:

* **produce:** Will create the list of files invoking the Java program on "producer" module and store them into the output folder.
* **select and move:** Will select the proper file following the rules and move it to the input folder of the consumer.
* **consume:** Will grab the files from it's input folder and process them.

Since the producer and consumer are standalone Java programs, that means that contains a class with a main method to execute so I discovered the **JavaExec** type of Gradle task.

On the producer _build.gradle_ file:

    task produce(type: JavaExec) {
        main = 'com.joantolos.gradle.file.producer.ProducerApp'
        classpath = sourceSets.main.runtimeClasspath
    }

This JavaExec type of task allows us to run a Java program, just specifying the main class and the classpath. You can also define the args array if needed.

The same strategy for the consumer:

    task consume(type: JavaExec) {
        main = 'com.joantolos.gradle.file.consumer.ConsumerApp'
        classpath = sourceSets.main.runtimeClasspath
    }

Now if we execute:

    gradle produce

The list of files is created into the output folder of the producer module. Then, if we manually grab one of them and put it into de input folder of the consumer module, we can execute the consumer:

    gradle consume

So, the only link missing is the selecting and moving part. For that, I found the Copy task from Gradle that have a simple syntax:

    task copy(type: Copy) {
        from 'outputFolder'
        into 'inputFolder'
    }

Now I know hoy to copy files, but first I have to be able to select the latest modified matching a substring on the name, from the produced list. For that, my college made this cool combination of regular expression and Groovy scripting.

Given:

* **outputFolder:** The folder where the files are located. The output folder from the producer module.
* **filePattern:** The substring to find in the file name.

We can apply this to find the candidate file, the last one modified matching the substring on it's name:

    String lastFile = new File(outputFolder).listFiles().findAll { filePattern.matcher(it.name) }?.sort { -it.lastModified() }?.head()?.getName()

Cool, we have a name, now let's copy the fortunate file to the input folder of the consumer. We have the Copy task from Gradle to do that, so something like that should work:

    task pickLast(type: Copy) {
        String lastFile = new File(outputFolder).listFiles().findAll { filePattern.matcher(it.name) }?.sort { -it.lastModified() }?.head()?.getName()

        from outputFolder + lastFile
        into inputFolder
    }

Good. Now if we execute the three tasks one by one, it works, eureka. Now let's create an additional Gradle task, let's call it _process_ that only has to execute the three task in order and we should be good to go. Now is where things get ugly...

In Gradle, there is no such thing as "order" in task and technically there is no point of calling a task inside of another, since this is a **building tool** we are talking about. What we can do is make the tasks depending one on another.

So, Gradle offers different tools to do that:

* dependsOn
* doLast
* taskY.shouldRunAfter taskX
* taskY.shouldRunBefore taskX
* taskY.mustdRunAfter taskX
* taskY.mustRunBefore taskX

After fooling around a little bit with several combinations I figure out some way to execute three tasks in order:

{{< img-post path="/img/gradleTask/" file="dependingTasks.png" alt="Depends on" type="center" >}}

It took me a while to figure out that so I will keep that diagram close to my heart, if I never have to work with that kind of things again.

The solution didn't completely work thought. For some reason, the copy task was always running _**before**_ the produce task. So, either there were no files to select from (that being the first execution), or it always was selecting from the latest execution.

I struggled with different combinations of the Gradle tools with little success and having the feeling that the Copy task is not being executed, but evaluated.

At that point in time I just hated Gradle and start thinking on alternative solutions. But then I went deep on the Gradle forums, which by the way are super useful (I deeply recommend them), and decided to give it another chance. I found some interesting concepts when working with tasks:

## Creating your own task type

This is a possibility that Gradle offers. We can use the power of Groovy and define a _class_ inside the _build.gradle_ file and use that class as a task type. So we can define something like this:

    task generator(type: Generate) {
        fileCount = 20
    }

    class Generate extends DefaultTask {
        @Input
        int fileCount = 10

        @OutputDirectory
        File generatedFileDir = project.file("${project.buildDir}/generated")

        @TaskAction
        void perform() {
            for (int i=0; i<fileCount; i++) {
                new File(generatedFileDir, "${i}.txt").text = i
            }
        }
    }

This is an example extract from the Gradle forum and it looks like it fit the needs perfectly. We even have annotations for input and ouput and then a _TaskAction_ where you can write Groovy code. Nice, let's try to adapt it to our needs. I would like to have something like this:

    task process(type: Generate) {
        outputFolder = '/producer/src/main/resources/output/'
        inputFolder = '/consumer/src/main/resources/input/'
        filePattern = 'File-Type-Something'
    }

    class Generate extends DefaultTask {
        @Input
        String inputFolder

        @Input
        String filePattern

        @OutputDirectory
        File outputFolder = outputFolder

        @TaskAction
        void perform() {
            //Generate, move and consume
        }
    }

That looks perfect, now I only have to make an instance of the producer inside the perform method of the task. What I would like to do is something like this:

    @TaskAction
    void perform() {
        Producer producer = new Producer(outputFolder)
        producer.produce()

        String lastFile = new File(outputFolder).listFiles().findAll { filePattern.matcher(it.name) }?.sort { -it.lastModified() }?.head()?.getName()

        FileUtils.copyFileToDirectory(new File(outputFolder + lastFile), new File(inputFolder))

        Consumer consumer = new Consumer(inputFolder)
        consumer.consume()
    }

This code already smells a little to my nose as it is doing a lot of things in a _Java fashion way_ inside the build file of a project. But not only that, the thing is that it does not even work. In fact, you can not do that.

You can use Java classes inside your build and use Groovy to perform actions with them, but only with classes inside of a jar file defined as a dependency. You can not use a class of your project, because it is not compiled yet. Gradle is a building tool, and you define and use tasks to define the **build** of your project. So, when trying to use the Producer or Consumer class on the script, that classes _are not compiled yet_.

That made me think that we are not using Gradle as it is supposed to be used. The copy task, the depends, the possibility of define classes... all this toolbox is offered to you in order to define the build of your project. You are not supposed to execute a Java program and then expect to collect the results of that program to execute another one. This is more a task for an SSH script, again, **Gradle is a building tool.**



# Conclusion

# The Batch Processor solution



# The Next Step solution

Files suck. I mean having to write and read files from disk, you face a lot of inconvenient stuff like concurrency, input/output exceptions, folders location, etc... Besides, writing files to disk is expensive and slow.

### Fonts:

* _{{< url-link "Blog Tricky Android" "http://trickyandroid.com/gradle-tip-3-tasks-ordering/" >}}_

* _{{< url-link "Blog Gradle: Introducing Incremental Build Support" "https://blog.gradle.org/introducing-incremental-build-support" >}}_

* _{{< url-link "Blog Gradle: Writing Custom Task Classes" "https://docs.gradle.org/current/userguide/custom_tasks.html" >}}_

* _{{< url-link "Blog Gradle: Copying files" "https://docs.gradle.org/current/userguide/working_with_files.html" >}}_
