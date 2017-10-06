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
type = "draft"
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

### Fonts:

* _{{< url-link "UOC - Intel·ligència artificial" "http://estudios.uoc.edu/es/asignaturas-libres/informatica-multimedia-telecomunicacion/inteligencia-artificial/presentacion#_euocuc322detallpreus_WAR_euocentrega2portlet_INSTANCE_MSj1_detallpreus" >}}_

* _Vicenç Torra i Reventós. Resolució de problemes i cerca_

* _{{< url-link "Russell, S.; Norvig, P. (1995). Artificial Intelligence: A modern approach. Prentice-Hall." "https://www.amazon.es/Artificial-Intelligence-Modern-Approach-Global/dp/1292153962/ref=sr_1_1?ie=UTF8&qid=1506669275&sr=8-1&keywords=Artificial+Intelligence%3A+A+modern+approach" >}}_
