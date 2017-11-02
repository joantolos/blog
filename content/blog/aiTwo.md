+++
author = "Joan Tolos"
categories = ["AI","UOC","Search"]
date = "2017-09-29"
description = "Problem solving and search"
featured = "aiTwo.png"
featuredalt = ""
featuredpath = "/img/ai/"
linktitle = ""
title = "Artificial Intelligence (Part Two)"
type = "post"
+++

{{< url-link "We have stablished" "http://www.joantolos.com/blog/aione/" >}} that intelligent activity is reached thought the use of **symbols** to represent the problem domain, **operations** over this patterns and **search** to select a solution from the possibilities.

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

### Fonts:

* _{{< url-link "UOC - Intel·ligència artificial" "http://estudios.uoc.edu/es/asignaturas-libres/informatica-multimedia-telecomunicacion/inteligencia-artificial/presentacion#_euocuc322detallpreus_WAR_euocentrega2portlet_INSTANCE_MSj1_detallpreus" >}}_

* _Vicenç Torra i Reventós. Resolució de problemes i cerca_

* _{{< url-link "Russell, S.; Norvig, P. (1995). Artificial Intelligence: A modern approach. Prentice-Hall." "https://www.amazon.es/Artificial-Intelligence-Modern-Approach-Global/dp/1292153962/ref=sr_1_1?ie=UTF8&qid=1506669275&sr=8-1&keywords=Artificial+Intelligence%3A+A+modern+approach" >}}_
