+++
author = "Joan Tolos"
categories = ["Clean Code", "Refactoring", "Git", "Ethics"]
date = "2017-09-08"
description = "When coding is a waste of time"
featured = "pic01.jpg"
featuredalt = ""
featuredpath = "/img/theCodeThatShouldNotBe/"
linktitle = ""
title = "The code that should not be"
type = "post"
+++


## The context

We were asked to implement a new feature, let´s say, selling apples. Not groceries, not fruits, just apples. Well, maybe on the next Sprint we will add bananas to sell as well. But that´s it, apples now and bananas later.

We all love to code for lists instead of instances, so the coder assigned to the task designed a beautiful code supporting a whole list of fruits, even it was clear from the start that business just needed apples _for now_. The shipping day arrived and the code was delivered on time, nice and easy.

When planning the next Sprint, business tells the team that the users kind-of like the apple feature but not as much as they thought. Besides, the team responsible to prepare the bananas to sell, is raising their hand saying that they won´t be ready for the near future. Bananas are really hard (and expensive) to grown and collect, so business is clearly thinking about letting go the idea of adding bananas. But you know how business is... they won´t say _"we won´t sell bananas ever"_ because they don´t want to close any door, they say _"right now, it is not necessary"_.

## The mythical feature to be

The developer that made the feature was furious. He was also truly frustrated as his code will never be used on production.

Conclusion:
* A waste of time
* The code will never be on production

## Commented code

I don't even read it anymore. I just delete it and push the change. I can´t think of any reason to have commented code on the repository.

The code has to be ready to be shipped at any time, that is one of the Continuous Delivery principle

## Deleting code will make you free
