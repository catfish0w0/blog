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

Monostack is a **Stack**. You are right, you did not hear me wrong. Monostack is basically just the data structure stack. It does not have any difference in implementation in code. The only thing that differs is the use of the Stack.

Monostack is a stack that follows specific ordering. To understand it thoroughly, it consists of 4 different types of monostack: increasing stack, non decreasing stack, decreasing stack, non increasing stack.

## What can monotonic Stack do??

It has 2 common uses cases

1. finding the next greater/smaller/greater equals/smaller equals element
2. finding the prev greater/smaller/greater equals/smaller equals element

For example: For example:
[3, 7, 8, 4]  
The previous smaller element of 7 is 3. The next smaller element of 8 is 4. <br>
The previous smaller element of 8 is 7. The next smaller element of 7 is 4. <br>
The previous smaller element of 4 is 3. <br>
There is no previous less element for 3. There is no next smaller element for 3 and 4. <br>

## When && Why do we have MonoStack??

Monostack exists because it utilizes the advantage of Stack on offering/polling/peeking top element in O(1) time Complexity.
and we can simply apply it based on this current usecase!

[leetcode2023](./leetcode_questions/2021-08-10-Test-page1.markdown)
