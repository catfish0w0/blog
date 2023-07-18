---
# multilingual page pair id, this must pair with translations of this page. (This name must be unique)
lng_pair: spring_1
title: How to build a backend web service with Java Servlet?

# post specific
# if not specified, .name will be used from _data/owner/[language].yml
author: Puff
# multiple category is not supported
category: Web Development
# multiple tag entries are possible
tags: [Java, Java Web Development]
# thumbnail image for post
img: ":servlet/Servlet.png"
# disable comments on this page
#comments_disable: true

# publish date
date: 2023-07-16 00:51:06 +0900
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

#### Introduction

Web development has come a long way since the early days of static HTML pages. Today, modern web development encompasses a broad range of technologies, tools, and practices that enable developers to build dynamic, interactive, and responsive websites and web applications. This field has evolved rapidly to meet the growing demands of users and to leverage advancements in technology.

#### What is Java Servlet??

Java Servlet is a Java programming technology that receives any request and returns in a response using related network protocols(for web applications, usually HTTP). It usually takes in a **Servlet container**, like Tomcat(blocking IO) or Netty(Non-blocking IO)...etc. When a client sends a request to the well configured servlet container, **the servlet container will invoke the corresponding servlet's methods, such as doGet() or doPost()**, based on the request type. After that, the servlet processes the request, generates a response, sends it back to the client, and makes the application functional.

Imagine a well-developed restaurant, the client side(frontend/UI) is the menu, the table, the seat, and the inside environment. The waiter itself is the Servlet that takes in any client's orders back to the kitchen. The kitchen is the server side that receives all the orders(HTTP request), cooks the recipe and returns the food(HTTP response) to clients.

#### Why do we need to learn Java Servlet?

It is because Servlet Technology is the low-level foundation for building dynamic and interactive web applications. Studying it can help us understand advanced technology, like other latest technology like Spring MVC, Spring Boot...etc. You will have to understand that starting with Java and plain Spring framework will pay for itself with a comprehensive understanding of the whole Spring Ecosystem, which Spring Boot builds upon.

Okay, I have done enough talking, let's jump right into the code.

<hr>
#### Implementation
Our Goal: To make the server able to receive HTTP request, and send back JSON Object as response.

Let's create a new Project java EE. I am using Intellij as my code editor.\
Here is the basic project set up.

![](:servlet/start_project.PNG){:data-align="center"}

Remember to click the servlet button afterward.

![](:servlet/servlet_click.PNG){:data-align="center"}

Just like we have mentioned, to make the servlet runnable, we need a servlet container. In this article, we are using Tomcat as the container. To embed Tomcat, **add the Tomcat dependency into our** <span style="color:red">**pom.xml**</span> file. And later, we can just invoke it in our ApplicationLauncher class.

using embed Tomcat(Tomcat 10.1.8 have embed version)

```
<dependency>
   <groupId>org.apache.tomcat.embed</groupId>
   <artifactId>tomcat-embed-core</artifactId>
   <version>10.1.8</version>
</dependency>
```
