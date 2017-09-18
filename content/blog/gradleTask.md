+++
author = "Joan Tolos"
categories = ["Gradle", "Refactoring", "Git"]
date = "2017-09-16"
description = "Dealing with order on Gradle tasks"
featured = "pic01.jpg"
featuredalt = ""
featuredpath = "/img/gradleTask/"
linktitle = ""
title = "One task after the other"
type = "draft"
+++

Trying to learn a little bit more about how Gradle deals with tasks and how to execute them in an specific order.

# The problem



# The Gradle solution

At that point in time I just hated Gradle and start thinking on alternative solutions. But then I went deep on the Gradle forums, which by the way are super useful, I deeply recommend them, and decided to give it another chance.



## Declaring explicit task dependencies

## Declaring task inputs and outputs

## Final notes about incremental builds

When developing your own build scripts, plugins and custom tasks, declaring task inputs and outputs is an important technique to keep in your toolbox. All of the core Gradle tasks use this to great effect. If you would like to learn about other ways to make your tasks incremental at a lower level, take a look at the incubating incremental task support. Incremental tasks provide a fine-grained way of building only what has changed when a task needs to execute.

# Conclusion

# The Batch Processor solution



# The Next Step solution

Files suck. I mean having to write and read files from disk, you face a lot of inconvenient stuff like concurrency, input/output exceptions, folders location, etc... Besides, writing files to disk is expensive and slow.

### Fonts:

* _{{< url-link "Blog Tricky Android" "http://trickyandroid.com/gradle-tip-3-tasks-ordering/" >}}_

* _{{< url-link "Blog Gradle: Introducing Incremental Build Support" "https://blog.gradle.org/introducing-incremental-build-support" >}}_

* _{{< url-link "Blog Gradle: Writing Custom Task Classes" "https://docs.gradle.org/current/userguide/custom_tasks.html" >}}_

* _{{< url-link "Blog Gradle: Copying files" "https://docs.gradle.org/current/userguide/working_with_files.html" >}}_
