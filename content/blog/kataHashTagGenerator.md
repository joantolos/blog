+++
author = "Joan Tolos"
categories = ["kata", "tdd", "java"]
date = "2020-02-22"
description = "Simple tool for community managers"
featured = "pic01.png"
featuredalt = ""
featuredpath = "/img/kataHashTagGenerator/"
linktitle = ""
title = "Kata hashtag generator"
type = "post"
+++

Our community manager needs a software to generate a single text sentence containing all the desired hashtags. The main feature is that it has to be quick and easy to use. Just copy from the software and paste into the social media post.

## Requirements

Given a static finite list of words, we want a single string containing a random sub set of said words, separated by spaces and preceded with the character #.
Also, we want the string to start from another static finite list of words but not randomized this time.

## Acceptance criteria

Given:

    profile.1.default=java,programming
    profile.1.random=tdd,testing,framework,spring,kubernetes,microservice,cloud,aws,test,spock,junit

When I do a GET request like:

    http://{host}/1/3

Where 1 is the profile ID and 3 is the number of random words desired,

Then I retrieve a single text sentence like:

    #programming #java #aws #tdd #spring

The first two words are the ones defined as default and the last three are randomly selected from the other list.

## Try it

You can try the application deployed on Heroku on the following end point:

https//kata-hashtag-generator.herokuapp.com/{profileId}/{ramdonCount}

Where:

- profileId is the id of the profile that defines the default and random words
- randomCount is the number of random words that I want to add

These are the list of words included on the deployed app:

    profile.1.default=java,programming
    profile.1.random=tdd,testing,framework,spring,kubernetes,microservice,cloud,aws,test,spock,junit

This call:

{{< url-link "https://kata-hashtag-generator.herokuapp.com/1/3" "https://kata-hashtag-generator.herokuapp.com/1/3" >}}

Would provide something like this:

    #java #programming #testing #junit #kubernetes

Where "java" and "programming" are the default words and "testing", "junit" and "kubernetes" are three of the random list.
You can find the code here: {{< url-link "GitHub repository" "https://github.com/joantolos/kata-hashtag-generator" >}}

# Disclaimer

All right I did this for my wife. I know almost no one reads these post till the end so I am going to indulge myself a little.

She runs an e-commerce and I saw her struggling every night trying to compose a nice update for her store’s Instagram. Once the hard work was ready, she had to figure out a list of hashtags to go along.

I propose her this simple solution and now she is saving some time. I am happy to make her work easier.

### References:

* _Photo by {{< url-link "Free-Photos" "https://pixabay.com/photos/analytics-hash-tag-hash-social-2998837/" >}} on {{< url-link "Pixabay" "https://pixabay.com" >}}_
