+++
author = "Joan Tolos"
categories = ["code"]
date = "2022-05-15"
description = "A simple problem solved for two different complexity times"
featured = "pic01.png"
featuredalt = ""
featuredpath = "/img/bigO2/"
linktitle = ""
title = "Big O notation example"
type = "post"
+++

Since I made the {{< url-link "post about Big O Notation" "http://www.joantolos.com/blog/big_o_notation" >}}, I have been exploring that knowledge using regular simple algorithms like calculating the size of an array and common stuff like that. Just adding a new dimension to the way I think about the problems and also re-thinking the good-old ways of doing stuff.

I use operations implemented on the programming language like accessing an element of an array and now and then I think about how those operations are actually implemented, and what their complexity in terms of Big O could be. I believe is a nice exercise to do from time to time.

I recently discovered this website where you can find several code challenges, submit your proposal and most important, they respond with how your solution performs against other submissions. The site is https://leetcode.com

I want to solve one of those problems and explain two different solutions, one of them performing better than the other and think about them in terms of Big O Notation.

This is the problem description as it is on the site:

# Two sum problem

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

Example 1:

    Input: nums = [2,7,11,15], target = 9
    Output: [0,1]
    Output: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:

    Input: nums = [3,2,4], target = 6
    Output: [1,2]

Example 3:

    Input: nums = [3,3], target = 6
    Output: [0,1]

Constraints:

- 2 <= nums.length <= 104
- -109 <= nums <= 109
- -109 <= target <= 109

Only one valid answer exists.

# The naive approach or the brute force approach

This would be my first try. Always.

Since I work with TDD, I feel very comfortable writing code that it is far from its final version. So, I establish all my tests cases and almost always go with the "brute force" approach to make my tests pass.

If we think of the problem of these terms, we end up with a couple loops. The highest order one, is taking the first element of the array and try the sum with the next one until the end, that is the second loop. And so on until we find the solution.

This is the code in Java:

    public int[] exponentialAlgorithm(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++){
            for (int j = 0; j < nums.length; j++){
                if (i != j && (nums[i] + nums[j] == target)) {
                    return new int[]{i, j};
                }
            }
        }

        return null;
    }

The only mystery is the if condition: the sum of the two elements must be the target and also, they must be different elements of the array, of course.



### References:
* _Photo by {{< url-link "John Barkiple" "https://unsplash.com/@barkiple?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" >}} on {{< url-link "Unsplash" "https://unsplash.com/s/photos/complexity?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText" >}}_
* _{{< url-link "LeetCode" "https://leetcode.com/problems/two-sum" >}}_
