+++
author = "Joan Tolos"
categories = ["code"]
date = "2019-01-18"
description = "Different Gradle modules, on of them creating a grammar"
featured = "pic01.png"
featuredalt = ""
featuredpath = "/img/antlr/"
linktitle = ""
title = "ANTLR with a Gradle Multi Project"
type = "post"
+++

ANTLR is a parser generator, a tool that helps you to create **parsers**. A parser takes a piece of text and transforms it in an organised structure, such as an Abstract Syntax Tree (AST). You can think of the AST as a story describing the content of the code, or also as its logical representation, created by putting together the various pieces.

The three basic steps to get an AST are:

1. Define a lexer and parser grammar
2. Invoke ANTLR to generate the lexer and parser in Java (other languages are possible. Using Java on this example)
3. Use the generated lexer and parser: Passing the text to parse and obtaining the AST

{{< img-post path="/img/antlr/" file="overview.png" alt="Module layout" type="center" >}}

### References:

* _Photo by {{< url-link "PDPics" "https://pixabay.com/en/grammar-magnifier-magnifying-glass-389907/" >}} on {{< url-link "Pixabay" "https://pixabay.com" >}}_

* _{{< url-link "The ANTLR Mega Tutorial" "https://tomassetti.me/antlr-mega-tutorial/" >}}_
