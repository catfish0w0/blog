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

**Basic Question 1: Find the next greater element in the array.**
Entity:\
Input: int[] array\
Output: int[] outputNextGreaterArray

Assumption:

1. it is an int array
2. unsorted

Example: 1, 7, 2, 3, 6, 2, 10\
return [ 7 10 -1 2 2 -1 -1 //left side first smaller element, use decreasing stack from left to right\

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

**[Daily Temperature:](https://leetcode.com/problems/daily-temperatures/)**\
**Problem Statement:**\
we are given an array of temperature, array[i] is the temperature at day i. return back an array such that the ith day wait result[i] day to get a warmer day. if it does not have a warmer day, result[i] should be 0.

Entity:\
Input: int[] temperatures\
Output: int[] nextWarmerDay

Assumption:

1. the temperature of each day are stored in int[] array, index means the ith day
2. no need to calculate for the last forcasted days

**Method 1 Brute Force:**

for every day\
&emsp;Look up to the right.

TC: O(n^2)&emsp;SC: O(1)

**Method 2 MonoStack:**

Again, what is inefficient in the above approach?

1. we can easily spot that the array[i] is the temperature of the day, and we want to find the next day that is warmer(greater in value) for every ith day. This is basically asking the previous question in a different wording. So we can use decreasing monoStack to assit our traversal and find the results.

TC: O(n)&emsp;C: O(n)

```Java
public int[] dailyTemperatures(int[] temperatures) {
   int[] result = new int [temperatures.length];

   Deque<Integer> monoStack = new LinkedList<>();
   for (int i = 0; i < temperatures.length; i++) {
      while (!monoStack.isEmpty() && temperatures[i] > temperatures[monoStack.peekFirst()]) {
         // array[i] element is the first element that larger than the element in the stack
         int index = monoStack.pollFirst();
         result[index] = i - index;
      }
      monoStack.offerFirst(i);
   }
   return result;
}
```

<hr>

##### Next Greater Element Series:

**[Next Greater Element 1:](https://leetcode.com/problems/next-greater-element-i/)**\
**Problem Statement:**\
Given 2 arrays, array1 and array2. array1 is the subset of array2, we want to find the next greater element of each element in array1 that is in array2.

Entity:\
Input: int[] array1, int[] array2\
Ouput: int[] result

Assumption:

1. both unsorted int[] array
2. array1.length will not > array2.length

**Method 1 Brute Force:**

for each element in array1\
&emsp;Search it in array2\
&emsp;Find its next greater element in array2

TC: O(n^2)&emsp; SC: O(1)

**Method 2 MonoStack:**

What is inefficient in the Brute Force solution??

1. We dont know the location of our array1 element in the array2(the corresponding index), that is why we need extra linear time for each array1 element to search for the location(index) at array2 before we really start searching up the next greater element. In order to optimize it, we can use a data structure that help us fast look up the location of value in index1 to index2.
2. Even we find the location of each element in the array2, we still need the O(n) linear time to search for the next greater element in array2. **Can we first use linear time to store the next greater element in array2, and then later we can use linear time to find array1 element?**

The answer yes, and that is the approach to optimize the solution.\
We will need a HashMap <value, next greater element in array2> , because it helps us look up the next greater element in O(1) time complexity.

Details:\
&emsp;initialize the hashmap and result array\
&emsp;for each element in array2\
&emsp;&emsp;find and store the next greater element in array2\
&emsp;for each element in array1\
&emsp;&emsp;if we find the value in the hashmap\
&emsp;&emsp;&emsp;lookup the next greater element\
&emsp;&emsp;else\
&emsp;&emsp;&emsp;put -1;

TC: O(n)&emsp;SC: O(n)

```Java
public int[] nextGreaterElement(int[] array1, int[] array2) {
   Deque<Integer> monoStack = new LinkedList<>();
   // maintain decreasing monoStack traverse from right to left;
   //  value , next greater element
   Map<Integer, Integer> map = new HashMap<>();

   int[] result = new int[array1.length];
   Arrays.fill(result, -1);

   for (int i = 0; i < array2.length; i++) {
      while (!monoStack.isEmpty() && array2[i] > array2[monoStack.peekFirst()]) {
         int index = monoStack.pollFirst();
         map.put(array2[index], array2[i]);
      }
      monoStack.offerFirst(i);
   }

   for (int i = 0; i < array1.length; i++) {
      if (map.containsKey(array1[i])) {
         result[i] = map.get(array1[i]);
      }
   }
   return result;
}
```

<hr>

**[Next Greater Element 2:](https://leetcode.com/problems/next-greater-element-ii/)**\
**Problem Statement:**\
Given a circular integer array array (i.e., the next element of nums[nums.length - 1] is nums[0]), return the next greater number for every element in array.

Entity:\
Input: int[] array\
Ouput: int[] result

Assumption:

1. unsorted int[] array
2. it is a circular array

**Method 1 Brute Force:**

for each element in the array\
&emsp;for length from 1 to n, where n is array.length\
&emsp;&emsp;if array[i + length % n] > array[i]\
&emsp;&emsp;&emsp;add it to result\
&emsp;&emsp;&emsp;break;

TC: O(n^2)&emsp;SC:O(1)

**Method 2 MonoStack:**

What is inefficient in the Brute Force solution??

1. for every element, we traverse linear time again to search for the next greater element

It is finding next greater element, we can use decreasing monoStack to help us look up the next greater element. For elements near the array end, since it is a <span style="color: red;">circular array</span>, we can extend the array length by 2!

TC: O(2n)&emsp;SC:O(n)

Code:

```Java
public int[] nextGreaterElements(int[] array) {
   Deque<Integer> monoStack = new ArrayDeque<>(); // inside the monoStack, we put index.
   int[] result = new int[array.length];
   Arrays.fill(result, - 1); // set up the whole result array as -1.

   for (int i = 0; i < 2*array.length; i++) {
      // we are using a decreasing Stack
      while (!monoStack.isEmpty() && array[i % array.length] > array[monoStack.peekFirst()]) {
         int index = monoStack.pollFirst();
         result[index] = array[i % array.length];
      }
      monoStack.offerFirst(i % array.length);
   }
   return result;
}
```

<hr>

**Method 3 No extending the length:**

What if the interviewer wants solution other than extending the array length??

The challenge we encounter here is that when we traverse from left to right, the last element cannot "see" the element at the front. To address this, we need to store the order differently using a stack.

Consider the sequence [1, 2, 3, 4, 3]. Instead of storing it directly, we store it in a reverse order within the stack, so the last element can have visibility to the first element. This means we need to reverse the storage and traverse from right to left.

By making this clever adjustment, we ensure that elements can interact in a way that gives us the desired results. It's like flipping the sequence to create a seamless connection between elements, just like a well-orchestrated dance routine!

Details:
[1, 2, 3, 4, 3]\
&emsp;&emsp;&emsp;&emsp;i\
case 0: if stack is empty, we put result[i] = -1, and put our current element back to the stack\
case 1: if the stack top element < current, pop it out, because it is not our target.\
case 2: if the stack top elemetn > target, store it in result[i] && i--.\
&emsp;&emsp;&emsp;and do we need to put it back to the stack??\
&emsp;&emsp;&emsp;the answer is yes, because it can be larger than the current one.

TC: O(n)&emsp;SC:O(n)

Code:

```Java
public int[] nextGreaterElements(int[] array) {
   Deque<Integer> stack = new ArrayDeque<>();
   for (int i = array.length - 1; i >= 0; i--) {
      stack.offerFirst(array[i]);
   }
   int[] result = new int[array.length];
   for (int i = array.length - 1; i >= 0; i--) {
      while (!stack.isEmpty() && array[i] >= stack.peekFirst()) {
         stack.pollFirst();
      }
      // if the stack is empty, that means the current element is the largest among the circular array
      if (stack.isEmpty()) {
         result[i] = -1;
      // else just look up the stack top, which means it is the next larger element.
      } else {
         result[i] = stack.peekFirst();
      }
      stack.offerFirst(array[i]);
   }
   return result;
}
```

<hr>

(No Next Greater Element 3, because it is unrelated to monostack topics)\
**[Next Greater Element 4:](https://leetcode.com/problems/next-greater-element-iv/)**\
**Problem Statement:**\
Given an array, find the second largest Element for each element in the array.

Example: [3, 5, 7, 7, 9, 10, 5, 7]\
return: [7, 7, 10, 10, -1, -1, -1, -1]

Entity:\
Input: int[] array\
Output: int[] result

Assumption:

1. return -1, if it has no second largest elements.

**Method 1 Brute Force:**

for each element in the array\
&emsp;linear scan for the second Largest Element;

TC: O(n^2)&emsp; SC: O(1)

**Method 2 MonoStack:**

What is inefficient in the Brute Force solution??\
linear scanning does a lot of extra work as we have encountered before.

How to make it efficient?\
The typical use case for a monoStack is to find the next greater element. However, in our current scenario, we need to find the second-largest elements, which are essentially the next-next greater elements that we've seen. To achieve this, we can try using two monoStacks. One Stack will hold every element we've encountered, while the other will hold elements that have already encountered one greater element. This approach seems reasonable.

But, can we really solve the problem using only two monoStacks?\
 The answer is no. Let's illustrate with an example: 7 5 9 3 6.
Decreasing Stack 1: \
Decreasing Stack 2: \
The reason we can't solely rely on two stacks is that if we pop and offer elements in the stack just once, the order will be reversed! Unfortunately, there are cases like the one above where we must maintain the same order as we've encountered. Otherwise, elements like 5 won't "see" 6, and this would violate the meaning of our approach and monotonic decreasing stack. Therefore, we need an extra <span style="color:red">buffer</span> stack to help us maintained the original order.(Please see my other stack post, this is very similar to one of the use case Deque by Three Stacks).

TC: O(n)&emsp;SC: O(n)

Code:

```Java
public int[] nextGreaterElements(int[] array) {
   Deque<Integer> monoStack1 = new LinkedList<>();
   Deque<Integer> monoStack2 = new LinkedList<>();
   Deque<Integer> bufferStack = new LinkedList<>();
   int[] result = new int[array.length];
   Arrays.fill(result, -1);

   for (int i = 0; i < array.length; i++) {
      // Why compare with decreasing stack 2 first??
      // Because stack 2 are the element that first see the second largest elements; where we store the result
      while (!monoStack2.isEmpty() && array[i]  > array[monoStack2.peekFirst()]) {
         int index = monoStack2.pollFirst();
         result[index] = array[i]; //current element is the second largest element in the array;
      }

      while (!monoStack1.isEmpty() && array[i] > array[monoStack1.peekFirst()]) {
         // since the current element larger than the one in monoStack1, we
         // first offer into buffer stack to avoid messing up the order.
         bufferStack.offerFirst(monoStack1.pollFirst());
      }
      // if buffer stack has something, we offer it into our decreasing stack 2.
      while (!bufferStack.isEmpty()) {
         monoStack2.offerFirst(bufferStack.pollFirst());
      }
      // remember, offer current elemnt to the decreasing stack 1.
      monoStack1.offerFirst(i);
   }
   return result;
}
```

<hr>
