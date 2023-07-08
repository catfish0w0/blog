---
# multilingual page pair id, this must pair with translations of this page. (This name must be unique)
lng_pair: monoStack_1
title: Dive Deeper Into Monotonic Stack

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
date: 2023-07-07 16:43:06 +0900
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

For a more comprehensive understanding of the definition and use cases of a monotonic stack, please refer to the initial post mentioned [here](./2023-07-02-Intro-To-Monotonic-Stack). This particular post will delve into various use cases of the monotonic stack in problem-solving on LeetCode problems.

**[Online Stock Span:](https://leetcode.com/problems/online-stock-span/)**\
**Problem Statement:**\
We want to implement a class that can support the stock span API.\
the span of the stock price is the number of consecutive days <= the given input price.

Assumption:

1. all stock price are integer.
2. we are only focusing on 1 stock.
3. no negative price(neglect shorting behavior)

Based on the Assumption, we can easily model the price of the stock as a list of integer.\
where **index** represent **the ith day**, and value represent the **stock price** itself.

**Method 1 Brute Force Linear Scan:**\
We can use an ArrayList to store every price that we have seen.\
int next (int price)\
&emsp;&ensp;add the price at the end of the arrayList\
&emsp;&ensp;initialize counter = 0\
&emsp;&ensp;traverse the arrayList from end to start to see how many consecutive days <= given input price.

**Method 2 MonoStack:**\
Where is the inefficient part in the above method??\
For this particular problem, we only want the consecutive days that is lower than or equals to the given price. If the price keeps increasing, we want to efficiently see all the price coverage <= current price, so we need a data structure to assit us to keep updating the most recent elements. One useful data structure is to use monoStack.

The monoStack only maintains previous stock price in decreasing order.\
The monotonic stack only stores the previous stock prices in decreasing order. When we retrieve a new data point, we compare it to the top element of our stack (<span style="color:red">as it represents the smallest stock price</span>). Additionally, we need to track the consecutive days where the price was lower than or equal to the current price, so that we can get the span in O(1) time. Therefore, our stack not only stores the stock prices but also maintains the information about the consecutive days.

Details:\
maintain a decreasing monoStack.\
int next(int price)\
&emsp;&ensp; initialize count = 1 (current day)\
&emsp;&ensp; while compare the stack top and price >= stack top price\
&emsp;&ensp; counting the days\
&emsp;&ensp; offer new Stock data object into the stack.

TC: amortized O(1)&emsp; SC: O(n)

Code:

```Java
static class Data {
   int stockPrice;
   int days;
   public Data(int price, int days) {
      stockPrice = price;
      this.days = days;
   }
}
Deque<Data> monoStack;
public StockSpanner() {
   monoStack = new LinkedList<>();
}

public int next(int price) {
   int count = 1;
   while (!monoStack.isEmpty() && price >= monoStack.peekFirst().stockPrice) {
      Data priceData = monoStack.pollFirst();
      count += priceData.days;
   }
   monoStack.offerFirst(new Data(price, count));
   return count;
}
```

**[Shortest Unsorted Continuous Subarray:](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/)**\
Problem Statement:\
given an array, find the shortest subarray such that you sort the subarray, and the whole array will be sorted in non-decreasing order.

entity:\
array -> non decreasing order -> increasing order with duplicate.\
return int length

**Method 1 Brute Force:**\
find all the subarary in the array\
for each index starting at i\
&emsp;&ensp;for each index ending at j\
&emsp;&ensp;&emsp;&ensp;if array from 0 to i - 1 is sorted\
&emsp;&ensp;&emsp;&ensp;if array from j + 1 to n is sorted\
&emsp;&ensp;&emsp;&ensp;update globalmin\

TC: O(n^3)&emsp;SC: O(1)

Code:

```Java
public int findShortestLength(int[] array) {
   int result = Integer.MAX_VALUE;
   int n = array.length;
   for (int i = 0; i < n; i++) {
      for (int j = i + 1; j < n; j++) {
         boolean isZeroToISorted = true;
         for (int k = 0; k < i; k++) {
            if (k > 0 && array[k] < array[k - 1]) {
               isZeroToISorted = false;
            }
         }
         boolean isJToNSorted = true;
         for (int k = j + 1; k < n; k++) {
            if (k < n && array[k] > array[k + 1]) {
               isJToNSorted = false;
            }
         }
         if (isZeroToISorted && isJToNSorted) {
            result = Math.min(result, j - i + 1);
         }
      }
   }
}
```

**Method 2: finding left boundary and right boundary like selection sort**\
compare every array[i] with every array[j], i < j < n;\
&emsp;&ensp;if array[j] < array[i], mean i j not in right position\
&emsp;&ensp;&emsp;selection is swapping, but not really swap for this question\
&emsp;&ensp;&emsp;record the position of nums[i], i;\
&emsp;&ensp;&emsp;and position of nums[j], j.\
&emsp;&ensp;&emsp;we want to mark the leftmost i, Math.min(i, left)\
&emsp;&ensp;&emsp;we want to mark the rightmost j, Math.max(j, right)

TC: O(n^2)&emsp;SC: O(1)

Code:

```Java
public int findUnsortedSubarray(int[] array) {
   // Method 2 Selection sort
   int left = array.length, right = 0;
   for (int i = 0; i < array.length - 1; i++) {
      for (int j = i + 1; j < array.length; j++) {
         if (array[j] < array[i]) {
            right = Math.max(right, j);
            left = Math.min(left, i);
         }
      }
   }
   return right - left < 0 ? 0 : right - left + 1;
}
```

what is inefficient in all the above methods?\
they all required nested loops. which is O(n^2)\
a lot of overlap calculation

**Method 3: sorting**\
sort the array\
compare two array, what is not identical\
TC: O(nlogn + n)&emsp;SC: O(1)

**Method 4: monoStack to determine the range**\
we can instead utilize the data structure to help us store the elements, and we determine the leftmost boundary and rightmost boundary by using increasing and decreasing stack. the meaning is to see whenever it violates the stack meaning, it will pop the element outside. and that we update the globalLeft and globalRight boundary.

What is not efficient in the above problem?\
the only thing we care is the value that i, and i + 1 not in sorted order.
So instead of using a stack, we can use just a variable to detect it.

TC: O(n)&emsp;SC: O(n)

Code:

```Java
public int findUnsortedSubarray(int[] array) {
   // Method 4
   Deque <Integer> monoStack = new LinkedList<>();
   int left = array.length, right = 0;
   for (int i = 0; i < array.length; i++) {
      while (!monoStack.isEmpty() && array[i] < array[monoStack.peekFirst()]){
         left = Math.min(left, monoStack.pollFirst());
      }
      monoStack.offerFirst(i);
   }
   monoStack.clear();

   for (int i = array.length - 1; i >= 0; i--) {
      while (!monoStack.isEmpty() && array[i] > array[monoStack.peekFirst()])
         right = Math.max(right, monoStack.pollFirst());
      monoStack.offerFirst(i);
   }
   return right - left > 0 ? right - left + 1 : 0;
}

```

**Method 5: no stack, only variable same idea.**\
TC: O(n)&emsp;SC: O(1)\

Code:

```Java
public int findUnsortedSubarray(int[] nums) {
   int end = -1;
   int max = nums[0];
   for(int i = 1; i < nums.length; i++){
      if(max > nums[i]){ // the left value is greater then current value
         end = i; // mark that index with end
      }
      else{
         max = nums[i];
      }
   }

   int start = 0;
   int min = nums[nums.length - 1];
   for(int i = nums.length - 2; i >= 0; i--){
      if(min < nums[i]){ // the right value is smaller then current value
         start = i; // mark that index with start
      }
      else{
         min = nums[i];
      }
   }
   return end - start + 1;
}
```
