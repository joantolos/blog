+++
author = "Joan Tolos"
categories = ["typescript", "javascript", "tdd", "test"]
date = "2020-05-03"
description = "A possible implementation for sort and paginate an array"
featured = "pic01.png"
featuredalt = ""
featuredpath = "/img/tableManager/"
linktitle = ""
title = "How to sort and paginate your table with Typescript"
type = "post"
+++

You should always delegate your sorting and pagination needs to the data retriever engine that you are using. For example, if it is a classical relational database you should use ORDER BY, OFFSET, FETCH, LIMIT and whatever mechanisms you have available. Same thing with NoSQL databases. These things are designed to perform well when asking for this kind of sorting and pagination features. So, you should always go for them.

Having said that... let's say you are dealing with a small table that comes from a bunch of dynamic calculations and the price of implementing sorting and pagination "at the origin" of data is too high. You can choose to manipulate the results later, once the data is retrieved.

This is an example of that implementation using Typescript.

# A bit of requirements

Given a JSON array of objects, we want to be able to sort the array by any of the objects property ascending or descending order. There has to be an order by default, in case the user does not specify one.

The sorting should be determined by a string in that form:

    field:asc,otherField:desc

Order is important so, with that example we expect the array to be first sorted by _field_ ascending and then if there are repeats, use _otherField_ descending as tie breaker.

Also, we need to paginate, that means, return a portion of the array given a start and ending point.

# TDD Approach

I am always talking about the benefits of using Test Driven Development technique (as you can see {{< url-link "here" "http://www.joantolos.com/blog/tddcasestudy/" >}}, or {{< url-link "here" "http://www.joantolos.com/blog/katasongsapi/" >}}, or {{< url-link "here" "http://www.joantolos.com/blog/javascripttrifecta/" >}}, or {{< url-link "here" "http://www.joantolos.com/blog/tddallin/" >}}...)

First thing I like to do is ask myself: _"how I would like this code to work?"_ and then I write a suite of tests as if the code existed. That is the hard part about TDD: it forces you to think before start typing.

Now, I would like to be able to do something like this: **tableManager.arrange(array, order, start, end)**. Easy enough to understand eh?. Ok, here is the actual test suite for this happy path scenario:

    describe('Table manager', () => {
      it('should sort and paginate: first page of two hits', () => {...});
      it('should sort and paginate: second page of two hits', () => {...});
    });

Now, first thing I see is that this "table arrangement" is really to actions in order: fist you should order the entire array and then, with the array on the proper order, grab a portion of that array.

Let's say that TableManager will need help of some guy "Sorting" and some other guy "Pagination". Then the only "management" it has to do is: apply sorting and then apply the pagination, something like this (in pseudocode):

    arrange(..., ...) {
      return pagination.paginate(sorting.sort(...), ...)
    }

Now I can focus on the two separate actions alone, forgetting the whole. Let's think about the test suite for sorting:

    describe('Sorting', () => {
      it('should sort by dynamic list of columns ascending and descending with no repeats', () => {...});
      it('should sort by dynamic list of columns ascending and descending with repeats', () => {...});
      it('should sort by dynamic list of columns ascending and descending with repeats, ignoring case', () => {...});
      it('should sort by dynamic list of columns by default sorting', () => {...});
    });

Great, let's make those tests pass. Now I can focus on the pagination:

    describe('Pagination', () => {
      it('should retrieve page 2', () => {...});
      it('should retrieve page 3', () => {...});
      it('should leave the list alone when no page required', () => {...});
    });

Now that everything is defined, I have a clear vision of what I have to do, just follow the tests, make them pass. The actual coding becomes a bit trivial even.

If you are curious, my implementation is placed here: {{< url-link "https://github.com/joantolos/kata-code-jam/tree/master/table-manager" "https://github.com/joantolos/kata-code-jam/tree/master/table-manager" >}}

# Relevant parts of the code:

## Pagination:

    paginate(records, hits, offset) {
      if (this.isPaginationAllowed(hits, offset)) {
        return records.slice(offset, ((hits * 1) + (offset * 1)));
      }
      return records;
    }

    private isPaginationAllowed(hits, offset) {
      return hits > 0 && offset >= 0;
    }

## Sorting:

    sort(records, order) {
      const orders = order ? order.split(',') : this.defaultOrder;
      const ordersKey = orders.map(key => key.split(':')[0]);
      const ordersDirection = orders.map(key => key.split(':')[1]);
      return records.sort((record, nextRecord) => this.compare(record, nextRecord, ordersKey, ordersDirection));
    }

    private compare(record, nextRecord, ordersKey, ordersDirection, index: number = 0) {
      const currentKey = ordersKey[index];
      const currentDirection = ordersDirection[index];

      if (currentKey) {
        let minorCriteria;
        let majorCriteria;

        if (currentDirection === 'asc') {
          minorCriteria = -1;
          majorCriteria = 1;
        } else {
          minorCriteria = 1;
          majorCriteria = -1;
        }

        if (String(record[currentKey]).toLowerCase() < String(nextRecord[currentKey]).toLowerCase()) {
          return minorCriteria;
        } else if (String(record[currentKey]).toLowerCase() > String(nextRecord[currentKey]).toLowerCase()) {
          return majorCriteria;
        } else if (String(record[currentKey]).toLowerCase() === String(nextRecord[currentKey]).toLowerCase()) {
          return this.compare(record, nextRecord, ordersKey, ordersDirection, index + 1);
        }
      }
      return 0;
    }

Remember, try to avoid this kind of manipulations when you are dealing with huge amounts of data. Delegate this to the proper actor.

### References:
* _Photo by {{< url-link "Tim Sullivan" "https://stocksnap.io/author/timsullivan" >}} on {{< url-link "StockSnap" "https://stocksnap.io" >}}_
