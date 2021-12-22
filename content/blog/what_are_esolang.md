+++
author = "Joan Tolos"
categories = ["code"]
date = "2022-10-15"
description = "An introduction to esoteric languages"
featured = "pic01.png"
featuredalt = ""
featuredpath = "/img/esolangs/"
linktitle = ""
title = "What are Esolang"
type = "post"
+++

There is a full community of coders working on what are called _Esoteric languages_ or **esolang** for short. This is one of those perks of the profession that makes me love it even more. The fact that this exists is awesome. It makes me proud to enjoy "the party" and being able to understand what they are doing.

# What are esolangs

An esoteric programming language, is a computer programming language designed to experiment with weird ideas, to be hard to program in, or as a joke, rather than for practical use.

It does not matter if the syntax is obfuscated and obscure, in fact, it can be it's sole goal. Before exploring what are actually the motivations to build such a language, I think it is relevant to clarify a concept that you will see again and again when looking into esolangs.

## What it means for a language to be _Turing complete_?

A programming language is Turing complete when you can implement any possible algorithm with it. It gets it's name from Alan Turing the great mathematician, computer scientist, logician, cryptanalyst, philosopher and theoretical biologist that coined the famous term "Turing machine": The mathematical model defining an abstract machine that manipulates symbols on a strip of tape according to a bunch of rules.

If you think about HTML for example... you can't implement Quick Sort in it. Same thing happens with SQL. Those languages are not Turing complete (I am not going to entertain the war with HTML being or not a programming language, it doesn't matter). Non Turing complete languages are designed to perform a very specific task (like talking to a database or a browser), and not for being used in a generic way.

Most of programming languages are Turing complete, sometimes are referred as "universal language" as well. When talking about Esolangs, it is important to point out if the language is Turing complete or not, so you can have an idea of what you can do with it.

**Big picture:** if the language contains loops, some form of functions, recursion, variable assignment... all the perks of a regular language, it probably is Turing complete. In fact, if you try to design a language right now, it would probably end up being Turing complete.

# Classes of Esolangs

There is a little but very active community online designing these new languages for all kind of purposes:

1. Recreation
2. Comedy
3. Computationally interesting
4. Multi coding o multi purpose

# Examples:

## Brainfuck

{{< url-link "Brainfuck" "https://esolangs.org/wiki/Brainfuck" >}} was invented by Urban Müller in 1993, in an attempt to make a language for which he could write the smallest possible compiler for the Amiga OS, version 2.0. He managed to write a 240-byte compiler. The language was inspired by FALSE, which had a 1024-byte compiler. Müller chose to name the language brainfuck (with the initial letter in lower case, although it is now often capitalised).

Hello World in Brainfuck:

	++++++++++[>+++++++>++++++++++>+++>+<<<<-]>++.>+.+++++++..+++.>++.<<+++++++++++++++.>.+++.------.--------.>+.>.

## Whitespace

{{< url-link "Whitespace" "https://esolangs.org/wiki/Whitespace" >}}, designed in 2003 by Edwin Brady and Chris Morris, is an imperative, stack-based, esoteric programming language that uses only whitespace characters—space, tab, and linefeed—as syntax. All other characters are ignored. Whitespace got a brief moment of fame when it was posted on Slashdot on April 1st, 2003. Most people took it as an April Fool's joke, while it wasn't.

Hello World in Whitespace:

{{< img-post path="/img/esolangs/" file="whitespace.png" alt="Hello World in Whitespace" type="center" >}}

Where blue means tab and red means space. That's right, only whitespace characters to code in this language.

# Multi purpose esoteric languages

There is a subset of esoteric languages that serve more than one purpose, and those are the ones I find the most interesting. It is really challenging to try to create one of those.

## Shakespeare

The {{< url-link "Shakespeare" "https://esolangs.org/wiki/Shakespeare" >}} Programming Language (SPL) is an esoteric programming language created by Karl Hasselström and Jon Åslund in 2001. The design goal of Shakespeare was, according to the Manual, to make a language with beautiful source code that resembled Shakespeare plays.

	Romeo, a young man with a remarkable patience.
	Juliet, a likewise young woman of remarkable grace.
	Ophelia, a remarkable woman much in dispute with Hamlet.
	Hamlet, the flatterer of Andersen Insulting A/S.

	                   Act I: Hamlet's insults and flattery.
	                   Scene I: The insulting of Romeo.
	[Enter Hamlet and Romeo]
	Hamlet:
	You lying stupid fatherless big smelly half-witted coward! You are as
	stupid as the difference between a handsome rich brave hero and thyself!
	Speak your mind!
	You are as brave as the sum of your fat little stuffed misused dusty
	old rotten codpiece and a beautiful fair warm peaceful sunny summer's
	day. You are as healthy as the difference between the sum of the
	sweetest reddest rose and my father and yourself! Speak your mind!
	You are as cowardly as the sum of yourself and the difference
	between a big mighty proud kingdom and a horse. Speak your mind.
	Speak your mind!
	[Exit Romeo]
	                   Scene II: The praising of Juliet.
	[Enter Juliet]
	Hamlet:
	Thou art as sweet as the sum of the sum of Romeo and his horse and his
	black cat! Speak thy mind!
	[Exit Juliet]
	                   Scene III: The praising of Ophelia.
	[Enter Ophelia]
	Hamlet:
	Thou art as lovely as the product of a large rural town and my amazing
	bottomless embroidered purse. Speak thy mind!
	Thou art as loving as the product of the bluest clearest sweetest sky
	and the sum of a squirrel and a white horse. Thou art as beautiful as
	the difference between Juliet and thyself. Speak thy mind!
	[Exeunt Ophelia and Hamlet]

	                   Act II: Behind Hamlet's back.
	                   Scene I: Romeo and Juliet's conversation.
	[Enter Romeo and Juliet]
	Romeo:
	Speak your mind. You are as worried as the sum of yourself and the
	difference between my small smooth hamster and my nose. Speak your
	mind!
	Juliet:
	Speak YOUR mind! You are as bad as Hamlet! You are as small as the
	difference between the square of the difference between my little pony
	and your big hairy hound and the cube of your sorry little
	codpiece. Speak your mind!
	[Exit Romeo]
	                   Scene II: Juliet and Ophelia's conversation.
	[Enter Ophelia]
	Juliet:
	Thou art as good as the quotient between Romeo and the sum of a small
	furry animal and a leech. Speak your mind!
	Ophelia:
	Thou art as disgusting as the quotient between Romeo and twice the
	difference between a mistletoe and an oozing infected blister! Speak
	your mind!
	[Exeunt]

This program prints "Hello world" when you run it with the Shakespeare interpreter. It uses a very complex way to evaluate the weight of the adjectives and other key words to work the program stack. But the great think about this is... you can represent the play...

## Recipe
Hello world, not eatable
Chocolate cake
Done it
Eat it
http://www.mike-worth.com/2013/03/31/baking-a-hello-world-cake/

## Piet
Piet_Mondrian
https://en.wikipedia.org/wiki/Piet_Mondrian
Couple of Piet pictures
https://www.dangermouse.net/esoteric/piet.html


Hello world in piet
http://www.bertnase.de/npiet/
Show it
Execute it
Show the physical picture

## Sonic Pi
Show the code for FizzBuzz
Make it sound

### References:
* _Photo by {{< url-link "Pixabay" "https://pixabay.com/photos/craft-tarot-divination-2728227/" >}}_
* _{{< url-link "Wikipedia: Turing machine" "https://en.wikipedia.org/wiki/Turing_machine" >}}_
