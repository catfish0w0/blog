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
tags:
  [
    data structure,
    algorithm,
    advanced data structure,
    monoStack,
    leetcode,
    Java,
  ]
# thumbnail image for post
img: ":monoStack/plates.jpg"
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

#### What is monotonic Stack??

A monotonic stack, also known as a monostack, is a data structure based on the **stack** concept. It shares the same implementation as a regular stack, differing only in its usage and behavior.

A monostack maintains a specific ordering of elements, and every it will keep everything consistant to avoid violation of the ordering. To gain a deeper understanding, here is an example of traversing an array with monostack. there are four types of monotonic stacks: increasing stack, non-decreasing stack, decreasing stack, and non-increasing stack.

Example:\
an array of [1, 7, 2, 3, 6, 2, 10]

| index | value | Increasing MonoStack | Decreasing MonoStack | Non-Dec MonoStack  | Non-Inc MonoStack |
| :---: | :---: | -------------------- | -------------------- | ------------------ | ----------------- |
|   0   |   1   | [1]                  | [1]                  | [1]                | [1]               |
|   1   |   7   | [1, 7]               | [7] kick 1           | [1, 7]             | [7]               |
|   2   |   2   | [1, 2] kick 7        | [7, 2]               | [1, 2]             | [7, 2]            |
|   3   |   3   | [1, 2, 3]            | [7, 3] kick 2        | [1, 2, 3]          | [7, 3]            |
|   4   |   6   | [1, 2, 3, 6]         | [7, 6] kick 6        | [1, 2, 3, 6]       | [7, 6]            |
|   5   |   2   | [1, 2] kick 2,3,6    | [7, 6, 2]            | [1, 2, 2] only dif | [7, 6, 2]         |
|   6   |  10   | [1, 2, 10]           | [10] kick 7,6,2      | [1, 2, 2, 10]      | [10]              |

## When && Why do we have MonoStack??

The Monostack exists because it leverages the advantages of a Stack, offering fast operations for pushing, polling, and peeking the top element with O(1) time complexity. By applying certain ordering in offering and polling conditions, it becomes highly efficient in finding the desired elements.

#### How/What can monotonic Stack do??

It has 2 common uses cases:

1. finding the **next greater/smaller/greater equals/smaller equals element**
2. finding the **prev greater/smaller/greater equals/smaller equals element**

For example: &ensp;[3, 7, 8, 4]\
The previous smaller element of 7 is 3.&ensp; The next smaller element of 8 is 4.\
The previous smaller element of 8 is 7.&ensp; The next smaller element of 7 is 4.\
The previous smaller element of 4 is 3.\
There is no previous less element for 3.&ensp; There is no next smaller element for 3 and 4.

```Java
//Increasing MonoStack, use case: find the next smaller element:
for (int i = 0; i < array.length; i++) {
   // if the new seeing current element less than the top element, that means it violates the increasing order
   // so we will poll it from the stack, by that time,
   // we know that the next smaller element for the polled element is the current array[i]!
   while (!stack.isEmpty() && array[i] <= stack.peekFirst()) {
      // if the element smaller than or equal to the stack top element, poll him down
      stack.pollFirst();
   }
// Dont forget, offer back
stack.offerFirst(array[i]);
}
```

###### Other different types of monoStack:

**Decreasing monostack:**\
Just change to this !stack.isEmpty() && array[i] >= stack.peekFirst()

**non-increasing monostack:**\
Just change to this !stack.isEmpty() && array[i] > stack.peekFirst();

**non decreasing monostack:**\
Just change to this !stack.isEmpty() && array[i] < stack.

##### Practice Questions:

**Basic Question 1: Find the next greater element in the array.**\
Entity:\
Input: int[] array\
Output: int[] outputNextGreaterArray

Assumption:

1. it is an int array
2. unsorted

Example: 1, 7, 2, 3, 6, 2, 10\
return [ 7 10 -1 2 2 -1 -1 //left side first smaller element, use decreasing stack from left to right

**Method 1 Brute Force:**

For each element,\
&emsp;find the first one that is larger than him from left to right.

TC: O(n^2)&emsp;SC: O(1)

**Method 2 MonoStack:**

What is inefficient in the above approach??

1. Everytime we are finding the next element in the array, we traverse almost the whole array to find the next greater element. This requires O(n^2) of time to check through. So what we can do is to find the next greater element in one time using monostack, since by only maintaining a stack with decreasing order, we can find the next greater element in O(1) time for each element.

Which kind of monoStack should we be using??\
Let's go through an example to find out!\
&emsp;&emsp;1, 7, 2, 3, 6, 2, 10\
**increasing stack:** if you go through the example, you will see it does not work, because if you offer first 2 to the stack, you will need to poll 7 out, but there is a next greater element for 7, and that polling would not allow us to update the element. So the increasing mono stack does not help us solve the problem.

**decreasing stack:** -1, -1, 7, 7, 7, 6, -1

TC: O(n)&emsp;SC: O(n)

Code:

```Java
public int[] firstLargerElementFromLeft(int[] array) {

   int[] result = new int[array.length];
   Deque<Integer> monoStack = new LinkedList<>(); // decreasing monoStack

   //it is easier to update when we find the next greater element for the specific element.
   Arrays.fill(result, -1);

   for (int i = 0; i < array.length; i++) {
      while (!monoStack.isEmpty() && array[i] > array[monoStack.peekFirst()]) {
         int prevElementIndex = monoStack.pollFirst();
         result[prevElementIndex] = array[i];
      }
      monoStack.offerFirst(i);
   }
   return result;
}
```

<hr>

**Basic Question 2: Find the distance of each element with the next first right side greater element in the array.**

Most of the time, the usecase is not that simple. In most interview questions or leecodes, we are using the relationship between the next first greater element or finding the distance in between.

The concept from the last question can be used. But the actual element that we store in the stack might be different.\
There are two common ways to handle this.

1. Use a wrapper class and the stack store Wrapper object
2. Seeing an array, and then we can use the index.

```Java
// 1st way
Deque<Wrapper> monoStack;
class Wrapper {
   int index;
   int value;
}

// 2nd way
while (!stack.isEmpty() && array[i] > array[stack.peekFirst()]) {
   stack.pollFirst();
}
stack.offerFirst(i);

// Code for finding the distance between current and next greater element.
public int[] distanceBetweenNextGreaterElement(int[] array) {

   int[] distance = new int[array.length];
   Deque<Integer> monoStack = new LinkedList<>(); // decreasing monoStack

   for (int i = 0; i < array.length; i++) {
      while (!monoStack.isEmpty() && array[i] > array[monoStack.peekFirst()]) {
         int prevElementIndex = monoStack.pollFirst();
         result[prevElementIndex] = i - prevElementIndex + 1;
      }
      monoStack.offerFirst(i);
   }
   return result;
}
```

<hr>
#### More Practice Questions

I have included all the problem links and solution links below.\
Here are some basic questions.

| Problem Number |                                     Problem                                      |                                                   Solution                                                   |
| :------------: | :------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------: |
|       1        |      [Daily Temperature](https://leetcode.com/problems/daily-temperatures/)      | [Solution](https://docs.google.com/document/d/1DXHJKdnaE7C69u7kko8H9SFAMWWwh_PDT7EoAK-n8hE/edit?usp=sharing) |
|       2        | [Next Greater Element 1](https://leetcode.com/problems/next-greater-element-i/)  | [Solution](https://docs.google.com/document/d/1z2zafEKWKmZMKgyNBgVQDRakjf7A9bIJBgFEcy5dDFA/edit?usp=sharing) |
|       3        | [Next Greater Element 2](https://leetcode.com/problems/next-greater-element-ii/) | [Solution](https://docs.google.com/document/d/1YVORE08cpUbG6aOFAVyl4RHWPcQT9BDKlDO5vyM595Y/edit?usp=sharing) |
|       4        | [Next Greater Element 4](https://leetcode.com/problems/next-greater-element-iv/) | [Solution](https://docs.google.com/document/d/1pjTw3r6tAGVCjsjw3wtbwDNt_t_eJHsD1S29OIvsTqI/edit?usp=sharing) |

Dive Deeper to Monotonic Stack

| Problem Number |                                                    Problem                                                    |                                                   Solution                                                   |
| :------------: | :-----------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------: |
|       5        |                     [Online Stock Span](https://leetcode.com/problems/online-stock-span/)                     | [Solution](https://docs.google.com/document/d/1ZP1vh_PqEnUOD4LteSoVPva2Uvth8bdUdDAOOST6BvM/edit?usp=sharing) |
|       6        | [Shortest Unsorted Continuous Subarray](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/) | [Solution](https://docs.google.com/document/d/1NfLHiIG-V3IJKC196NTV57uKpwDr1BlZ1LvR2bMmOqY/edit?usp=sharing) |
|       7        |        [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)        | [Solution](https://docs.google.com/document/d/10_bI7vbCZiKnYm6XcuLchmmpgVh92Yqf1nqkHCK-UVM/edit?usp=sharing) |
|       8        |                     [Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/)                     | [Solution](https://docs.google.com/document/d/1HoG7YtxGxaZ-a0gmEIE_iAOxA3E7fEmZv83x2_93dIg/edit?usp=sharing) |
