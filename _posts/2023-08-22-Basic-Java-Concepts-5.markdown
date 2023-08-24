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

#### String Processing Interviewing Questions

As the old saying: when you see a question that is String Processing type of question, you will know it is a String Processing type of question. One good thing about String Processing type of question is that it is very easy to identify. Usually this type of algorithmic question is not hard in Logic, but ,most of the time, the question itself is very annoying to cover all cases, and the code can get very long and reluctant as well. If the question itself is asking to implement the above mentioned String APIs, you probably will not able to implement it using StringBuilder(the interviewer will ask you to do it in-place). Here is the summary of this type of question.

1. ask for clairification first, which character can be in the input String, which characters dont, this is very important, can save you a lot of times from nasty edge cases.
2. if the problem itself involve integers, ask for signs character.
3. Discuss different synario case by case, list them out visually.
4. most of the time, it will utilize two-pointer techniques. left side of slow pointer is what i want to keep for the result, while fast pointer is used to traverse the rest of the String.

#### Practice Question by topics

String Removal:

| Problem Number |                                                          Problem                                                          | Solution |
| :------------: | :-----------------------------------------------------------------------------------------------------------------------: | :------: |
|       1        |                                           remove certain character from String                                            |          |
|       2        |                                                       Remove Spaces                                                       |          |
|       3        |    [Remove All Adjacent Duplicates In String](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)    |          |
|       4        | [Remove All Adjacent Duplicates in String II](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/) |          |
|       5        |                             [Remove Comments](https://leetcode.com/problems/remove-comments/)                             |          |
|       6        |       [Remove All Occurrences of a Substring](https://leetcode.com/problems/remove-all-occurrences-of-a-substring/)       |          |
|       7        |                [Removing Stars From a String](https://leetcode.com/problems/removing-stars-from-a-string)                 |          |

String Reversal:

| Problem Number |                                         Problem                                         | Solution |
| :------------: | :-------------------------------------------------------------------------------------: | :------: |
|       1        |             [Reverse String](https://leetcode.com/problems/reverse-string/)             |          |
|       2        |          [Reverse String II](https://leetcode.com/problems/reverse-string-ii/)          |          |
|       3        | [Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/) |          |
|       4        |  [Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/)  |          |

String Palindrome Series:

| Problem Number |                                  Problem                                  | Solution |
| :------------: | :-----------------------------------------------------------------------: | :------: |
|       1        |    [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)    |          |
|       2        | [Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/) |          |
|       3        |   [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)   |          |

String to Integer, Integer to String Series:

| Problem Number |                                                 Problem                                                 | Solution |
| :------------: | :-----------------------------------------------------------------------------------------------------: | :------: |
|       1        |                   [Integer to Roman](https://leetcode.com/problems/integer-to-roman/)                   |          |
|       2        |                   [Roman to Integer](https://leetcode.com/problems/roman-to-integer/)                   |          |
|       3        |           [Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/)           |          |
|       4        |          [Excel Sheet Column Number](https://leetcode.com/problems/excel-sheet-column-number/)          |          |
|       5        | [Cells in a Range on an Excel Sheet](https://leetcode.com/problems/cells-in-a-range-on-an-excel-sheet/) |          |
|       6        |            [String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)            |          |

String to Math Operation:

| Problem Number |                              Problem                               | Solution |
| :------------: | :----------------------------------------------------------------: | :------: |
|       1        |      [Add Binary](https://leetcode.com/problems/add-binary/)       |          |
|       2        |      [Add String](https://leetcode.com/problems/add-strings/)      |          |
|       3        |                   Add String with negative input                   |          |
|       4        | [Multiply String](https://leetcode.com/problems/multiply-strings/) |          |

String Replace, Modify String Series:

| Problem Number |                                                                       Problem                                                                       | Solution |
| :------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------: | :------: |
|       1        | [Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/) |          |
|       2        |                           [Rearrange Spaces Between Words](https://leetcode.com/problems/rearrange-spaces-between-words/)                           |          |
|       3        |                                                                   String Replace                                                                    |          |
|       4        |                                                                   Compress String                                                                   |          |
|       5        |                                                                 Decompress String I                                                                 |          |
|       6        |                                                                Decompress String II                                                                 |          |
|       7        |                                       [Text Justification](https://leetcode.com/problems/text-justification/)                                       |

Split String

| Problem Number |                                                     Problem                                                     | Solution |
| :------------: | :-------------------------------------------------------------------------------------------------------------: | :------: |
|       1        |             [Split Strings by Separator](https://leetcode.com/problems/split-strings-by-separator/)             |          |
|       2        | [Maximum Score After Splitting a String](https://leetcode.com/problems/maximum-score-after-splitting-a-string/) |          |
|       3        |    [ Split a String in Balanced Strings](https://leetcode.com/problems/split-a-string-in-balanced-strings/)     |          |
|       4        |  [Number of Good Ways to Split a String](https://leetcode.com/problems/number-of-good-ways-to-split-a-string/)  |          |
|       5        |      [ Number of Ways to Split a String](https://leetcode.com/problems/number-of-ways-to-split-a-string/)       |          |
