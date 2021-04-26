+++
author = "Joan Tolos"
categories = ["code"]
date = "2015-08-26"
description = "Using Cobertura tool on multi-module maven projects"
featured = "pic01.jpg"
featuredalt = ""
featuredpath = "/img/cobertura/"
linktitle = ""
title = "Cobertura and Maven"
type = "post"

+++

## The problem

Most of developers have used or heard about Cobertura tool to calculate test coverage on Java code. The main problem with that tool is that is difficult to use inside a multi-module maven project, where some module contains tests that uses java classes on several other modules.
The result on that cases is a poor coverage or zero percent, just because is not taking into account all the modules implies.

## The solution

I have written a very simple POC using Cobertura tool into a multi-module project, you can find it on GIT:

{{< url-link "Cobertura plus POC" "https://github.com/joantolos/cobertura-plus" >}}

On the **README.md** file you will find all the steps needed to execute the tests and check the report.

On that example whe have two modules with code (product and enum), a module containing two tests and a module to collect all the Cobertura scripts and results.

{{< img-post path="/img/cobertura/" file="cobertura-module-layout.png" alt="Module layout" type="center" >}}

If you follow the steps detailed on the README.md file on GIT, you will obtain a Cobertura report like this:

{{< img-post path="/img/cobertura/" file="cobertura-report.png" alt="Coverage report" type="center" >}}

With that POC you have all the necessary information to include the Cobertura capabilities in your multi-module project.

Hope this post helps other developers to improve the code checking the final reports.
