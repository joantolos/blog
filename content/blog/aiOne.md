+++
author = "Joan Tolos"
categories = ["AI","UOC"]
date = "2017-09-21"
description = "What is AI?"
featured = "aiOne.png"
featuredalt = ""
featuredpath = "/img/ai/"
linktitle = ""
title = "Artificial Intelligence (Part One)"
type = "post"
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

There is not a single definition of AI but a lot of them according different points of view. We are going to consider AI as a computer science field and how the different programs and applications define it.

The goals of the different programs will lead to different definitions:

* The goal of the program can be obtain an specific **conduct** or to obtain an specific **reasoning**. This **conduct/reasoning** pair makes the _first dimension_.
* On the other hand, it is required that the programs are **correct**. You can measure this correction comparing the performance with the performance on actual people or compared against an ideal concept of intelligence. This ideal is named _**rationality.**_ The way we measure the correction is the _second dimension_.

Using these two dimensions, there are four possible visions for the goals and so, four possible definitions:

1. **Act like people: The Turing test.** This definition is based on the proposal by **{{< url-link "Alan Turing" "https://en.wikipedia.org/wiki/Turing_test" >}}** defining intelligence as an operational way: A conduct is intelligence when has enough level to confuse a human interlocutor.
1. **Reason like people: The cognitive model.** In this definition, not only the result is important but also how it is obtained. The goal is for the process to be similar to the one made by humans. **{{< url-link "The General Problem Solver." "https://en.wikipedia.org/wiki/General_Problem_Solver" >}}**
1. **Reason rationally: The thoughts laws.** This point of view is based on considering what it means to think correctly or, what is equivalent, know when a new fact can be deduced logically from the knowledge of what is available.
1. **Act rationally: The rational agent.** What it is important is to reach the correct conclusions, not if the conclusions were obtained using logic deductions.

Considering the follow hypothesis:

* {{< url-link "The physical symbol system hypothesis" "https://en.wikipedia.org/wiki/Physical_symbol_system" >}}

* {{< url-link "Heuristic search hypothesis" "https://en.wikipedia.org/wiki/Heuristic_(computer_science)#Newell_and_Simon:_heuristic_search_hypothesis" >}}

We can achieve _intelligent activity_ with the use of:

* **Symbols:** The meaningful elements of a system.
* **Operations:** Operations between the symbols allowing us to generate solutions.
* **Search:** To select a solution from the possible ones generated from the operations.

This hypothesis explains the two most important elements on the development of AI applications:

1. Define the symbolic structures and operations to solve problems.
2. Define search strategies to find the potential solutions generated by these structures and operations.

## Three alternatives

This definition is challenged by other authors and other systems had been build following different hypothesis. These are based on different hypothesis:

1. **Biologic models based systems:**

    This alternative is based on _neuronal networks_. These networks represent the world thought the weight associated to each connection (or neuron), no symbols required.

1. **Emergent systems:**

    The solution to a problem is not obtained from a single individual system but emerges from the activities of independent agents (and relatively simple though usually specialists).

1. **Situated action theory:**

    The theories of the action argue that intelligence should not be seen as a process of building and evaluating models of the world, but rather as a less structured process of acting in the world and responding to results obtained. Therefore, more importance is given to the ability to act than when explaining these actions.

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
