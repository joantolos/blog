+++
author = "Joan Tolos"
categories = ["AI","UOC","Search","Knowledge"]
date = "2017-11-22"
description = "Knowledge systems"
featured = "aiThree.png"
featuredalt = ""
featuredpath = "/img/ai/"
linktitle = ""
title = "Artificial Intelligence (Part Three)"
type = "draft"
+++



### Systems based on rules

### Systems with structured representation

The structured representation allows to _relate_ the units from which the knowledge is defined. This is accomplished modelling the interconnections between the objects of the domain. Some of this representations are:

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

:   _In abstraction, the problem of finding the solution field is search on a graph since we find a node which satisfies the property. As so, we can use all the search strategies {{< url-link "explained before." "http://www.joantolos.com/blog/aitwo/" >}}_

The algorithms must take into account the intersections where there are several paths: before considering what is in the object associated to the intersection, the nodes in the paths that carry it must have been taken into account from the origin.

To solve that problem, we can use the {{< url-link "topological sorting algorithm." "https://en.wikipedia.org/wiki/Topological_sorting" >}}

### Fonts:

* _{{< url-link "UOC - Intel·ligència artificial" "http://estudios.uoc.edu/es/asignaturas-libres/informatica-multimedia-telecomunicacion/inteligencia-artificial/presentacion#_euocuc322detallpreus_WAR_euocentrega2portlet_INSTANCE_MSj1_detallpreus" >}}_

* _Vicenç Torra i Reventós. Sistemes basats en el coneixement_

* _{{< url-link "Stefik, M. (1995). Introduction to Knowledge Systems. Morgan Kauffman." "https://www.amazon.es/Introduction-Knowledge-Systems-Mark-Stefik-ebook/dp/B01H5GQH7G/ref=sr_1_1?ie=UTF8&qid=1511341998&sr=8-1&keywords=Introduction+to+Knowledge+Systems" >}}_
