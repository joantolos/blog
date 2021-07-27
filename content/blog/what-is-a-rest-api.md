+++
author = "Joan Tolos"
categories = ["code"]
date = "2021-10-15"
description = "Definition and examples"
featured = "pic01.png"
featuredalt = ""
featuredpath = "/img/restAPI/"
linktitle = ""
title = "What is a REST API"
type = "post"
+++

The simple (obvious and absurd) answer to the question _"what is a REST API?"_ would be: **It is an API that conforms to the REST architectural style.** The proper follow up questions of course are: what is an API and what is the REST architectural style. If you know the conventions of REST and what are the main characteristics of an API you can deduce your own answer. So, let's dig in:

## What is an API

Sometimes, the acronym itself can clarify the meaning of the term. API stands for Application Programming Interface. Meaning, a set of definitions and protocols for building and integrating application software.

Using this definitions and protocols, two (or more) pieces of software can interact with each other without having to know anything about each-other's implementations.

Another way to visualise the concept is thinking about **contracts.** Sometimes API are referred as contracts... if I send you this request following your definition and/or protocols, you will respond what is expected. As long as all the parties follow the contract, everything runs as it should.

This abstraction allows an easy integration between pieces of software into a new or an existing architecture. If some of the API needs to change, as long as the contract remains the same, the pieces interacting with this API will not notice anything. If there is the need to change the contract, this is called a _breaking change_ so some kind of _version control_ should be in place so the clients of that API can choose the new implementation if they are ready to adapt to the new contract.

Summing up, an API let you open up access to your resources while maintaining security and control.

## What are the REST conventions

REST stands for representational state transfer. When a client request is made via a RESTful API, it transfers a representation of the state of the resource to the requester or endpoint. This representation, is delivered usually on JSON (Javascript Object Notation) format. Others are available but JSON is the most generally popular programming language to use because, despite its name, it’s language-agnostic, as well as readable by both humans and machines.

The HTTP request is made by a client, to a host (the API) in order to be able to access a resource on the API. An http request is made by the following elements:

- A request line: Includes a method, the path and the http version number. Example: GET /api/v2/users HTTP/1.1
- Http headers or header fields. Example: Accept-Language: fr, de
- A message body, if needed.

So, the REST API will expose a series of resources, each one of them will have this "signature"... will be a combination of request line, headers and body. That will make the contract of the API.

## So, what is then a REST API

All right, after these two definitions, we know that a REST API will transfer a representation of the state of a resource according to the HTTP request made. The collection of possible HTTP requests that the API will accept are often referred as the contract of the API. Let's see a simple example.

This request:

**GET /api/jedis**

Will responde something like:

    [
        {
            "username": "luke",
            "password": "123"
        },
        {
            "username": "vader",
            "password": "456"
        }
    ]

Simple enough right? And pretty self explanatory. The JSON format is very convenient because it's easy to read as we read natural language and it's very easy to manipulate programatically.

The advantages of working with one or several API on your architecture are pretty obvious. You can treat the API as a black box without worrying about how it is implemented or the specifics. A single API can have several consumers, for example, you can build an API to serve a browser bases web application and a mobile application at the same time. The data will be consistent between the two consumers but the representation will be different as it is fitting different devices.

{{< img-post path="/img/restAPI/" file="api.png" alt="Classes Diagram" type="center" >}}

You can also find API sold as standalone. So if you plan to create an application about car routes or traffic, you can probably find some provider that will sold you an API exposing the data that you need. So building APIs can be a business model in itself.

## Other kinds of API

If we now know that REST is a kind of API that follow some specifics, we can easily deduce than must be **other** kinds of API, some other specifics to follow. REST being one of the most popular choices nowadays, the next obvious option is SOAP (and more recently GraphQL but out of the scope of this post).

Going back to the acronyms again, SOAP stands for: Simple Object Access Protocol. The last word already give us a clue of the main difference between SOAP and REST. SOAP is a **protocol**, REST are a group of **conventions.** That is a big difference right there. A protocol is something you must follow, a convention is something you should follow, but not really obliged to.

SOAP, being an official protocol, it comes with strict rules and advanced security features such as built-in ACID compliance and authorisation. Higher complexity, it requires more bandwidth and resources which can lead to slower page load times. The SOAP messages are build on XML and XML alone and consist on:

- Envelop
- Header
- Body
- Fault

You want to use SOAP if you have a need for high security and/or perform complex transactions. It is widely used for financial services, payments, authentication... One of the most well known {{< url-link "SOAP APIs is PayPal’s public API" "https://developer.paypal.com/docs/nvp-soap-api/soap/" >}} that allows you to accept PayPal and credit card payments, add a PayPal button to your website, let users log in with PayPal, and perform other PayPal-related actions. Although it is rendered deprecated, it is one of the most famously used.

## Public REST API to checkout and play

One of the most popular public API's is the {{< url-link "Google Maps API" "https://developers.google.com/maps/documentation" >}} if you want to mess around with maps and locations. There is also this famous repository with a huge collection of public APIs: https://github.com/public-apis/public-apis where you can find data from animals to news... wherever you can imagine.

## A few examples made by myself

If you want to create your own REST API, there are a lot of resource on line to help you do it in any language or flavour you can imagine. Just a few examples of my own with several languages/frameworks etc...

- {{< url-link "Users API made with Kotlin using Postgres" "https://github.com/joantolos/kata-kotling-spring" >}}
- {{< url-link "Users API made with Java using Postgres" "https://github.com/joantolos/kata-spring-db" >}}
- {{< url-link "Songs API made with Java using Postgres, consuming a third party public API" "https://github.com/joantolos/kata-songs-api" >}}
- {{< url-link "API made with Java with token authentication" "https://github.com/joantolos/kata-scores" >}}

Take a look and make your own!

### References:

* _Photo by {{< url-link "Sincerely Media" "https://unsplash.com/@sincerelymedia?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" >}} on {{< url-link "Unsplash" "https://unsplash.com/s/photos/soap-bar?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" >}}_
* _{{< url-link "Red Hat: What is a REST API?" "https://www.redhat.com/en/topics/api/what-is-a-rest-api" >}}_
* _{{< url-link "SOAP vs REST vs JSON, a 2020 comparison" "https://raygun.com/blog/soap-vs-rest-vs-json/" >}}_
* _{{< url-link "SOAP vs REST. What's the Difference?" "https://smartbear.com/blog/soap-vs-rest-whats-the-difference/" >}}_
* _{{< url-link "What is  an API" "https://www.redhat.com/en/topics/api/what-are-application-programming-interfaces" >}}_
* _{{< url-link "SOAP APIs is PayPal’s public API" "https://developer.paypal.com/docs/nvp-soap-api/soap/" >}}_
* _{{< url-link "Google Maps API" "https://developers.google.com/maps/documentation" >}}_
* _{{< url-link "Public APIs" "https://github.com/public-apis/public-apis" >}}_
