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
&emsp;&ensp; initialize count = 1 (current day)
&emsp;&ensp; while compare the stack top and price >= stack top price
&emsp;&ensp; counting the days
&emsp;&ensp; offer new Stock data object into the stack.

TC: amortized O(1)
SC: O(n)

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

**[Shortest Unsorted Continuous Subarray:](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/)**
