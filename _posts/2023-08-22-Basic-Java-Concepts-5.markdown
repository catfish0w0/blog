---
# multilingual page pair id, this must pair with translations of this page. (This name must be unique)
lng_pair: basc_java_5
title: A Review of String and StringBuilder in Java

# post specific
# if not specified, .name will be used from _data/owner/[language].yml
author: Puff
# multiple category is not supported
category: Java Basic
# multiple tag entries are possible
tags: [Java]
# thumbnail image for post
img: ":java_basic/string/StringMeme2.png"
# disable comments on this page
#comments_disable: true

# publish date
date: 2023-08-22 17:14:06 +0900
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

#### What is String??

String is a **special Object** class that is implemented by Java. Unlike other data structures like arrayList, HashMap…etc, you do not need to import String from java.utils, because String is specifically implemented inside the java.lang package. If you look at the source code, you will see that in Java 11, inside the String class, there is a public final byte[] as a field.

```java
public final class String implements java.io.Serializable, Comparable<String>, CharSequence
private final byte[] value[];
```

This leads to some unique properties that String has.

1. String is immutable, immutable means you **cannot change characters internally**, for example: “abc” + “d” -> will lead to open a new memory space for a new String
2. Can lead to index out of bound exception, if you access index over its length
3. Can lead to null pointer exception, if you access a method in a null object.

#### How to create a String Object in Java

1. **Directly define method:**
   `String a = "abc"`
2. **new String keyword:**
   `String a = new String("aaa")`
3. **intern() method:**
   `String s2 = a.intern()`

#### What API do we need to know about String?

The following table is a quick guide that include all APIs you should know about when you use Java for coding interviews. You can find the details of String APIs [here](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html).

| String API                                    |                                                                              Comment or things need to be aware of                                                                              |
| --------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| char charAt(int index)                        |                                                                                                                                                                                                 |
| int compareTo(String s2)                      | This API compare String based on their lexicographically order, \Capital character is greater than non-capital character. \ ABC.compareTo(abc) would return -1, meaning ABC is smaller than abc |
| int compareToIgnoreCase(String s2)            |                                                                              same API as above just without cases                                                                               |
| String concat(String s2)                      |                                                                                    same as adding String "+"                                                                                    |
| boolean equals(String s2)                     |                                                                                                                                                                                                 |
| boolean equalsIgnoreCase(String s2)           |                                                                                                                                                                                                 |
| replace(char oldChar, char newChar)           |                                                                                        non-static method                                                                                        |
| replace(CharSequence oldS, CharSequence newS) |                                                                                        non-static method                                                                                        |
| int indexOf(char c)                           |                                                                                                                                                                                                 |
| int indexOf(String s1)                        |                                                                                                                                                                                                 |
| int length()                                  |                                                                                                                                                                                                 |
| String substring(int beginIndex)              |                                                                                                                                                                                                 |
| String substring(int beginIndex, int length)  |                                                                                                                                                                                                 |
| char[] toCharArray()                          |                                                                                                                                                                                                 |
| String toLowerCase()                          |                                                                                                                                                                                                 |
| String toUpperCase()                          |                                                                                                                                                                                                 |
| String trim()                                 |                                                                                                                                                                                                 |
| String repeat(int repeatTime)                 |                                                                         it concat the same String for repeatTime times                                                                          |

#### What is StringBuilder()?

StringBuilder is a class that Java implemented to allow user to "dynamically modify" the String. Again, StringBuilder is in Java.lang package, so you can use it without importing it.

#### How to create StringBuilder in Java?

Just like creating an Object: `StringBuilder sb = new StringBuilder()`

#### What API do we need to know about StringBuilder?

| StringBuilder API                                    |                                Comment or things need to be aware of                                 |
| ---------------------------------------------------- | :--------------------------------------------------------------------------------------------------: |
| append(char ch)                                      |                                                                                                      |
| append(char[] charArray)                             |                                                                                                      |
| append(char[] charArray, int startIndex, int length) |                                                                                                      |
| append(CharSequence s)                               |                           if append null, it will append “null” inside sb                            |
| append(CharSequence s, int start, int length)        |                                                                                                      |
| append(String s)                                     |                                                                                                      |
| int capacity()                                       |                        Yes just like an ArrayList, StringBuilder has capacity                        |
| char charAt(int index)                               |                             if it exceeds length, it can throw exception                             |
| delete(int startIndex, int length)                   |                                                                                                      |
| deleteCharAt(int index)                              |                                                                                                      |
| int indexOf(String str)                              |                                                                                                      |
| int indexOf(String str, int fromIndex)               |                                                                                                      |
| insert(int index, String s)                          |            it put the String into the StringBuilder, and push the rest of the String back            |
| int lastIndexOf(String)                              |                   lastIndexOf return the first index of the rightmost occurrence.                    |
| replace(int startIndex, int length, String str)      |                                                                                                      |
| reverse()                                            |                                                                                                      |
| setCharAt(int index, char ch)                        |                                                                                                      |
| setLength(int newLength)                             | Be aware of the exact length, if set too much length, it will appear a lot of empty useless charcode |
| subString(int startIndex)                            |                                                                                                      |
| substring(int startIndex, int length)                |                                                                                                      |
| toString()                                           |                                                                                                      |

#### More Practice Questions

| Problem Number | Problem | Solution |
| :------------: | :-----: | :------: |
|       1        |         |          |
|       2        |         |          |
|       3        |         |          |
|       4        |         |          |
|       3        |         |          |
