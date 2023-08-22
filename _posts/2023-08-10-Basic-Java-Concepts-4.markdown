---
# multilingual page pair id, this must pair with translations of this page. (This name must be unique)
lng_pair: basc_java_3
title: A Review of Linked List and Implementation in Java

# post specific
# if not specified, .name will be used from _data/owner/[language].yml
author: Puff
# multiple category is not supported
category: Java Basic
# multiple tag entries are possible
tags: [Java]
# thumbnail image for post
img: ":java_basic/linked-list/linkedlist.jpg"
# disable comments on this page
#comments_disable: true

# publish date
date: 2023-08-10 17:14:06 +0900
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

#### What is Linked List??

A linked list is another linear data structure that stores data in a ListNode, and the ListNode has another address that points to its next ListNode.

#### How to represent a LinkedList?

using the head of the Linked List `ListNode head` \
that means all Linked List Interview Problem is actually traversal problem. Because If we have the head, we can basically extract all the data afterward.

#### How to traverse a LinkedList?

we dont wnat to lose the address of the head, because we wont be able to visit it afterward.
so, we create a variable that allow us traverse the linked list.

```java
ListNode cur = head;
while (cur != null) {
    cur = cur.next;
}
```

#### What problems do we need to be extra cautious?

1. Null-pointer exception, since linked list is using pointer to traverse the list.
2. Losing the value of head.
   head = head.next -> will lead to lose the head pointer!

#### Singly Linked List Implementation

API to Implement:\

1. get(int index)/searchByValue
2. addHead/addTail/addIndex
3. deleteHead/deleteTail/deleteByIndex

```Java
public SinglyLinkedList class {
    // how to print a node?
    // if you put System.out.println(new ListNode(1)) -> it will pops up error.
    // just like you want to ompare ListNode(1) && ListNode(2)
    // since they all extend the class Object in Java
    // you have to override the toString method / compare method in order to directly
    // print it out or compare it.

    static class ListNode {
        int value;
        ListNode next;
        public ListNode(int value) {
            this.value = value;
        }
        @Override
            public String toString() {
            return value + “ -> “;
        }
    }

    // field
    ListNode head;
    int size;
    public SinglyLinkedList() {
        head = null;
        size = 0;
    }

    // get the value of the index node, index range from 0 to n - 1
    public Integer get(int index) {
        if (index < 0 || index >= size) {
            throw exception;
        }
        ListNode cur = head;
        for (int i = 0; i < index; i++) {
            cur = cur.next;
        }
        return cur.value;
    }

    // return the firstNode that has target value
    public ListNode searchByValue(int value) {
        ListNode cur = head;
        while (cur != null) {
            if (cur.value == value) {
                return cur;
            }
            cur = cur.next;
        }
        return cur; // null
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public int getSize() {
        return size;
    }

    public void printLinkedList() {
        ListNode cur = head;
        while (cur != null) {
            System.out.println(cur); //We implement toString.
            cur = cur.next
        }
    }

    public void addHead(int value) {
        ListNode newHead = new ListNode(value);
        newHead.next = head;
        head = newHead;
        size++;
    }

    public void addTail(int value) {
        if (head == null) {
            addHead(value);
        }
        ListNode cur = head;
        while (cur.next != null) {
            cur = cur.next;
        }
        cur.next = new ListNode(value);
        size++;
    }

    public void addIndex(int index, int value) {
        if (index < 0 || index >= size) {
            return;
        }
        if (index == 0) {
            addHead(value);
        } else if (index == size) {
            addTail(value);
        } else {
            ListNode cur = head;
            for (int i = 0; i < index; i++) {
                cur = cur.next;
            }
            ListNode next = cur.next;
            cur.next = new ListNode(value);
            cur = cur.next;
            cur.next = next;
            size++;
        }
    }

    public void deleteHead() {
        if (head == null) {
            return;
        }
        head = head.next;
        size–;
    }

    public void deleteTail() {
        if (head == null) {
            return;
        }
        if (head.next == null) {
            deleteHead();
            return;
        }
        ListNode cur = head;
        while (cur.next.next != null) {
            cur = cur.next;
        }
        cur.next = null;
        size--;
    }

    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) {
            return;
        }
        if (index == 0) {
            deleteHead();
            return;
        } else if (index == size - 1) {
            deleteTail();
            return;
        } else {
            ListNode prev = head;
            for (int i = 0; i < index - 1; i++) {
                prev = prev.next;
            }
            prev.next = prev.next.next;
            size--;
        }
    }

}
```

#### Doubly Linked List Implementation

The only difference between Doubly Linked List and Singly Linked List is <span style="color:red">**adding and deleting**</span>.

```java
public DoublyLinkedList class {

	static class ListNode {
        int value;
        ListNode next;
        ListNode prev;
        public ListNode(int value) {
            this.value = value;
        }
        @Override
        public String toString() {
            return “<-” + value + “ -> “;
        }
    }

    // field
    ListNode head;
    int size;
    public DoublyLinkedList() {
        head = null;
        size = 0;
    }
    //基本上改跟查 的Code是完全不需要變化
    // get the value of the index node, index range from 0 to n - 1
    public Integer get(int index) {
        if (index < 0 || index >= size) {
            throw exception;
        }
        ListNode cur = head;
        for (int i = 0; i < index; i++) {
            cur = cur.next;
        }
        return cur.value;
    }

    // return the firstNode that has target value
    public ListNode searchByValue(int value) {
        ListNode cur = head;
        while (cur != null) {
        if (cur.value == value) {
            return cur;
        }
        cur = cur.next;
        }
        return cur; // null
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public int getSize() {
        return size;
    }

    public void addHead(int value) {
        ListNode newHead = new ListNode(value);
        //多左一句
        if (head != null) {
            head.prev = newHead;
        }
        newHead.next = head;
        head = newHead;
        size++;
    }

    //増 跟刪除都只係改動左連pointer的方法.
    public void addTail(int value) {
        if (head == null) {
            addHead(value);
        }
        ListNode cur = head;
        while (cur.next != null) {
            cur = cur.next;
        }
        ListNode newHead = new ListNode(value);
        cur.next = newHead;
        newHead.prev = cur;
        size++;
    }

    public void addIndex(int index, int value) {
        if (index < 0 || index >= size) {
            return;
        }
        if (index == 0) {
            addHead(value);
        } else if (index == size) {
            addTail(value);
        } else {
            ListNode cur = head;
            for (int i = 0; i < index; i++) {
                cur = cur.next;
            }
            ListNode next = cur.next;
            ListNode newNode = new ListNode(value);
            cur.next = newNode;
            newNode.prev = cur;

            newNode.next = next;
            next.prev = newNode;
            size++;
        }
    }

    public void deleteHead() {
        if (head == null) {
            return;
        }
        head = head.next;
        head.prev = null;
        size–;
    }

    public void deleteTail() {
        if (head == null) {
            return;
        }
        if (head.next == null) {
            deleteHead();
            return;
        }
        ListNode cur = head;
        while (cur.next.next != null) {
            cur = cur.next;
        }
        cur.next.prev = null;
        cur.next = null;
        size--;
    }

    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) {
            return;
        }
        if (index == 0) {
            deleteHead();
            return;
        } else if (index == size - 1) {
            deleteTail();
            return;
        } else {
            ListNode prev = head;
            for (int i = 0; i < index - 1; i++) {
                prev = prev.next;
            }
            ListNode delete = prev.next;
            ListNode next = delete.next;

            delete.prev = null;
            delete.next = null;

            prev.next = next;
            next.prev = prev;

            size--;
        }
    }
}
```

#### Circular Linked List Implementation

The only difference between SinglyLinkedList and CircularLinkedList is the <span style="color:red">**terminate condition in the while loop, and always look for the tail in adding and deleting head/tail**</span>.

```java
public CircularLinkedList class {
    static class ListNode {
        int value;
        ListNode next;
        public ListNode(int value) {
            this.value = value;
        }
        @Override
        public String toString() {
            return value + “ -> “;
        }
    }

    ListNode head;
    int size;
    public CircularLinkedList () {
        head = null;
        size = 0;
    }

    // get the value of the index node, index range from 0 to n - 1
    public Integer get(int index) {
        if (index < 0 || index >= size) {
            throw exception;
        }
        ListNode cur = head;
        for (int i = 0; i < index; i++) {
            cur = cur.next;
        }
        return cur.value;
    }

    // return the firstNode that has target value
    public ListNode searchByValue(int value) {
        ListNode cur = head;
        while (cur != head) {
            if (cur.value == value) {
                return cur;
            }
            cur = cur.next;
        }
        return null; // null
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public int getSize() {
        return size;
    }

    public void addHead(int value) {
        ListNode newHead = new ListNode(value);
        newHead.next = head;
        ListNode cur = head;
        while (cur.next != head) {
            cur = cur.next;
        }
        cur.next = newHead;
        head = newHead;
        size++;
    }

    public void addTail(int value) {
        if (head == null) {
            addHead(value);
        }
        ListNode cur = head;
        while (cur.next != head) {
            cur = cur.next;
        }
        cur.next = new ListNode(value);
        cur = cur.next;
        cur.next = head;
        size++;
    }

    public void addIndex(int index, int value) {
        if (index < 0 || index >= size) {
            return;
        }
        if (index == 0) {
            addHead(value);
        } else if (index == size) {
            addTail(value);
        } else {
            ListNode cur = head;
            for (int i = 0; i < index; i++) {
                cur = cur.next;
            }
            ListNode next = cur.next;
            cur.next = new ListNode(value);
            cur = cur.next;
            cur.next = next;
            size++;
        }
    }

    public void deleteHead() {
        if (head == null) {
            return;
        }
        ListNode cur = head;
        // find the last pointer;
        while (cur.next != head) {
            cur = cur.next;
        }
        head = head.next;
        cur.next = head;
        size–;
    }

    public void deleteTail() {
        if (head == null) {
            return;
        }
        if (head.next == null) {
            deleteHead();
            return;
        }
        ListNode cur = head;
        while (cur.next.next != head) {
            cur = cur.next;
        }
        cur.next = head;
        size--;
    }

    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) {
            return;
        }
        if (index == 0) {
            deleteHead();
        return;
        } else if (index == size - 1) {
            deleteTail();
        return;
        } else {
            ListNode prev = head;
            for (int i = 0; i < index - 1; i++) {
                prev = prev.next;
            }
            prev.next = prev.next.next;
            size--;
        }
    }
}
```

#### More Practice Questions

| Problem Number | Problem | Solution |
| :------------: | :-----: | :------: |
|       1        |         |          |
|       2        |         |          |
|       3        |         |          |
|       4        |         |          |
|       3        |         |          |
