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
img: ":java_basic/how_java_pass_variable/array.jpg"
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

Welcome to the second post of the Data Structure and Java Basic Series. In this blog, our primary focus will be on arrays in Java, as well as the **Arrays library** and the **Random library** that Java provides. If you have any confusion related to fundamental Java concepts or want to revisit the first post, which covers _how Java copies and passes variables in functions_, you can find it [here](https://www.catfish0w0.com/posts/2023-07-24-Basic-Java-Concepts).

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

###### Key Point 1: How do you create a matrix and traverse a matrix

```java
public static void main(String[] args) {
    int[][] matrix = {
        {1, 2, 3, 4},
        {5, 6, 7, 8},
        {9, 10, 11, 12}
    };
    System.out.println(“Original Matrix: “ + Arrays.deepToString(matrix));

    // traversal
    for (int i = 0; i < matrix.length; i++) {
        for (int j = 0; j < matrix[i].length; j++) {
            System.out.print(array[i][j] + " ");
        }
        System.out.println();
    }
}
```

In memory: matrix is located like this.
![](:java_basic/array/array2.png){:data-align="center"}

In summary: array in Java has its advantages and restriction\
Advantages:

1. Contant Time Complexity int lookup and random access operation

Restriction:

1. Static Typing
1. Cannot change in Size, add in size or delete elements require O(n) time complexity to copy the array.

#### Arrays Library: Exploring Java's Array Functionality

Having covered the fundamental concepts of arrays, let's now delve into how Java empowers developers with array functionality. Java provides a built-in class called Arrays within the Java utils library, offering a plethora of useful APIs for array manipulation. Understanding these methods and their underlying logic is crucial, especially when preparing for technical interviews. For more detailed information, you can refer to the [original Java Doc](<https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Arrays.html#equals(java.lang.Object%5B%5D,java.lang.Object%5B%5D)>). Let's explore the rich functionality that Java's Arrays library has to offer!

#### API Summary

###### API 1: toString() method

**Function Signature**: `public static String toString(Object[] a)`

The toString() API is specifically designed to provide a string representation of the elements within the array. For user-defined classes, Java will naturally print the memory location of the instance by default. However, if you desire Java to display the field values instead, you can override the toString() method within the class.

Example:

```java
public static void main(String[] args) {
    String[] array = {“Gary”, “Tom”, “Bob};
    System.out.println(Arrays.toString(array));  //Output: [Gary, Tom Bob]

    NewObject[] array = new NewObject[3];
    array[0] = new NewObject(1);
    array[1] = new NewObject(2);
    array[2] = new NewObject(3);

    System.out.println(Arrays.toString(array));  //Output: [1, 2, 3];

    static class NewObject {
        int x;
        NewObject(int x) {
            this.x = x;
        }
        //overriding the toString() method
        public String toString(){
            return Integer.toString(x);
        }
    }
}
```

###### API 2: deepToString() method

**Function Signature**: `public static String deepToString(Object[] a)`

The deepToString method returns a string representation of the "deep contents" of the specified array. If the array contains other arrays as elements, the string representation will encompass their contents and any nested arrays within them, continuing **recursively**.

Example Code:

```java
public static void main(String[] args) {
    int[][] matrix = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    System.out.println(Arrays.toString(matrix));      //Output: [[I@15aeb7ab, [I@7b23ec81, [I@6acbcfc0]
    System.out.println(Arrays.deepToString(matrix));  //Output: [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
}
```

Java Source Code:

```java
public static String deepToString(Object[] a) {
   if (a == null)
       return "null";

   int bufLen = 20 * a.length;
   if (a.length != 0 && bufLen <= 0)
       bufLen = Integer.MAX_VALUE;
   StringBuilder buf = new StringBuilder(bufLen);
   deepToString(a, buf, new HashSet<>()); // here is the recursion coming.
   return buf.toString();
}
```

###### API 3: sort() method

**Function Signature**: `public static void sort(Object[] a)`
`public static void sort(Object[] a, int fromIndex, int toIndex) // sort specific range`
`public static <T> void sort(T[] a, Comparator<? super T> c) // sort with given comparator`
`public static <T> void sort(T[] a, int fromIndex, int toIndex, Comparator<? super T> c) // sort specific range with given comparator.`

This API allows you to sort the specified array of objects into ascending order based on the natural ordering of its elements. However, a prerequisite for using this method is that the type of the array must implement the Comparable interface.

The term "natural ordering" refers to the default ordering of elements based on their inherent characteristics. For example, for numeric types, natural ordering is based on their numerical values, while for strings, it is based on their lexicographical order.

Java's Arrays.sort employs different sorting strategies depending on the array length:

If the array length is short, it uses dualQuickSort, a quicksort variation optimized for smaller arrays.\
For longer arrays, it employs TimSort, which proves to be more efficient for larger datasets.\
By leveraging these sorting strategies, Java's Arrays.sort can efficiently handle arrays of varying lengths and deliver optimal sorting performance for a wide range of use cases.

Example Code:

```java
public static void main(String[] args) {
    int[] array = {53, 11, 17, 84, 36, 24};
    System.out.println(“before sorting: ” + Arrays.toString(array)); // Output: {53, 11, 17, 84, 36, 24}
    Arrays.sort(array);
    System.out.println(“after sorting: ” + Arrays.toString(array));  // Output: {11, 17, 24, 36, 53, 84}
}
```

###### API 4: sort with reverseOrder

can only use this API when the class that has natural ordering() <- implement Comparable interface.

Example Code:

```java
    public static void main(String[] args) {
        NewObject[] array = new NewObject[6];
        array[0] = new NewObject(53);
        array[1] = new NewObject(11);
        array[2] = new NewObject(17);
        array[3] = new NewObject(84);
        array[4] = new NewObject(36);
        array[5] = new NewObject(24);

        System.out.println(Arrays.toString(array));     //Output: [53, 11, 17, 84, 36, 24]
        Arrays.sort(array);
        System.out.println(Arrays.toString(array));     //Output: [11, 17, 24, 36, 53, 84]
        Arrays.sort(array, Collections.reverseOrder());
        System.out.println(Arrays.toString(array));     //Output: [84, 53, 36, 24, 17, 11]
    }
    static class NewObject implements Comparable<NewObject>{
        int x;
        NewObject(int x) {
            this.x = x;
        }

        public String toString(){//overriding the toString() method
            return Integer.toString(x);
        }
        @Override
        public int compareTo(NewObject a) {
            return Integer.compare(this.x, a.x);
        }
    }
```

###### API 5: sort with reverseOrder

This API will return a fixed-size list backed by the specified array, which is also called List View of the array.

Example Code:

```java
public static void main(String[] args) {
    // create an array of String
    String[] array = new String[]{“abc”, “xyz”, “pqr”};
    List<String> list = Arrays.asList(array);

    // printing the list
    System.out.println(“The original array: “ + list);
}
```

However, this API could lead to serious problem if you do not pay attention to its underlying logic.

Java Source Code:

```java
public static <T> List<T> asList(T... a) {
   return new ArrayList<>(a);
}

private static class ArrayList<E> extends AbstractList<E> // <- private static class
   implements RandomAccess, java.io.Serializable
{
   @java.io.Serial
   private static final long serialVersionUID = -2764017481108945198L;
   @SuppressWarnings("serial") // Conditionally serializable
   private final E[] a;   // <- pay attention to this line
}
```

In fact, the asList method is not creating the Java.utils.ArrayList that we expect it to see. It creates an ArrayList that is an private inner class of Arrays(that means people would not be able to access it normally).

**Issues with Arrays.asList()**:

1. One limitation of using Arrays.asList() to create an ArrayList is that you cannot add or delete elements from this specific type of ArrayList. When attempting to add or delete elements, it results in a UnsupportedOperationException at runtime. For instance:

```java
public static void main(String[] args) {
    int[] array = {1, 2, 3, 4};
    List<Integer> list = Arrays.asList(array);
    list.add(5); // Output: java.lang.UnsupportedOperationException
}
```

2. Another important distinction is between reference types and primitive types. When using Arrays.asList() with arrays of reference types, modifications to the list also affect the original array.

```java
public static void main(String[] args) {
    String[] array = new String[]{"a", "b", "c"};
    List<String> list = Arrays.asList(array);
    list.set(0, "c");
    System.out.println(Arrays.toString(array)); // Output: [c, b, c] - The original array is changed.
    System.out.println(list); // Output: [c, b, c]
}
```

**How to create a real java.utils.ArrayList<>() as expected?**

```java
public static void main(String[] args) {
    String[] array = new String[]{"a", "b", "c"};
    List<String> list = new ArrayList<>(Arrays.asList(array));
    list.add("d"); // Output: {"a", "b", "c", "d"}
}
```

###### API 6: fill, fill with Range

**Function Signature**: `public static void fill(Object[] a, Object val)`
`public static void fill(Object[] a, int fromIndex, int toIndex, Object val)`

This API would assigns the specified Object reference to each element of the specified array of Objects. Be aware, if you are filling in a range, the toIndex is exclusive, that means it will fill elements until the index == toIndex. [fromIndex, toIndex)

Example Code:

```java
public static void main(String[] args) {
    int[] array = new int[]{1, 2, 3, 4, 5, 6};
    Arrays.fill(array, 0, 4, 8);
    System.out.println(“array filled in range: “ + Arrays.toString(array)); //Output: {8, 8, 8, 8, 5, 6}
    Arrays.fill(array, 10);
    System.out.println(“array fully-filled: “ + Arrays.toString(array));    //Output: {10, 10, 10, 10, 10, 10}
}
```

###### API 7: copyOf

**Function Signature**: `public static <T> T[] copyOf(T[] original, int newLength)`

This API copies the specified array, truncating or padding with nulls (if necessary) so the copy has the specified length. The underlying logic is to utilize the System.arraycopy method.

Example Code:

```java
public static void main(String[] args) {
    String[] name = new String[]{"John", "Gary", "Alan", "Liz"};
    String[] copyName = Arrays.copyOf(name, 2); //Output: [John, Gary]
    String[] copyRangeName = Arrays.copyOfRange(name, 0, 3); //Output: [John, Gary, Alan]
    System.out.println(Arrays.toString(copyName));
    System.out.println(Arrays.toString(copyRangeName));
}
```

###### API 8: equals and deepEquals

**Function Signature**: `public static boolean equals(Object[] a, Object[] a2)`
`public static boolean deepEquals(Object[] a1, Object[] a2)`
Equals method returns true if the two specified arrays of Objects are equal to one another.
The underlying logic for deepEquals is similar to deepToString(), using recursion to deep digging into the array parenthesis.

###### API 9: binarySearch

Does not recommend to use. As a software engineer, you should implement your own binarySearch method.!!

#### Practice Questions

| Problem Number |                        Problem                        |                                               Solution                                                |
| :------------: | :---------------------------------------------------: | :---------------------------------------------------------------------------------------------------: |
|       1        | [High Five](https://leetcode.com/problems/high-five/) | ![](https://docs.google.com/document/d/1UFcQUbRZRQLSstLyUknyV64j2rGflt3JZzaD8GRhdKI/edit?usp=sharing) |
