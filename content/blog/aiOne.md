+++
author = "Joan Tolos"
categories = ["AI","UOC"]
date = "2017-09-21"
description = "What is AI?"
featured = "aiOne.png"
featuredalt = ""
featuredpath = "/img/aiOne/"
linktitle = ""
title = "Artificial Intelligence (Part One)"
type = "draft"
+++

I am going to study an introduction to Artificial Intelligence (AI) and I want to share my learning experience. This will be a series of post, minimum of five.

# History

On the early sixties, there was a gathering between several investigators interested on artificial intelligence, neural networks and automats theory as a consequence of the first works made on the field.

The following years there was a lot of progress on the field and several programs were design to solve numerous problems:

* Geometric problems
* Algebraic problems
* _Checkers_ players
* LISP programming language was invented

These programs were successful on limited domains, known as _micro-worlds_, but failed on the adaptation to real environments because of the following three factors:

1. Lack of knowledge on the application domain consistent only on a few syntactic manipulations.
1. Most of the problem had **{{< url-link "NP complexity class" "https://en.wikipedia.org/wiki/NP_(complexity)" >}}**. With low input knowledge, the problems could be solved, but with bigger input data, they were unsolvable.
1. The basic structures used to generate an intelligent conduct, had big limitations. The neuronal network couldn't learn the XOR function.

The problem resolution was based on a general purpose search engine with high cost. To lower that cost, the first search algorithms were developed, like **{{< url-link "Heuristic Search" "https://en.wikipedia.org/wiki/Heuristic_(computer_science)" >}}** and **{{< url-link "Alpha Beta Search." "https://en.wikipedia.org/wiki/Alpha–beta_pruning" >}}** Some kind of logic was starting to be developed to represent the knowledge domain of the application.

Other works were focused on add some kind of learning process to the applications:

* {{< url-link "The ID3 decision tree was created" "https://en.wikipedia.org/wiki/ID3_algorithm" >}}
* {{< url-link "Version space learning" "https://en.wikipedia.org/wiki/Version_space_learning" >}}
* {{< url-link "Backpropagation" "https://en.wikipedia.org/wiki/Backpropagation" >}}

Concepts like _uncertainty_ and _non precision_ started to be taken into account. With all those development, at the eighties, the first commercial systems where launched.

# Definitions and points of view



## Some applications

* **{{< url-link "Theorist (Newell, Shaw, Simon, 1957):" "https://en.wikipedia.org/wiki/Logic_TheoristLogic" >}}** An automatic theorem prover.

* **{{< url-link "Mycin (Shortliffe i Buchanan, 1975):" "https://en.wikipedia.org/wiki/Mycin" >}}** Designed to help on the recommendations of therapies fitted for a patients with bacterial infections.

* **{{< url-link "AM (Lenat, 1977):" "https://en.wikipedia.org/wiki/Automated_Mathematician" >}}** Experimental program to build theories on the mathematics field. From a group of arithmetic concepts, the software builds new concepts.

* **Prospector (Duda, 1979):** Helps locate minerals like copper and uranium. It was a huge success at the eighties when it recommended the excavation on a place where a large deposit of {{< url-link "molybdenum" "https://en.wikipedia.org/wiki/Molybdenum" >}} was found.

* **{{< url-link "EQP (McCune, 1997):" "https://en.wikipedia.org/wiki/William_McCune" >}}** The EQP system proved the robbing problem. It is a well known problem on boolean algebraic unsolved until then.

* **{{< url-link "Deep Blue (IBM, 1997):" "https://en.wikipedia.org/wiki/Deep_Blue_(chess_computer)" >}}** The first computer that won a human on chess. It won the world champion G. Kasparov. The program has knowledge of the domain included on the function used to evaluate the different games. Also, it included a large database with final-game data that allowed it to play a perfect game once achieved that stage.

# Characteristics

There are a lot of intelligent systems applied to several different environments but there are some commons elements on all of them:

1. **Use of symbolic information:** The information to process is _symbolic_. They have to reason about facts, abstract concepts and obtain conclusions.
1. **Use of domain description:** In order to find a solution, the systems have to know the problem environment.
1. **Use of incomplete, inaccurate or conflict data:** There is some level of uncertainty with the data to be processed.
1. **Use heuristic methods:** On the AI applications, we implement how to find the solution instead of a list of steps to follow. The heuristic methods, help to do that but don't grant success. Most of the times, there isn't a better solution, but they can found a good one enough to keep going.
1. **Are adaptive:** When the environment changes, the system has to be able to change it's behaviour.

### Fonts:

* _{{< url-link "UOC - Intel·ligència artificial" "http://estudios.uoc.edu/es/asignaturas-libres/informatica-multimedia-telecomunicacion/inteligencia-artificial/presentacion#_euocuc322detallpreus_WAR_euocentrega2portlet_INSTANCE_MSj1_detallpreus" >}}_

* _Vicenç Torra i Reventós. Què és la intel·ligència artificial_

* _{{< url-link "Haton, J.P.; Haton, M.C. (1993). L’intelligence Artificielle. París: Presses Universitaires de France" "https://www.amazon.es/Lintelligence-artificielle-Haton/dp/2130455123/ref=sr_1_1?ie=UTF8&qid=1505999369&sr=8-1&keywords=Haton+L’intelligence+Artificielle" >}}_

* _{{< url-link "Luger, G.F. (1995). Computation & Intelligence. Menlo Park: MIT Press." "https://www.amazon.es/Computation-Intelligence-Collective-Association-Artificial/dp/0262621010/ref=sr_1_1?s=foreign-books&ie=UTF8&qid=1505999286&sr=1-1&keywords=Luger+Computation+%26+Intelligence" >}}_
