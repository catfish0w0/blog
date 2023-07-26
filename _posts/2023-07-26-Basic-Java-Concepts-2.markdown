---
# multilingual page pair id, this must pair with translations of this page. (This name must be unique)
lng_pair: basc_java_2
title: Basic Data Structure and Concept of Java language

# post specific
# if not specified, .name will be used from _data/owner/[language].yml
author: Puff
# multiple category is not supported
category: Java Basic
# multiple tag entries are possible
tags: [Java]
# thumbnail image for post
img: ":java_basic/how_java_pass_variable/core_java_programming.jpg"
# disable comments on this page
#comments_disable: true

# publish date
date: 2023-07-26 10:42:06 +0900
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

#### Arrays in Java: Exploring the Data Structure and Java Libraries

Welcome to the second post of the Data Structure and Java Basic Series. In this installment, our primary focus will be on arrays in Java, as well as the **Arrays library** and the **Random library** that Java provides. If you have any confusion related to fundamental Java concepts or want to revisit the first post, which covers _how Java copies and passes variables in functions_, you can find it [here](https://www.catfish0w0.com/posts/2023-07-24-Basic-Java-Concepts).

<br>
#### What is an array??

An array is not only the most basic but also a special data structure in Java. Think of an array as an Object Type variable that stores data in a contiguous memory location. This arrangement allows arrays to exhibit extremely efficient functionality, also enabling them to logically implement various data structures. From linear data structures like lists, stacks, and queues to nonlinear data structures like Trie and adjacent lists, arrays are incredibly versatile.

One notable feature of Java is the use of static arrays. Unlike some other languages such as Python, which only have dynamic arrays (known as lists), Java supports both static and dynamic arrays. Static arrays have a fixed size defined during their creation, while dynamic arrays can grow or shrink as needed.

<br>
#### Why should we learn array / What is so special about array?

One intriguing aspect is that arrays are not explicitly defined in Java's source code. Unlike other data structures with defined classes or libraries, arrays are a **native construct** directly integrated into the language. When creating an instance of an array, the syntax differs slightly from other data structures, emphasizing its unique nature. At the same time, array **allows direct access** to elements, which provide **constant Time Complexity O(1)** for lookup and random access based on given index. It has no overhead and is widely supported by most languages.

<br>
###### Key Point 1: How do you create an array

In Java arrays, two main components are essential: the <span style="color:red">type</span> and the <span style="color:red">length</span>. When creating an array, it is imperative to specify its length; you cannot create an array without providing this crucial information

```java
public void static main(String[] args) {
    int[] array = new int[array.length]
    ElementType[] array = new ElementType[5];// Method 1 Output: {null, null, null, null, null}
    int[] array = new int[]{1, 2, 3, 4, 5};  // Method 2 Output: {1, 2, 3, 4, 5}
    int[] array = {1, 2, 3, 4, 5};           // Method 3 not recommended, because of readability. Output: {1, 2, 3, 4, 5}
}

```

<br>
###### Key Point 2: How do you access array elements / traverse an array?

In Java, you can access array elements using their index and the array's length. Let's consider an example array: {0, 0, 0, 0, 0}.

Indices: The indices start from 0, and each element is referenced by its corresponding index, **ranging from 0 to n-1** (no negative index or overlength index is allowed).

Length: The array's length is a **public field**, which is why we don't need to add parentheses when accessing it using array.length.

To visit an array at a random index, you use the expression array[index]. This is not calling a method; instead, it is akin to dereferencing and directly retrieving the value at the specified index.

For instance, to populate the array with values, consider the following loop:

```java
for (int i = 0; i < array.length; i++) {
    array[i] = i + 1;
}
// Output: {1, 2, 3, 4, 5}
```

In memory, the array is stored as shown below:
![](:java_basic/array/array1.png){:data-align="center"}

#### What is a matrix?

A matrix is a two-dimensional array with rows and columns (n \* m matrix). In Java, you can represent a matrix as **an array of arrays**.

**Important Note to understand**\
During interviews, it's essential not to assume that all matrices are of the form n \* m. Different matrices can have varying dimensions. For example:

Exmaple Matrix:

|  type  |                 look                 | Traversal                 | Comments                                                                       |
| :----: | :----------------------------------: | ------------------------- | ------------------------------------------------------------------------------ |
| sorted | 1, 2, 3<br /> 4, 5, 6<br /> 7, 8, 9  | 1, 2, 3, 4, 5, 6, 7, 8, 9 | traverse from left to right, top to bot<br /> form sorted sequence             |
| Young  | 1, 4, 7<br /> 2, 6, 8<br /> 3, 9, 12 |                           | Sorted from left to right in each row<br /> sorted from top to bot in each col |

<br>
###### Key Point 1: How do you create a matrix
```java
public static void main(String[] args) {
    int[][] matrix = new int[][]{{1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12}};
    System.out.println(“Original Matrix: “ + Arrays.deepToString(matrix));
}
```

###### Key Point 1: How do you traverse a matrix

```java
public static void main(String[] args) {
    int[][] matrix = new int[][]{{1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12}};
    for (int i = 0; i < matrix.length; i++>) {
        for (int j = 0; j < matrix[i].length; j++>) {
            System.out.print(array[i][j] + " ");
        }
        System.out.println();
    }
}
```
