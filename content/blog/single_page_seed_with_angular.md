+++
author = "Joan Tolos"
categories = ["code"]
date = "2021-03-10"
description = "Angular client tutorial deployed"
featured = "pic01.png"
featuredalt = ""
featuredpath = "/img/angularCli/"
linktitle = ""
title = "Single page seed with Angular"
type = "post"
+++

We are using the Angular client on my job now and I wanted to do a tutorial to learn the basics. I already did the {{< url-link "Tour of heroes tutorial" "http://www.joantolos.com/blog/angulartutorial/" >}} but it was a long time ago and since I don't code much front end usually, I could use a refresh.

I need an excuse, thought. If I am making a single page webapp and deploy it, I want it to be useful somehow, not just an exercise. Cue to the most ridiculous app idea you probably read:

# Lazy oven

{{< img-post path="/img/angularCli/" file="logo.png" alt="Logo" type="center" >}}

Ok, it was last Christmas holidays. It was my wife's turn to put the kids to sleep and we decided to have a late dinner afterwards. Some frozen salmon cake made on the oven. While she is telling bedtime stories and singing lullabies, I am making dinner so when the kids are sleep, we can have a bite and maybe watch a TV show if we don't fall sleep.

Anyway, when cooking on the oven we have to take into account the time to heat the oven, the time cooking and some minutes after to let the dish cool off a little before start eating. My question is... if we want to start eating at 22:30 and the dish takes 25 minutes to cook, when do I have to start the oven, put in the dish and put it out? A simple subtraction, I know, but it bothers me. Suddenly, it hit me: I want a simple single web app where I can put the time when I want to start eating and the time that takes to cook the dish and then it tells me when to start the oven, put in the dish and put it out.

I am going to write an example because the pure complexity of the problem may be too much...

> I want to eat at 22:00 and the (let's say) pizza, takes 15 minutes to cook, I have to start the oven at 21:30, put the pizza at 21:40 and put it out at 21:55, wait for five minutes and eat at 22:00.

It is ridiculous, I know, but trust me that I will be using it more than twice.

# Hands on

First step on the Angular CLI tutorial, is to actually install the CLI on your machine:

    npm install -g @angular/cli

Now is the time to create, build, and serve a new, basic Angular project on a development server, go to the parent directory of your new workspace use the following commands:

    ng new kata-lazy-oven
    cd kata-lazy-oven
    ng serve

You can now go to localhost:4200 and see the welcome page from Angular:

{{< img-post path="/img/angularCli/" file="welcome.png" alt="Welcome from Angular" type="center" >}}   

Now, this page is not much, but it is something deployable. Before going into modifying this page or adding our Angular components and whatnot, let's just figure out a way to deploy this default app into Heroku.

# Deploying on Heroku

{{< url-link "Heroku" "www.heroku.com" >}} is awesome. I use it for all of my little pet projects and every time that I try some need language or... well, everything that I do, I try to deploy it to production on {{< url-link "Heroku" "www.heroku.com" >}}. That way I deal with the problems and difficulties of pushing the code to production environment and that makes the whole learning experience way more real. Everything works on localhost, always. When you have to deal with a real database and a real environment, you will face problems that will provide you very useful skills.

1. Create an account on Heroku if you don't already have one.
1. Create the app "kata-lazy-oven" (or any other name that you like but it will have to be consistent with the one on the code)
1. Connect your app to your github repo where you have the code. You can configure it to build and deploy on every push. There are a lot of continuous delivery and integration that Heroku offers out of the box

{{< url-link "Heroku" "www.heroku.com" >}} offers a lot of cool features like logging, a bunch of add-ons and a lot of them go for free. Don't miss it.

## Modifying the Angular default app to be deployed on Heroku

We have to do several minor modifications on the code generated by de Angular client.

### Using express

We are going to need something to serve our files. Let’s go with {{< url-link "Express" "https://expressjs.com/" >}}. We will also need “path” to setup our server.

> Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications.

    npm install --save express path

Create a server file. In your main application directory create a file called server.js and add the following code:

    const express = require('express');
    const path = require('path');
    const app = express();

    // Serve static files....
    app.use(express.static(__dirname + '/dist/kata-lazy-oven'));

    // Send all requests to index.html
    app.get('/*', function(req, res) {
      res.sendFile(path.join(__dirname + '/dist/kata-lazy-oven/index.html'));
    });

    // default Heroku PORT
    app.listen(process.env.PORT || 8080);

### Proper scripts configuration

When we push code to Heroku, the scripts listed in the package.json file will be consulted, and if we have any preinstall or postinstall scripts, they will be run at the appropriate times. What we want to do in this scenario is have the build command run after the dependencies have been installed.

So, open the package.json file, add this postinstall script and change the start script from "ng serve" to "node server.js":

    "scripts": {
       ...
       "start": "node server.js",
       "postinstall": "ng build --aot --prod"
     }

Now we are not using the Angular client anymore to start our app but Node with Express, so, on your local terminal you can go:

    npm start

And the app will start on localhost:8080 which is the port we put on the server.js file.

### Push to GIT, check the app

If you have configured your app on Heroku to deploy when a changed is pushed to the repository, the build will be already in progress. If not, just deploy the app, wait until the build is finished and check the url:

https://kata-lazy-oven.herokuapp.com/

At this point in time, you should see the exact same Angular welcome page that you see on localhost. It doesn't do much, but it is something online. Of course, I have named the app "kata-lazy-oven", but you can named it as you wish.

# Angular router tutorial

I am going to quickly sum up the routes tutorial with the simple modifications that I made for this app. I recommend you follow {{< url-link "the actual tutorial here." "https://angular.io/guide/router-tutorial" >}}

First, create the two components we are going to use, settings and recipe:

    ng generate component settings
    ng generate component recipe
    ng generate component page-not-found

On the settings we are going to set up the input data and on the recipe we will show the final result. That way we can play a bit with passing data from component to component. We will also use a component for when a non-existing page is requested.

In your code editor, locate the file, settings.component.html and replace the placeholder content with the following HTML.

    <h3>Settings</h3>
    <p>Settings here</p>

In your code editor, locate the file, steps.component.html and replace the placeholder content with the following HTML.

    <h3>Recipe</h3>
    <p>Recipe here</p>

In your code editor, locate the file, page-not-found.component.html and replace the placeholder content with the following HTML.

    <h2>Page Not Found</h2>
    <p>We couldn't find that page! Not even with x-ray vision.</p>

Then, we should add some styles... these are the styles suggested on the tutorial:

    .button {
      box-shadow: inset 0px 1px 0px 0px #ffffff;
      background: linear-gradient(to bottom, #ffffff 5%, #f6f6f6 100%);
      background-color: #ffffff;
      border-radius: 6px;
      border: 1px solid #dcdcdc;
      display: inline-block;
      cursor: pointer;
      color: #666666;
      font-family: Arial;
      font-size: 15px;
      font-weight: bold;
      padding: 6px 24px;
      text-decoration: none;
      text-shadow: 0px 1px 0px #ffffff;
      outline: 0;
    }
    .activebutton {
      box-shadow: inset 0px 1px 0px 0px #dcecfb;
      background: linear-gradient(to bottom, #bddbfa 5%, #80b5ea 100%);
      background-color: #bddbfa;
      border-radius: 6px;
      border: 1px solid #84bbf3;
      display: inline-block;
      cursor: pointer;
      color: #ffffff;
      font-family: Arial;
      font-size: 15px;
      font-weight: bold;
      padding: 6px 24px;
      text-decoration: none;
      text-shadow: 0px 1px 0px #528ecc;
      outline: 0;
    }

Put them on "app.component.css"

Then, on app.component.html, you can add the basic two buttons to navigate between routes:

    <h1>Lazy Oven</h1>

    <router-outlet></router-outlet>

    <nav>
      <a class="button" routerLink="/settings" routerLinkActive="activebutton">Settings</a> |
      <a class="button" routerLink="/recipe" routerLinkActive="activebutton">Recipe</a>
    </nav>

Last, add the proper declarations and imports the app.module.ts file:

    declarations: [
      AppComponent,
      PageNotFoundComponent,
      SettingsComponent,
      StepsComponent
    ],
    imports: [
      BrowserModule,
      RouterModule.forRoot([
        {path: 'settings', component: SettingsComponent},
        {path: 'recipe', component: RecipeComponent},
        {path: '', redirectTo: '/settings', pathMatch: 'full'},
        {path: '**', component: PageNotFoundComponent}
      ]),
    ],    

Again, check out the actual tutorial for more details.

After those modifications you should see the following when starting the app on localhost with "ng serve":

{{< img-post path="/img/angularCli/" file="tutorial.gif" alt="Tutorial" type="center" >}}

# Lazy oven business logic

The application logic is encapsulated into two pages:
- The settings page where you can put your eating time and the cooking time of the meals
- The recipe page where you can see the results and see when do you have to do the different steps

So, the app will have page three components, one for hosting the whole app, one for the settings and another one for the results. The only tricky part is to pass the data from the settings page to the result page, so it can calculate and render the result. I am doing this with a generic service that will store the data input from the settings page, modify it and calculate the final times.

This service, which I called simply "lazy-oven.service", allows to store the data from one component to be used on the other and also mades the calculations needed. That is the only tricky part of the application.

# Take over

Here is the code: https://github.com/joantolos/kata-lazy-oven and here is the application deployed: https://kata-lazy-oven.herokuapp.com/

Now I only have to apply some cool styles and design so the pages look nice. I will probably spend the rest of my life doing that because I really suck with HTML and CSS. This was the point of these exercise: learn about Angular, HTML, CSS and fight with the browser.

If you visit the deployed application on Heroku, you will probably see something broken because I will be playing with styles and pages so it looks nice.

### References:

* _{{< url-link "Using Angular routes in a single-page application" "https://angular.io/guide/router-tutorial" >}}_
* _{{< url-link "Deploy Angular 7 App to Heroku" "https://codemeals.com/angular-tutorials/deploy-angular-7-app-to-heroku/" >}}_
* _{{< url-link "Express" "https://expressjs.com/" >}}_
* _{{< url-link "Sharing Data Between Angular Components" "https://medium.com/front-end-weekly/sharing-data-between-angular-components-f76fa680bf76" >}}_
