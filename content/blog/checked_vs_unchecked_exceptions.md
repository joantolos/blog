+++
author = "Joan Tolos"
categories = ["code"]
date = "2022-03-16"
description = "Definition and examples"
featured = "pic01.png"
featuredalt = ""
featuredpath = "/img/exceptions/"
linktitle = ""
title = "Checked vs unchecked exceptions in Java"
type = "post"
+++

Some people asked me once on an interview the difference between checked and unchecked exceptions in Java. The question made sense because it was a follow up on a take home test that I did and we were discussing. I did some kind of exception treatment and we were talking about the choices I made.

I remember making a mental note at that moment because although I answered the question I was not satisfied about how I did it. So, this is me trying to expose a better response to that question.

## What is an exception

An exception is an unexpected event during a program execution that disrupts the normal instructions flow. This definition is common for pretty much any programming language and each one of them will have it's own nuances and ways to deal with exceptions. It is important to know the ways the language deals with exceptions, and be wise enough to choose well. A good exception treatment will really make a difference in a piece of software.

The concept of checked and unchecked exception is introduced by the Java compiler. Checked and unchecked exceptions are part of the basics of the language.

There are basically to ways to deal with an exception in Java:

1. The method can deal with the exception itself with a _try/catch_
2. The method can propagate the exception with a _throws_

Using the proper technique is very important not only for the correct execution of your code but it also helps a great deal in terms of readability and understanding of the code.

This is the exception Java class hierarchy:

{{< img-post path="/img/exceptions/" file="exceptionClassHierarchy.png" alt="Exceptions Hierarchy in Java" type="center" >}}                    

## Checked exceptions

Java compiler checks them in what it's called compiled time. So, the compiler won't let you go on if you don't deal with these exceptions.

Normally these are exceptions that point to scenarios outside the normal program flow... a SQL problem, a class not found, an input output problem, a file not found... This signals a problem with the proper resources the program needs to go on.

For example, the InputStream class will throw an InputOutputException and if you want to use an input stream, you will have to deal with that exception no matter what. The compiler will complain if you don't deal with it.

## Unchecked exceptions

Java compiler won't check them so they appear in what it's called execution time or runtime.

These are exceptions that don't go against the correct program execution, in principle... an arithmetic exception, an array growing uncontrollably or the famous (infamous) null pointer exception.

They can also be used to explicit your program domain like sending a "user not found exception" if you are trying to search for an user, or more specific logics. Used in that sense, these exceptions provide intent and context to the code, making it more easy to read and follow.

## Diferences

The exception itself has nothing special that makes it checked or unchecked. The same exception can be checked in some context and unchecked on another. It's the way it is treated on the code that will define it's nature.

## Best practices

- You may want to use checked exceptions when a method can't do what it is suppose to do. For example, the method "loadConfig" may throw a checked FileNotFound exception
- Checked exceptions are normally used for resources related problems but not for programming problems
- A nice way to define a method signature, it's to declare them close to the methods name. For example, a "findUser" method throwing a UserNotFoundException makes sense. So the consumer must deal with the problem of an user not found.

General rule is: If the consumer or the client of the method can recover from the exception, it can be checked. That way, the consumer can decide what to do with the exception adjusting it to serving it's interests. If the consumer can not reasonably recover from that exception, you may want to make it unchecked and deal with it locally.

## Conclusion

Dealing with exceptions is not trivial. In fact, error managing on software it's a whole art in itself. A good error managing in your software can make the difference between a nice software and a really good piece of software.

Theoretically, the only point where a program can interrupt it's execution is on startup because it lacks some resources... files, external connections or whatever it is. If the program can start, the rest of problems must be able to be dealt during execution without any need to stop or disrupt the program.

### References:

* _Photo by {{< url-link "Ricardo Gomez" "https://unsplash.com/@rgaleria?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" >}} on {{< url-link "Unsplash" "https://unsplash.com/s/photos/exception?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" >}}_
