+++
author = "Joan Tolos"
categories = ["code"]
date = "2019-09-06"
description = "Java, Spring Boot, Mock Server"
featured = "pic01.png"
featuredalt = ""
featuredpath = "/img/kataSongsAPI/"
linktitle = ""
title = "6 tools to help you do TDD with Java and Spring Cloud"
type = "post"
+++

I am always trying to manifest the benefits of TDD (see: {{< url-link "The real reason why you don't like TDD" "http://www.joantolos.com/blog/tddcasestudy/" >}} and {{< url-link "TDD: All in" "http://www.joantolos.com/blog/tddallin/" >}}). Most of the times when I find colleges that “can’t” do it right away it is because their software is not “TDD ready” meaning that it is difficult to test.
Solving that pitfall alone is going to improve your software because good code is easy to test, generally speaking.
That is why I create these “seeds” from time to time so people can clone a layout or template which is already “TDD ready”.
Of course this is going to depend on the system requirements but I try to make examples with the most common needs.

I already did an approximation for Javascript {{< url-link "(6 tools to help you do TDD with NodeJS)" "http://www.joantolos.com/blog/javascripttrifecta/" >}} and now I am going to try for Java with Spring Cloud.

Technical requirements:

*  The micro service will register on eureka to consume data from other micro service
*  Also, it will have to consume data from an external api, not registered to eureka, like a third party service
*  It has to connect to a relational database to retrieve and store data.

These three technical requirements will force us to put some solutions in place in order to make tests comfortably:

*  It has to be able to mock responses from a service registered in Eureka
*  It has to be able to mock responses for the external API
*  We will have to deal with the connection to database on test execution

These kind of dependencies are just and example of what makes difficult to start with TDD. I always spend some time trying to set up a test friendly environment, making sure that I can add and modify tests easily.

I will also introduce a layout proposal that will allow us to test on several levels: acceptance, integration and performance.

# A little of business requirements

We have to build a REST API to deal with songs and song information. The Typical CRUD end points will be the following:

* POST add a song
* PUT Edit an existing song
* GET get info from a song
* GET get all songs info

These endpoints are going to make us implement INSERT, UPDATE and SELECT into our database access.

Then, some other end points to deal with the other services connection:

* GET to get all the songs from a peer API connected to Eureka
* GET to get the lyrics from an existing song. The lyrics are provided from an external API

# Overview

{{< img-post path="/img/kataSongsAPI/" file="kataSongsAPIOverview.png" alt="Overview" type="center" >}}

We are going to deploy two instances of the same API, one dedicated to expose "generic" songs info and another just for country songs. This is just to illustrate consuming data from different micro services on your app but normally these service won't be just different instances of the same code. But, technically, it requires the same implementation so I am not creating a new different service just for that.

As proper micro services, each one of them has it's own data domain, so a dedicated database containing the songs.

On the other hand, we have a third party provider that exposes songs lyrics from an artist and song name.

# Localhost pre requirements

Database and Eureka ready on local environment.

## Database

You need to run an instance of PostgresSQL on localhost:5432

You can download Postgres from: https://www.postgresql.org/

Once you run the Postgres server on your local machine, the values for default are:

* Host: localhost
* Database: postgres
* User: postgres
* Password: 123

Now you can connect with your Database IDE of choice (for this simple stuff I recommend {{< url-link "DBeaver" "https://dbeaver.io" >}}) and execute the following SQL script:

    DROP TABLE IF EXISTS songs;

    CREATE TABLE songs (
    	name	VARCHAR(30) NOT NULL,
    	artist	VARCHAR(30) NOT NULL,
    	album	VARCHAR(30) NOT NULL,
    	release_year	VARCHAR(30) NOT NULL
    );

    ALTER TABLE songs ADD CONSTRAINT p_songs PRIMARY KEY (name);

    INSERT INTO songs (name, artist, album, release_year) VALUES('Yellow', 'Coldplay', 'Parachutes', '2000');
    INSERT INTO songs (name, artist, album, release_year) VALUES('Master of puppets', 'Metallica', 'Master of puppets', '1986');
    INSERT INTO songs (name, artist, album, release_year) VALUES('Cocaine', 'Eric Clapton', 'Slowhand', '1977');

This will create the bare minimum for the app to work: just a songs table and three songs added.

## Eureka

Run an instance of eureka on localhost:8761

You can clone this code and run it: {{< url-link "kata-eureka-spring repository" "https://github.com/joantolos/kata-eureka-spring" >}}

    ./gradlew clean build

And then:

    ./gradlew bootRun

## Bypassing localhost requirements

You can skip setting up the database if you copy the configuration from the test environment to the production code environment. Test are using H2 as in-memory database (explained later on), so no external connection is required. If you configure your production code to use it, and uncomment the database creation script "createDatabase.sql" located on the resources file, you can get away without a Postgres instance on your localhost. Is not as accurate scenario as it would be with a real application, but I suppose it can do the trick.

You can ignore setting up your local eureka instance or

## Starting the service on localhost

Clone the repo {{< url-link "kata-songs-api repository" "https://github.com/joantolos/kata-songs-api" >}} and execute:

    ./gradlew clean build

This will build the code and also generate the coverage report. You will find the report on _kata-songs-api/build/reports/jacoco/rootReport/html/index.html_

You can run the SongsAPI class on your IDE or by console:

    java -jar kata-songs-api-src/build/libs/kata-songs-api-1.0.0.jar

This is a Spring Cloud application so you can also run the Gradle task that comes from the plugin:

    ./gradlew bootRun

Then you can access the Swagger UI and test the endpoints:

http://localhost:8080/swagger-ui.html#/

{{< img-post path="/img/kataSongsAPI/" file="swagger.png" alt="Swagger" type="center" >}}

**Remember:** You need to start Postgres and Eureka previously.

# Deploying on Heroku

> _Heroku is a platform as a service based on a managed container system, with integrated data services and a powerful ecosystem, for deploying and running modern apps. The Heroku developer experience is an app-centric approach for software delivery, integrated with today’s most popular developer tools and workflows._

Procfile and environment variables

# Tests

## Plain and simple JUnit unit test

> _JUnit is a simple framework to write repeatable tests. It is an instance of the xUnit architecture for unit testing frameworks._

## Spock unit test

> _Spock is a testing and specification framework for Java and Groovy applications. What makes it stand out from the crowd is its beautiful and highly expressive specification language. Thanks to its JUnit runner, Spock is compatible with most IDEs, build tools, and continuous integration servers. Spock is inspired from JUnit, jMock, RSpec, Groovy, Scala, Vulcans, and other fascinating life forms._

## Acceptance tests

### Cucumber

> _Validate executable specifications against your code on any modern development stack. With over 40 million downloads, Cucumber Open is the world’s #1 automation tool for Behavior-Driven Development._

### H2 in-memory database

> _The main features of H2 are: Very fast, open source, JDBC API. Embedded and server modes; in-memory databases. Browser based Console application. Small footprint: around 2 MB jar file size._

### Mock Server

> _MockServer can be used for mocking any system you integrate with via HTTP or HTTPS (i.e. services, web sites, etc).
When MockServer receives a requests it matches the request against active expectations that have been configured.
An expectation defines the action that is taken, for example, a response could be returned._

{{< url-link "Mock Server" "http://www.mock-server.com" >}} is a very powerful and easy to use tool to mock any external http calls your code does.

mockServerMatcher.log -> Example of non matching request

## Integration tests

## Performance tests

### Gatling

> _Gatling is a powerful open-source load testing solution. Gatling is designed for continuous load testing and integrates with your development pipeline. Gatling includes a web recorder and colorful reports._

### References:

* _Photo by {{< url-link "Matt Artz" "https://unsplash.com/photos/pH6wLT6TVFc" >}} on {{< url-link "Unsplash" "https://unsplash.com" >}}_
* _{{< url-link "The real reason why you don't like TDD" "http://www.joantolos.com/blog/tddcasestudy/" >}}_
* _{{< url-link "TDD: All in" "http://www.joantolos.com/blog/tddallin/" >}}_
* _{{< url-link "6 tools to help you do TDD with NodeJS" "http://www.joantolos.com/blog/javascripttrifecta/" >}}_
* _{{< url-link "Mock Server" "http://www.mock-server.com" >}}_
* _{{< url-link "Spock framework" "http://spockframework.org/" >}}_
* _{{< url-link "Cucumber framework" "https://cucumber.io/" >}}_
* _{{< url-link "JUnit framework" "https://junit.org/junit4/" >}}_
* _{{< url-link "Gatling" "https://gatling.io/open-source/" >}}_
* _{{< url-link "Heroku" "https://www.heroku.com/platform" >}}_
