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

For a more comprehensive understanding of the definition and use cases of a monotonic stack, please refer to the initial post mentioned [here](./2023-07-02-Intro-To-Monotonic-Stack.markdown). This particular post will delve into various use cases of the monotonic stack in problem-solving on LeetCode problems.

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
int span (int price)\
&emsp;&ensp;add the price at the end of the arrayList\
&emsp;&ensp;initialize counter = 0\
&emsp;&ensp;traverse the arrayList from end to start to see how many consecutive days <= given input price.

**Method 2 MonoStack:**

**[Shortest Unsorted Continuous Subarray:](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/)**
