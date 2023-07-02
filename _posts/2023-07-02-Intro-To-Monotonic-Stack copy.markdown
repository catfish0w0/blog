---
# multilingual page pair id, this must pair with translations of this page. (This name must be unique)
lng_pair: monoStack_1
title: Intro to Monotonic Stack

# post specific
# if not specified, .name will be used from _data/owner/[language].yml
author: Puff
# multiple category is not supported
category: data structure and algorithm
# multiple tag entries are possible
tags: [data structure, algorithm, advanced data structure, leetcode, Java]
# thumbnail image for post
img: ":post_pic1.jpg"
# disable comments on this page
#comments_disable: true

# publish date
date: 2023-07-02 00:51:06 +0900
# seo
# if not specified, date will be used.
#meta_modify_date: 2022-02-10 08:11:06 +0900
# check the meta_common_description in _data/owner/[language].yml
#meta_description: ""

# optional
# please use the "image_viewer_on" below to enable image viewer for individual pages or posts (_posts/ or [language]/_posts folders).
# image viewer can be enabled or disabled for all posts using the "image_viewer_posts: true" setting in _data/conf/main.yml.
#image_viewer_on: true
# please use the "image_lazy_loader_on" below to enable image lazy loader for individual pages or posts (_posts/ or [language]/_posts folders).
# image lazy loader can be enabled or disabled for all posts using the "image_lazy_loader_posts: true" setting in _data/conf/main.yml.
#image_lazy_loader_on: true
# exclude from on site search
#on_site_search_exclude: true
# exclude from search engines
#search_engine_exclude: true
# to disable this page, simply set published: false or delete this file
#published: false
---

<!-- outline-start -->

<!-- outline-end -->

## What is monotonic Stack??

&ensp;Monostack is a **Stack**. You are right, you did not hear me wrong. Monostack is basically just the data structure stack. It does not have any difference in implementation in code. The only thing that differs is the use of the Stack.

&ensp;Monostack is a stack that follows specific ordering. To understand it thoroughly, it consists of 4 different types of monostack: increasing stack, non decreasing stack, decreasing stack, non increasing stack.

## What can monotonic Stack do??

&ensp;It has 2 common uses cases

&ensp;1. finding the next greater/smaller/greater equals/smaller equals element
&ensp;2. finding the prev greater/smaller/greater equals/smaller equals element

&ensp;For example: For example:
&ensp;[3, 7, 8, 4]  
&ensp;The previous smaller element of 7 is 3. The next smaller element of 8 is 4. <br>
&ensp;The previous smaller element of 8 is 7. The next smaller element of 7 is 4. <br>
&ensp;The previous smaller element of 4 is 3. <br>
&ensp;There is no previous less element for 3. There is no next smaller element for 3 and 4. <br>

## When && Why do we have MonoStack??

&ensp;Monostack exists because it utilizes the advantage of Stack on offering/polling/peeking top element in O(1) time Complexity.
and we can simply apply it based on this current usecase!

#### Questions usecase:

**Basic Question 1: Find the first right side greater element in the array.**

&ensp;Entity:
&ensp;Input: int[] array
&ensp;Output: int[] outputNextGreaterArray

&ensp;Assumption:

&ensp;1. it is an int array
&ensp;2. unsorted

Example
&emsp;&emsp; 1, 7, 2, 3, 6, 2, 10
&ensp;return [ -1 1 1 2 3 1 1 //left side first smaller element, use decreasing stack from left to right
&ensp;return [ -1 -1 7 7 7 6 -1 // left side first larger element

&ensp;**Method 1 Brute Force:**
&ensp;for each element,
&emsp;find the first one that is larger than him from left to right.

&ensp;**Method 2 MonoStack:**
&ensp;Use increasing monostack or decreasing monostack are okay.
&ensp;&emsp;&emsp;1, 7, 2, 3, 6, 2, 10
&ensp;increasing stack: -1 -1 7 7// not working, because for 3, supposed we have 7 to say
&ensp;decreasing stack -1, -1, 7, 7, 7, 6, -1

&ensp;when to update?
&ensp;Code:

```Java
public int[] firstLargerElementFromLeft(int[] array) {

   int[] result = new int[array.length];
   Deque<Integer> stack = new LinkedList<>(); // decreasing monoStack

   for (int i = 0; i < array.length; i++) {
      while (!stack.isEmpty() && array[i] >= stack.peekFirst()) {
         stack.pollFirst();
      }
      if (!stack.isEmpty()) { // if it has element inside
         // the first element in the stack is the first that is > the current element.
         result[i] = stack.peekFirst());
      } else {
         result[i] = -1;
      }
      stack.offerFirst(array[i]);
   }
   return result;
}
```

**Basic Question 2: Find the distance of each element with the next first right side greater element in the array.**
&ensp;Most of the time, the usecase is not that simple. In most interview questions or leecodes, we are using the relationship between the next first greater element or finding the distance in between.

&ensp;The concept from the last question can be used. But the actual element that we store in the stack might be different.

&ensp;There are two common ways to handle this.

&ensp;1. Use a wrapper class and the stack store Wrapper object
&ensp;2. Seeing an array, and then we can use the index.

```Java
// first way
Deque<Wrapper> monoStack;
class Wrapper {
   int index;
   int value;
}

// second way
   while (!stack.isEmpty() && array[i] > array[stack.peekFirst()]) {
      stack.pollFirst();
   }
   stack.offerFirst(i);
```

**[Daily Temperature:](https://leetcode.com/problems/daily-temperatures/)**

&ensp;Problem Statement:
&ensp;we are given an array of temperature, array[i] is the temperature at day i.
&ensp;return back an array such that the ith day wait result[i] day to get a warmer day.
&ensp;if it does not have a warmer day, result[i] should be 0.

&ensp;**Method 1 Brute Force:**
&ensp;for every day
&emsp;Look up to the right.

&ensp;**Method 2 MonoStack:**
