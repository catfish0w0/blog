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

<hr>

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

<hr>

**[Shortest Unsorted Continuous Subarray:](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/)**\
**Problem Statement:**\
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
TC: O(n)&emsp;SC: O(1)

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

<hr>

**[Largest Rectangle in Histogram:](https://leetcode.com/problems/largest-rectangle-in-histogram/)**\
**Problem Statement:**\
Given an array, array[i] means the height of the bar, we want to find the 1 largest rectangle.

Assumption:

1. array[i] has no negative number

**Method 1 Brute Force:**\
We can try finding all possible rectangles in the given array.

for each left boundary in the array:
&emsp;for each right boundary in the array:
&emsp;&emsp;find the minimum height bar \* length

TC: O(n^3)&emsp;SC:O(1)

Code:

```Java
public int height(int[] array) {
   int n = array.length;
   int result = 0;

   for (int i = 0; i < n; i++) {
      for (int j = i + 1; j < n; j++) {
         int minimumHeight = Integer.MAX_VALUE;
         for (int k = i; k <= j; k++) { //calculate the height
            minimumHeight = Math.min(minimumHeight, array[k]);
         }
         result = Math.max(result, minimumHeight * (j - i + 1));
      }
   }
   return result;
}
```

<hr>

**Method 2: Optimized Brute Force:**\
We can optimize the above approach by seeing the fact that we dont need to find every possible subarray. What we need is just treating each height bar as the minimumHeight bar and see how far it can reach to its left and right sides.

TC: O(n^2)&emsp;SC:O(1)

Code:

```Java
public int height(int[] array) {
   int n = array.length;
   int result = 0;

   for (int i = 0; i < n; i++) {
      int leftIndex = i;
      int rightIndex = i;

      while (leftIndex > 0 && array[leftIndex] >= array[i]) {
         leftIndex--;
      }
      while (rightIndex < n - 1 && array[rightIndex] >= array[i]) {
         rightIndex++;
      }
      result = Math.max(result, array[i] * (rightIndex - leftIndex + 1));
   }
   return result;
}
```

**Method 3: Divided and Conquer:**\
we can see this problem by checking that the array height can be divided into the last array element, and then we are finding the minimum bar throughout the array \* the boundary from left to right.

Recursion Definition: find the minimum rectangle area with left and right boundary.

Base Case:
if (left > right) return 0
if (left == right) return array[left]

Subproblem:
recursion(left, i - 1), recursion(i + 1, right); i is the minimum bar.

Recursive definition:
Everytime, we search to find the minimum bar from left to right, after that we look for more to divided and conquer

return min(area, subproblem 1, subproblem 2)

```Java
public int height(int[] array) {
   int n = array.length;
   return findMinHeight(array, 0, n - 1);
}
private int findMinHeight(int[] array, int left, int right) {
   if (left > right) {
      return 0;
   }
   if (left == right) {
      return array[left];
   }

   // find minimum bar
   int minimum = Integer.MAX_VALUE;
   for (int i = left; i <= right; i++) {
      minimum = Math.min(minimum, array[i]);
   }

   return Math.min(minimum * (right - left + 1), Math.min(findMinHeight(array, left, i - 1), findMinHeight(array, i + 1, right)));
}
```

**Method 3: MonoStack:**\
What is inefficient in the above approaches??
A lot of repetition wasted on finding the subarray or searching the minimum bar throughtout the array or <span style="color:red">finding the left and right boundary</span> in the array.

We can then optimized approach by seeing the functionality of Increasing monoStack.
Example: heights = [2,1,5,6,2,3]

| index | value | Increasing MonoStack | Notes                                                      |
| :---: | :---: | -------------------- | ---------------------------------------------------------- |
|   0   |   2   | [2]                  |
|   1   |   1   | [1]                  | <span style="color:red"> right boundary of 2 is 1. </span> |
|   2   |   5   | [5] poped out [2, 1] |
|   3   |
