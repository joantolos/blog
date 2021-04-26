+++
author = "Joan Tolos"
categories = ["code"]
date = "2018-05-03"
description = "Mocha, Chai, Istanbul, Nock, Mock-Require and Lint explained"
featured = "pic01.png"
featuredalt = ""
featuredpath = "/img/javascriptTrifecta/"
linktitle = ""
title = "6 tools to help you do TDD with NodeJS"
type = "post"
+++

I am using NodeJS more and more to implement middleware services instead of Java. That means that I am dealing with Javascript on a daily basis. In order to add features with guaranties, I code with TDD ({{< url-link "and only TDD" "http://www.joantolos.com/blog/tddallin/" >}}) and that means that I need a few tools to code comfortably:

* Some BDD or asserting framework
* Some Code Coverage framework ({{< url-link "I use code coverage to inspire refactors" "http://www.joantolos.com/blog/katamarsrover/" >}})
* Some mocking device

## Mocha

> _Mocha is a feature-rich JavaScript test framework running on Node.js and in the browser, making asynchronous testing simple and fun. Mocha tests run serially, allowing for flexible and accurate reporting, while mapping uncaught exceptions to the correct test cases._

Mocha allows you to write spec.js file for your tests. An example:

On your editor:

    var assert = require('assert');
    describe('Array', function() {
      describe('#indexOf()', function() {
        it('should return -1 when the value is not present', function() {
          assert.equal([1,2,3].indexOf(4), -1);
        });
      });
    });

On the terminal:

    $ ./node_modules/mocha/bin/mocha

    Array
      #indexOf()
        ✓ should return -1 when the value is not present


    1 passing (9ms)

Working with NodeJS, you can add the script on your package.json file:

    "scripts": {
      "test": "mocha"
    }

So you can run your tests normally:

    $ npm test

## Chai

> _Chai is a BDD / TDD assertion library for node and the browser that can be delightfully paired with any javascript testing framework._

Chai allows you to humanise the test and make them more readable which I think is a key feature if you want to write good tests. I always thought that tests are the best documentation and we should use any opportunity to communicate intent when writing code. Meaningful names will make your code easy to read and this library allows you to create actual sentences with both the capability of do the work and explain the message.

Look at some examples:

### Should

    chai.should();

    foo.should.be.a('string');
    foo.should.equal('bar');
    foo.should.have.lengthOf(3);
    tea.should.have.property('flavors').with.lengthOf(3);

### Expect

    var expect = chai.expect;

    expect(foo).to.be.a('string');
    expect(foo).to.equal('bar');
    expect(foo).to.have.lengthOf(3);
    expect(tea).to.have.property('flavours').with.lengthOf(3);

### Assert

    var assert = chai.assert;

    assert.typeOf(foo, 'string');
    assert.equal(foo, 'bar');
    assert.lengthOf(foo, 3)
    assert.property(tea, 'flavours');
    assert.lengthOf(tea.flavours, 3);

Look at this beautiful piece of code:

**tea.should.have.property('flavours').with.lengthOf(3);**

That is self-explanatory and express exactly what the code should do. That is what we should aim: write code and tests that explains the story of the application that you are making, so any coder can quickly get it.

Combining Chai with Mocha we can reach tests suites like this:

    describe('Beverages behaviour', function() {
      describe('Tea', function() {
        it('should have three flavours', function() {
          tea.should.have.property('flavours').with.lengthOf(3);
        });
        it('should be hot', function() {
          expect(tea.isHot).to.be.true;
        });
      });
      describe('Lemonade', function() {
        it('should be cold', function() {
          expect(lemonade.isHot).to.be.false;
        });
      });
    });

And you will see on console:

    Beverages behaviour
      #Tea
        ✓ should have three flavours
        ✓ should be hot
      #Lemonade
        ✓ should be cold

How beautiful is that.

## Istanbul

> Istanbul instruments your ES5 and ES2015+ JavaScript code with line counters, so that you can track how well your unit-tests exercise your codebase.

This tool provides an easy way to take a look at the code coverage, and most important, at the HTML report that generates. We are already using mocha, so we only have to add _nyc_ when using it:

    nyc mocha

We can see the results right away when we build the code:

{{< img-post path="/img/javascriptTrifecta/" file="istanbul.png" alt="Istanbul on console" type="center" >}}    

Additionally, we can generate a HTML report from the coverage results going to the created folder _./nyc_output_ and typing:

    nyc report --reporter=html

or you can add the generation on your build script so every time you run your tests, the report is created. You only have to add some nyc configuration on your package.json file. Like this:

    "nyc": {
      "check-coverage": true,
      "per-file": true,
      "lines": 80,
      "statements": 80,
      "functions": 80,
      "branches": 80,
      "include": [
        "src/*/*.js"
      ],
      "reporter": [
        "text",
        "cobertura",
        "html"
      ],
      "report-dir": "./.nyc_output/coverage-report"
    }

Then you can see your familiar coverage report:

{{< img-post path="/img/javascriptTrifecta/" file="coverageReport.png" alt="Istanbul report" type="center" >}}    

## Nock

> Nock is an HTTP mocking and expectations library for Node.js
Nock can be used to test modules that perform HTTP requests in isolation.
For instance, if a module performs HTTP requests to a CouchDB server or makes HTTP requests to the Amazon API, you can test that module in isolation.

This is a library to mock any combination of http request that you can imagine. The usage is simple, the best way to understand it is with an example.

There is a free API available on GitHub called {{< url-link "the GitBug Jobs API" "https://jobs.github.com/api" >}} which provides information about the job offers available on GitHub. Some example call is the following:

https://jobs.github.com/positions.json?description=java&location=barcelona

Which will retrieve a response like this one:

    [
       {
          id:"3d0c8c86-5a78-11e8-9dac-d37aab551739",
          created_at:"Fri May 18 08:49:59 UTC 2018",
          title:"Front-end Jedi ",
          location:"Barcelona, Spain",
          type:"Full Time",
          description:"Job description trunked for the article purpose",
          how_to_apply:"https://marfeel.bamboohr.com/jobs/view.php?id=1",
          company:"Marfeel",
          company_url:null,
          company_logo:"http://github-jobs.s3.amazonaws.com/2618f276-5a78-11e8-802d-263daf7f08b9.png",
          url:"http://jobs.github.com/positions/3d0c8c86-5a78-11e8-9dac-d37aab551739"
       },
       {
          id:"f9080d9e-26dd-11e8-97ec-50dc22333a0f",
          created_at:"Sun May 13 17:13:09 UTC 2018",
          title:"Java Backend Developer",
          location:"Barcelona",
          type:"Full Time",
          description:"Job description trunked for the article purpose",
          how_to_apply:"https://king.com/es/jobs/java-backend-developer-803?breadcrumbs=/jobs&amp;location=barcelona&amp;src=NGP-12180",
          company:"King",
          company_url:"http://www.king.com",
          company_logo:"http://github-jobs.s3.amazonaws.com/f5d692c6-26dd-11e8-93a2-8d7be3afb0d0.png",
          url:"http://jobs.github.com/positions/f9080d9e-26dd-11e8-97ec-50dc22333a0f"
       }
    ]

This response will change every time there is a new job offer or one offer disappears, so we can't not rely on it for testing purpose. Now, what we can do is mock the service response using Nock.

On your "beforeEach" section of your test suite, you simulate the call:

    beforeEach(function() {
      nock('https://jobs.github.com:443', { 'encodedQueryParams': true })
        .get('/positions.json')
        .query({ 'description': 'java', 'location': 'barcelona' })
        .reply(200, [
          {
            id: '3d0c8c86-5a78-11e8-9dac-d37aab551739',
            created_at: 'Fri May 18 08:49:59 UTC 2018',
            title: 'Front-end Jedi ',
            location: 'Barcelona, Spain',
            type: 'Full Time',
            description: 'Super fake job',
            how_to_apply: 'Just ride a giant rocket',
            company: 'ACME'
          },
          {
            id: 'f9080d9e-26dd-11e8-97ec-50dc22333a0f',
            created_at: 'Sun May 13 17:13:09 UTC 2018',
            title: 'Java Backend Developer',
            location: 'Barcelona',
            type: 'Full Time',
            description: 'Another fake job but matching the API service contract.',
            how_to_apply: 'Follow the yellow brick road',
            company: 'Pied Piper'
          }
        ]);
    });

There you define the host, the http method, headers, content, params etc... You can match any request that you can think of. Then nock will return the content specified on the "reply" section, instead of making the actual real call.

Now you know what the service will return, always and you can perform your tests. Of course, if the API contract changes, you will have to update the mock.

## Mock-Require

> mock-require is useful if you want to mock require statements in Node.js. I wrote it because I wanted something with a straight-forward API that would let me mock anything, from a single exported function to a standard library.

This will substitute a required library with an specific code that you choose. I find this specially util when working with third party libraries inside the company project. Sometimes you are working with a project where different teams implicated and some team has to provide you some functionality. If you want to go ahead and code without waiting their results, you can mock their logic and start with your implementation.

If the project is big and the team is allocated this happens a lot, so a good tool to have in hand. Example:

    var mock = require('mock-require');

    mock('http', { request: function() {
      console.log('http.request called');
    }});

    var http = require('http');
    http.request(); // 'http.request called'

It is really simple to use as you can see.

## Javascript Lint

> With JavaScript Lint, you can check all your JavaScript source code for common mistakes without actually running the script or opening the web page.

This is extra. Lint is not directly attached to TDD but I find it a very useful tool to write good code on Javascript.

Lint will prevent your build to happen if the code does not match the rules defined. For example, if you write this if statement:

    if(true){
      console.log('Hello');
    }

{{< img-post path="/img/javascriptTrifecta/" file="lintFailing.png" alt="Lint Failing" type="center" >}}   

Lint rule "keyword-spacing" is expecting an space after the if statement, and the "space-before-blocks" rules wants a space before the brace. Changing the code like this:

    if (true) {
      console.log('Hello');
    }

Now Lint is happy and the build can happen. Sometimes we refer at Lint as the _Javascript Police_. The rules for Lint to follow are defined on the file _.eslintrc_

Is annoying sometimes but long term it really helps to have a consistent code base. Most of coding IDE include an option to include Lint on their grammatical syntax highlight, that way you can see the mistakes while coding and don't have to wait until the build.

## Take Out

It looks like a lot, and it probably is. That is why I have created a seed project that includes Gradle as a building tool: {{< url-link "Javascript TDD Seed" "https://github.com/joantolos/javascript-tdd-seed" >}}

This seed contains the combination of the six tools already prepared with some explanatory tests. Clone the repo and play with it. It's easier than it looks.

### References:

* _Photo by {{< url-link "Matt Artz" "https://unsplash.com/photos/lt2GzPlOAmc" >}} on {{< url-link "Unsplash" "https://unsplash.com" >}}_
* _{{< url-link "Javascript TDD Seed" "https://github.com/joantolos/javascript-tdd-seed" >}}_
* _{{< url-link "Mocha" "https://mochajs.org" >}}_
* _{{< url-link "Chai" "http://www.chaijs.com/" >}}_
* _{{< url-link "Istanbul" "https://istanbul.js.org/" >}}_
* _{{< url-link "Nock" "https://github.com/node-nock/nock" >}}_
* _{{< url-link "The GitBug Jobs API" "https://jobs.github.com/api" >}}_
* _{{< url-link "Mock-Require" "https://www.npmjs.com/package/mock-require" >}}_
* _{{< url-link "Javascript Lint" "http://www.javascriptlint.com/" >}}_
* _{{< url-link "Measure your code coverage using Istanbul (with a demo)" "https://medium.com/walkme-engineering/measure-your-nodejs-code-coverage-using-istanbul-82b129c81ae9" >}}_
