---
# multilingual page pair id, this must pair with translations of this page. (This name must be unique)
lng_pair: basc_java_1
title: Basic Data Structure and Concept of Java language

# post specific
# if not specified, .name will be used from _data/owner/[language].yml
author: Puff
# multiple category is not supported
category: Java Basic
# multiple tag entries are possible
tags: [Java]
# thumbnail image for post
img: ":java_basic/core_java_programming.jpg"
# disable comments on this page
#comments_disable: true

# publish date
date: 2023-07-24 12:34:06 +0900
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

This will be the first post of the Data Structure and Java Basic Series. In this series I will be This is the inaugural post of the <span style="color:red">**Data Structure and Java Basic Series**</span>. Throughout this series, I will cover various topics, including the fundamentals of Java programming, the practical Java utils library, and eventually, delve into data structures in Java, among other subjects. For this specific post, the primary focus will be on the concept of how Java passes variables in functions.

#### Java Fundamental Concepts

Before delving into the concept of variable passing, let's explore some fundamental concepts in Java. Unlike languages such as JavaScript and Golang, Java operates on two key principles:

1. **No program without a class**: At least one class is required to execute any Java program.
2. **No object without a class**: Creating an object using a class to define its **attributes** and **method/function**.

#### Variables in Java

In light of this, Java relies heavily on two types of variables: **primitive types** and **object types**.

**Primitive Types**: These include basic data types like byte, short, integers, long, floating-point numbers, double, characters, and booleans. They are directly supported by the hardware and have limited size and behavior.\
**Object Types**: These refer to variables that can hold references to objects in memory. Objects are instances of classes and allow developers to define more complex data structures and behavior.

#### How does Java copy variables and allocate memory??

In Java, variables are stored in two spaces in the CPU: the Stack and the Heap. When you declare a primitive data type in Java, a memory location in the stack is assigned to store the primitive data type. This is referred to as deep copying. For instance:

```Java
int a = 3; // stored in the stack
int b = a;
System.out.println(a); // Output: 3
System.out.println(b); // Output: 3

a = 5;
System.out.println(a); // Output: 5
System.out.println(b); // Output: 3
```

However, when you use the assignment operator on an **object** variable, such as:

```Java
class NewObject {
    int x;
    NewObject(int x) {
        this.x = x;
    }
}
NewObject a = new NewObject(3) ; // a is in the stack, but the actual object is in the heap.
NewObject b = a;

System.out.println(a); // Output: Main$NewObject@7b23ec81
System.out.println(b); // Output: Main$NewObject@7b23ec81
```

Java treats the two types of variables differently. The object's attributes are stored in the heap, but the main function runs in the stack. Java creates a reference that points to the object in the heap, and when you want to access the data in that object, you need to dereference the object. So, when you use the assignment operator b = a, Java copies only the reference of that variable, and this is called shallow copying.

```Java
NewObject a = new NewObject(3) ; // a is in the stack, but the actual object is in the heap.
NewObject b = a;              // shallow copying
System.out.println(a.value); //return 3
System.out.println(b.value); //return 3
a.value = 5;                      // change the actual value of that address.
System.out.println(a.value); //return 5
System.out.println(b.value); //return 5 <- see? it is also equals to 5!

// How to deep copy?
NewObject c = new NewObject(a.value) // you can only new an instance to deep copy it.
a.value = 10;
System.out.println(a.value); // return 10
System.out.println(c.value); // return 5

```

Inside the memory, It will look something like this:
![](:java_basic/how_java_pass_variable/firstMemory.png){:data-align="center"}

In summary:\
For local variables:\
&emsp;primitive type: stack\
&emsp;object type: its referrence store in stack, the object itself stores in heap.

For memeber variables:\
&emsp;primitive type: heap\
&emsp;object type: its referrence store in heap as well!\

#### How Java pass variable in function?

Java's variable assignment and copying in memory work similarly to how it passes variables in functions. When you pass a primitive type to a function, Java allocates a new memory space and performs deep copying in the stack. On the other hand, when you pass an object type to a function, Java copies the reference and passes it to the function.

Here are some examples to help you grasp the concept:

Example 1:

```Java
public static void main(String[] args) {
    NewObject originalObj = new NewObject(5);
    changeValue1(originalObj);
    System.out.println(originalObj.value); // return 5;
}
private void changeValue1(NewObject obj) {
    NewObject newObj = new NewObject(10);
    obj = newObj;
}
```

![](:java_basic/how_java_pass_variable/secondMemory.png){:data-align="center"}

The final output is not 10 because Java passes the reference and assigns it to the function, not the original object. In this case, we are changing value to the copy of the original instance.

Example 2:

```Java
public static void main(String[] args) {
    NewObject originalObj = new NewObject(5);
    changeValue2(originalObj);
    System.out.println(originalObj.value); // return 10;
}
private void changeValue2(NewObject obj) {
    obj.value = 10;
}
```

![](:java_basic/how_java_pass_variable/thirdMemory.png){:data-align="center"}
In this example, we directly dereference the value of the object and assign a new value to the object in the heap. Therefore, all other variables that share the same address will reflect the change in value.

Example 3 and 4:

```Java
public static void main(String[] args) {
    NewObject originalObj = new NewObject(5);
    changeValue3(originalObj);              // Example 3
    System.out.println(originalObj.value); -> 5

    originalObj = changeValue3(originalObj); // Example 4
    System.out.println(originalObj.value); -> 10;
}
private NewObject changeValue3(NewObject obj) {
    NewObject newObj = new NewObject(10);
    return newObj;
}
```

![](:java_basic/how_java_pass_variable/fourthMemory.png){:data-align="center"}

In this changevalue function, we create a new instance and return the reference of that instance. In example 3, we did not catch the return value, so we did not have reference of it, the value stay the same. In example 4, we did assign the returned reference to our originalObj instance, so the value would be 10!

In summary, Java is always **"pass by value"**.
&emsp;For primitive type variable, it **deepcopy** the value.
&emsp;For object type variable, it **shallowcopy** the value.

Here is a question from previous Amazon OA. Hope you can get it right!.

```Java
public class Main {
    public static void main(String[] args) {
        B b = new B();
        b.f();
        b.a2.g(5);
    }
}
public class B {
    public void f() {
        int x1 = 7;
        A a1 = new A();
    }
    int x2 = 8;
    A a2 = new A();
}
class A {
    int x = 7;
    public void g(int num) {
        int x3 = num;
        System.out.println(x3);
    }
}
What variables are located in the stack?

What variables are located in thew heap?


```

<br>
<br>
<br>
<br>
<br>
<br>
What variables are located in the stack?\
b, x1, a1,x3

What variables are located in the heap??
x2, a2, x
