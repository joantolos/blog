+++
author = "Joan Tolos"
categories = ["AI","UOC"]
date = "2017-12-05"
description = "An introduction to AI"
featured = "ai.png"
featuredalt = ""
featuredpath = "/img/ai/"
linktitle = ""
title = "Artificial Intelligence"
type = "draft"
+++

I have done an introduction to Artificial Intelligence (AI) course and I want to share my learning experience. This post covers my notes and summaries of the content of the course.

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

# Problem solving and search

We have stablished that intelligent activity is reached thought the use of **symbols** to represent the problem domain, **operations** over this patterns and **search** to select a solution from the possibilities.

At that point, we can see how to **formulate a problem** defining the _state space_.

# State space and problem representation

We have to create a model of the problem. This process will usually follow the steps:

1. Environment modeling
  We define an **STATE** as the world representation in a specific state.
  We have to deduce on our system...
    * What is an state?
    * What are the possible states?
    * How do we represent an state?
2. Actions modeling
  We call **ACTIONS** as the way to move from an state to another and the **BRANCHING FACTOR** as the number of actions that can be applied on an specific state.
  Then we can define the **STATE SPACE** which is the group of possible states and the group of actions.

  Here an STATE SPACE representation for the linear jigsaw puzzle problem:

  {{< img-post path="/img/ai/" file="stateSpace.png" alt="Module layout" type="center" >}}

3. Problem definition
  We can define the problem as the **initial state** and the **goal function**.

# Building a solution

We define the **solution** as the road through the _space state_ graph where, given an _initial state_, it will satisfy the _goal function._

The search algorithm chooses a node and consider the possible actions that can be applied. Each one of this actions creates a new steps group. This made the representation of the data structure as a tree, a searching tree.

{{< img-post path="/img/ai/" file="tree.png" alt="Tree layout" type="center" >}}

For the implementation we need the _data structure_ for the tree and the _functions_ for build and operate with the tree, that will define the following steps:

1. **Node Representation**

    A node will contain:
  * id
  * parent id
  * how is generated
  * state
  * additional info
1. **Data Structure**
  * Already expanded nodes (List)
  * Nodes to expand (Queue with priority)
      * Apply selection operation
      * Add nodes to the structure
1. **Algorithm**
  {{< img-post path="/img/ai/" file="algorithm.png" alt="Tree layout" type="center" >}}

# Not informed search strategies

The search strategy is defined by the following questions:

* Which node we have to expand?
* How to sort the not-expanded nodes?

1. **Amplitude search**
{{< img-post path="/img/ai/" file="amplitudeSearch.png" alt="Amplitude search" type="center" >}}
1. **Deep search**
{{< img-post path="/img/ai/" file="deepSearch.png" alt="Deep search" type="center" >}}
1. **Uniform Cost search**
The uniform cost search introduces the concept of the _cost_ of it's path from the initial state. We call that _g(h)_. This search is complete and optimal when that cost function is always positive.

We can consider the uniform cost search as a **generalisation of the amplitude search** when the cost of all operators are the same.

# Heuristic searches

In general, we can not know how close is a state from the solution. We will use a function that give us an _estimation_ from the node to the solution. That is called **heuristic function**.

An heuristic function is a function that applied to a node, estimates the cost of the best path between that node and a solution node. This function are represented as _h(n)_

1. **Avid Search**
The uniform cost search consider the cost only from the initial state. It does not take into consideration that the next node has to lead to a solution. Using an heuristic function _h(n)_ as a criterion to order the nodes on the ready to expand list, defines the avid search.
1. **A* Algorithm**
The **avid search** uses an heuristic function to estimate the node that correspond to the minimum cost from a node to the goal node. That choosing thought, makes the search not optimal nor complete. On the other hand, the **uniform cost search** minimises the cost of the path to origin node to current node.

The two algorithms are complementary, we can define a function:

**_f(n) = g(n) + h(n)_**

Where:

* **g(n)** is the cost from the initial state to n
* **h(n)** is the estimation from this node to the solution

We can establish that _f(n)_ is an estimation of the cost of the path going from an initial state to another state solution going through the current node _n_

The selection of the node to expand according to this function is what it is called **algorithm A*:**

{{< img-post path="/img/ai/" file="algorithmA.png" alt="Amplitude search" type="center" >}}

The completion and optimality of the algorithm A* depends on the heuristic function. An algorithm A* is optimal and complete when the heuristic function does not over-estimate the cost to reach the goal. If the heuristic function covers that case, it is an admissible heuristic function.

This is a representation of the A* algorithm on pseudo-code:

    begin
    	input the start node S and the set of GOALS of goal nodes;
    	OPEN <- {S}
    	G[S] <- 0;
    	PRED[S] <- null;
    	found <- false;

    	while OPEN is not empty and found is false do
    		begin
    			L <- the set of nodes OPEN for which F is the least;

    			if L is a singleton then let X be its sole element
    			else if there are any goal nodes in L
    				then let X be one of them;
    				else let X be any element of L;

    			remove X from OPEN and put X into CLOSED;

    			if X is a goal node then found <- true
    				else begin
    					generate the set SUCCESSORS of successors of X;
    					for each Y in SUCCESSORS do
    						if Y is not already on OPEN or on CLOSED then
    							begin
    								G[Y] <- G[X] + distance(X,Y);
    								F[Y] <- G[Y] + h(Y);
    								PRED[Y] <- X;
    								insert Y on OPEN;
    							end
    						else
    							begin
    								Z <- PRED[Y];
    								temp <- F[Y]-G[Z] - distance(Z,Y) + G[X] + distance(X,Y);
    								if temp < F[Y] then
    									begin
    										G[Y] <- G[Y] - F[Y] + temp;
    										F[Y] <- temp;
    										PRED[Y] <- X;
    										if Y is on CLOSED then
    											insert Y on OPEN and remove Y from CLOSED;
    									end;
    							end;
    				end;
    		end;

    	if found is false then output "Failure";
    	else trace the pointers in the PRED fields from X back to S, "CONSing" each node onto the growing list of nodes to get the path from S to X;
    end;

# Knowledge systems

The knowledge system solve the problems using an intense knowledge of the application field. The knowledge base, the inference system and the user interface are the components associated.

Building that kind of a system requires a big investment in time and resources and it has to be carefully evaluated if it is worth it.

You should only build a knowledge system when:

* The usual programming techniques can not solve the problem.
* There are experts that have a good structured knowledge of the system domain.
* We don´t always have human experience on the environments where the knowledge is needed.

If there is a point to build a knowledge system, then you have to build a **model.**

A model is an abstraction used for specific goals. When we know the model goal, we can do an approximation of the phenomena we want to model. It represents a structured way to understand the entities and the processes that allows to build the solution on the real world.
The model allows has to understand better the process and also be able to predict.

### Systems based on rules

These systems are used mostly to solve problems of _classification_ and _diagnose_. There are based on **facts** and **rules**

* Facts: Knowledge about the objects of the system.
* Rules: Establish the relation between the objects.
  * Follow this format: **IF** [_premise_] **THEN** [_conclusion_] where both premise and conclusion are assertions of the facts.

Using the facts and rules, the inference system extract conclusions about the knowledge base which can be concluding new facts or assert the certainty of a fact.

**Rule system architecture**

{{< img-post path="/img/ai/" file="ruleSystemArchitecture.png" alt="Rule system architecture" type="center" >}}

* **Rules base:** First formal aspect of the representation. It contains de group of **rules**, the info of the domain.
* **Working memory:** Second formal aspect of the representation. It contains the group of **facts** which are temporary and relative to the specific problem trying to solve.
* **Interpret:** It is the inference aspect, it concludes new facts.

About the cyclic system of inference:

{{< img-post path="/img/ai/" file="inference.png" alt="Inference" type="center" >}}

* **Recovery:** Selects the rules that we can apply. The selected sub group is named _conflict set_.
* **Refinement:** Selects a rule from the sub group.
* **Execution:** Applies the rule.

The cycle ends once it has been proven whatever it is we are trying to prove or the conflict set is empty. So, we have a goal (a solution state) and a search problem (the group of rules). We can apply the search strategies explained before.

**Strategies for drive the search**

* Textual order
* Refractoriness
* Recency
* Specificity

**Strategies for doing the inference**

* Forward reasoning

We start from the knowledge and start applying the rules until the goal is reached. To know if we can apply a rule, we look to the _precedent_. If it is fulfilled, it is added to the work memory the rule conclusions.

* Backward reasoning

We start from the goal and select the rules that fulfill the goal.

### Systems with structured representation

The structured representation allows to _relate_ the units from which the knowledge is defined. This is accomplished modeling the interconnections between the objects of the domain. Some of this representations are:

* Frames
* Semantic networks
* Scripts

The difference between them is blurry since their structure is similar: several concepts and relations between them. Using **Frames** as an example, it can represent concepts defining the situation and domain of the problem. It can take into account the typical values, the exceptions and the incomplete or redundant information. It also allows modifications, inclusions or suppressions of their properties, creating a frame restructure.

#### Formal Aspects

From the formal point of view, a frame system is a network where each node represents an object, and the arcs mean the relations that can be establish between the objects. This representation structures the knowledge in a similar way than the object oriented programming paradigm.

As so, the relation between the objects are the same of the OOP like:

* Class
* Sub Class
* Super Class
* Instance
* Inherence

{{< img-post path="/img/ai/" file="frameExample.png" alt="Frame example" type="center" >}}

There to fields types: member slot and own slot. Each instance of the class has a _copy_ of the member slot and can be modified and the own slot are belong to the frame, so each instances share them. Some of the elements typically included on the fields are:

* Values of the domain
* Reference to another frame, the value indicates an object of the same system. Like on the example above, we have Maria as the owner of the frame car.
* Value restrictions
* Functions: The frame as a function associated that it is called every time there is a need of calculate the field.
* Demons: Procedures called as _secondary effect_ of a relevant action on the knowledge base.

#### Inferential Aspects

When asking to a frame representation, the problem normally is to know if an object satisfies some property or to know the value that an specific field associates with the object. For doing that, the frame system uses inherence to find _the field_ which is solution to the problem.

It can be a problem when there is multiple inherence (which happens most of the time). Depending of the order on which the relations are considered, the system will answer one thing or another. So, the multiple inherence is a _search problem_ because to find a result, we have to consider different alternatives and not all of them lead to a solution.

:   _In abstraction, the problem of finding the solution field is search on a graph since we find a node which satisfies the property. As so, we can use all the search strategies explained before._

The algorithms must take into account the intersections where there are several paths: before considering what is in the object associated to the intersection, the nodes in the paths that carry it must have been taken into account from the origin.

To solve that problem, we can use the {{< url-link "topological sorting algorithm." "https://en.wikipedia.org/wiki/Topological_sorting" >}}

### Case based Systems

The case based reasoning is formed on the idea of using previous experiences and solve new situations in a similar way that we solved the previous ones.

O

#### Inferential Aspects

### Model based Systems

#### Inferential Aspects

### Fonts:

* _{{< url-link "UOC - Intel·ligència artificial" "http://estudios.uoc.edu/es/asignaturas-libres/informatica-multimedia-telecomunicacion/inteligencia-artificial/presentacion#_euocuc322detallpreus_WAR_euocentrega2portlet_INSTANCE_MSj1_detallpreus" >}}_

* _Vicenç Torra i Reventós. Què és la intel·ligència artificial_

* _{{< url-link "Haton, J.P.; Haton, M.C. (1993). L’intelligence Artificielle. París: Presses Universitaires de France" "https://www.amazon.es/Lintelligence-artificielle-Haton/dp/2130455123/ref=sr_1_1?ie=UTF8&qid=1505999369&sr=8-1&keywords=Haton+L’intelligence+Artificielle" >}}_

* _{{< url-link "Luger, G.F. (1995). Computation & Intelligence. Menlo Park: MIT Press." "https://www.amazon.es/Computation-Intelligence-Collective-Association-Artificial/dp/0262621010/ref=sr_1_1?s=foreign-books&ie=UTF8&qid=1505999286&sr=1-1&keywords=Luger+Computation+%26+Intelligence" >}}_

* _Vicenç Torra i Reventós. Resolució de problemes i cerca_

* _{{< url-link "Russell, S.; Norvig, P. (1995). Artificial Intelligence: A modern approach. Prentice-Hall." "https://www.amazon.es/Artificial-Intelligence-Modern-Approach-Global/dp/1292153962/ref=sr_1_1?ie=UTF8&qid=1506669275&sr=8-1&keywords=Artificial+Intelligence%3A+A+modern+approach" >}}_

* _Vicenç Torra i Reventós. Sistemes basats en el coneixement_

* _{{< url-link "Stefik, M. (1995). Introduction to Knowledge Systems. Morgan Kauffman." "https://www.amazon.es/Introduction-Knowledge-Systems-Mark-Stefik-ebook/dp/B01H5GQH7G/ref=sr_1_1?ie=UTF8&qid=1511341998&sr=8-1&keywords=Introduction+to+Knowledge+Systems" >}}_
