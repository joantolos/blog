+++
author = "Joan Tolos"
categories = ["TDD","BDD","Architecture", "Test", "Design"]
date = "2017-11-02"
description = "Using TDD on a critical point of the project"
featured = "pic01.jpg"
featuredalt = ""
featuredpath = "/img/tddAllIn/"
linktitle = ""
title = "TDD: All in"
type = "draft"

+++

## The setup

We faced a complicated release to production on our team. We had to include a brand new feature that will stress the application on different levels: user interface, backend and data. We had also a small window to release it so the pressure was high. Let's establish a little bit the requirements, on a high level (without revealing details of the business).

  {{< img-post path="/img/tddAllIn/" file="overview.png" alt="Tree layout" type="center" >}}

We had to implement the new feature in the green boxes. All that components exists already so we have to add the feature without impacting the existing code. So, we needed:

* Add a whole new navigation path on the User Interface (in that case, a web browser application), including the possibility for a user to upload a file.
* Add the new endpoint to the application API (the Node JS microservice) which will parse the data from the other services and arrange it in a way that is super easy to consume for the UI. In other words, it creates a tailored JSON response to fit the specific needs of the UI. That way there is no logic on the browser.
* Add the logic of the feature on a Java Microservice. This was the tricky part because we had two dependecies:
  * We need to retrieve data from a third party (inside the company) Java Microservice which we don't control
  * The input for this third party microservice is calculated from the user input on the user interface (the user uploads a file).

The content of that file is then processed by a series of complex algorithm (related with chemical and biological stuff) and the result of all that process is transform into the third party service input contract. This input transformation was implemented on a POC just to proof the viability of the feature. The results were good so now we have to transform this POC code into well crafted production code. The POC code was created by mathematicians and scientist so although it does the job, we can not simply use that code. We have to understand it and re-write it on a fashion that suites the application. This code is represented as "spaghetti code" on the diagram.
No offence intended for the scientist colleges that wrote that code. The algorithmic work that includes is beautiful, it's just not created to fit into entire microservice architecture.

So the risks are very clear:

* Thigh schedule
* Dependency from another team
* Unraveling the spaghetti code

I always consider black boxes as a big risk and the dependency with the other team and the spaghetti code are black boxes. So, all the alerts went on, this was a risky feature.

## The implementation

I had to write the code on the Java Micro-Service and the Node JS Micro-Service. Another fellow developer will write the code on the User Interface at the same time.

At that point I took a big decision: I choose to go full TDD from the beginning, let me explain... It is tempting in situations like that with big risks and thigh schedule to try to make the minimum impact on the code base. Try to "smuggle" the feature in without making any noise or big refactors. And TDD explicitly states a refactor on every iteration. I have been coding with TDD for a long time now, so I choose to really test the technique and prove to myself that TDD fits stressful situations as well. I went all in with TDD.

All right, let's code the first test.

My fellow from the UI needs to start working right away if we want to meet the date, so we decided a JSON contract for the UI to consume that seemed appropriate at the time, keeping in mind that when the black boxes starts to open, the contract may change.

So my first test was that given a certain input example, the API will response with the decided JSON. I just made an endpoint that will response the same mock JSON result every time. The UI developer has data to work with from day one, even before than he has the minimum framework to start showing the data. Now the only thing that I have to do is substitute all the pieces of that mocked JSON with the real results bit by bit and the User Interface will start to see real dynamic data little by little. All right, we have an strategy, let's open the boxes.

The difficult thing about the third party Java Micro-Service is that the input for the call is constructed from the user input file with the algorithms applied from the spaghetti code. So building this input is the tricky part.

## The conclusion
