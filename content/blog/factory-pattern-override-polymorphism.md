+++
author = "Joan Tolos"
categories = ["code"]
date = "2021-08-14"
description = "An example with code for both techniques implemented"
featured = "pic01.png"
featuredalt = ""
featuredpath = "/img/overridePolymorphism/"
linktitle = ""
title = "Override polymorphism and factory pattern with TypeScript"
type = "post"
+++

One of the main benefits of object oriented programming (OOO) is the possibility for polymorphism. Polymorphism is the provision of a single interface to entities of different types or the use of a single symbol to represent multiple different types. I find this feature difficult to match on other paradigms such as Functional Programming.

I recently stumbled upon a case on my work where override polymorphism was needed. I want to extrapolate a general example to be able to write about it.

# Overview

This is the basic overview of the code example for this code. Dog, Cat and Bird are implementing the interface Animal. Dog and Cat also extend the abstract class Mammal and override the abstract method "sound" and "imitation":

{{< img-post path="/img/overridePolymorphism/" file="classesDiagramTransparent.png" alt="Classes Diagram" type="center" >}}

Dog, Cat and Bird have one public method: **summary**, that will return the phrase:

Cat:

> The Cat is a Mammal that makes a noise called growl and it sounds something like "meow"

Dog:

> The Dog is a Mammal that makes a noise called bark and it sounds something like "woof"

Bird:

> The Bird makes a noise called warble and it sounds something like "twit"

# Factory builder pattern

First off, a factory builder is needed. Factory builder is one of the most common patterns and one of the "Gang of four design patterns" that you probably know.

For the present example, this is a very light weight version where a simple switch statement will create the proper class:

    public build(animalName: string): Animal {
        switch (animalName) {
          case 'dog': {
            return new Dog();
          }
          case 'cat': {
            return new Cat();
          }
          case 'bird': {
            return new Bird();
          }
        }
      }

You get the idea... the method returns an implementation of the interface Animal just depending on an id. For this case, the animal name.

# Overriding Polymorphism

Now, the interface has three methods:

    export interface Animal {

      summary();
      imitation();
      sound();

    }

Bird, which is not a mammal, implements all three of them as you should expect from an interface implementation. But Cat and Dog, only implement "imitation" and "sound". The summary one is implemented on the abstract class "Mammal", and not only that, it needs "sound" and "imitation" on it's implementation. That is why those two methods are declared as abstract on "Mammal" and where the override occur.

When an instance of Dog or Cat is created, the code of the abstract class becomes part of the instance and it chooses the abstract method implementation accordingly of what instance are you creating.

# Code example

I have made this little example in code on this repo: https://github.com/joantolos/kata-code-jam/tree/master/override-polymorphism

It is done on TypeScript which is not a very wise choose for this kind of example. Although TypeScript uses types, I have noticed that is kind of "loose" on what you can get away with. I believe I have done it right and made the right choices but a more Object Oriented "Hardcore" language like Java would have been more appropriate.

# Conclusion

Polymorphism is one of the best features of Object Oriented Programming. I find it very difficult to match. If used right, it can express the intention of the code very easily. Intent is the property of your code that will help you most for growing and maintaining it. It will also help others to understand.

### References:

* _{{< url-link "Wikipedia: Polymorphism" "https://en.wikipedia.org/wiki/Polymorphism_(computer_science)" >}}_
* _{{< url-link "Wikipedia: Factory method" "https://en.wikipedia.org/wiki/Factory_method_pattern#Java" >}}_
* _{{< url-link "Example repo" "https://github.com/joantolos/kata-code-jam/tree/master/override-polymorphism" >}}_
