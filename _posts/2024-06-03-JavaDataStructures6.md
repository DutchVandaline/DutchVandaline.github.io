---
layout: single
title:  "Java Data Structure #6"
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned
**First**, I can use two `if` statements handling the edge cases.

## Disclaimer
 For LeetCode, I started learning about data structures on Udemy. I've been studying with lecture named *Java Data Structures & Algorithms + LEETCODE Exercises*. 

# DLL: Remove Last

## Solution

 Singly Linked List is done so, I am dealing with doubly Linked List. This is not that difficult because of SLL I think. There are few more codes because of `prev` but it's okay. For `removeLast`, there is a change. 
 Original code had `length--;` and then `if(length==0)` again, but it makes the code hard to read. So, there are two `if` statements.

```java
   public Node removeLast(){
	    Node temp = tail;
	    if(length == 0) return null;
	    if(length == 1){
	        head = null;
	        tail = null;
	    } else{
	        tail = tail.prev;
	        tail.next = null;
	        temp.prev = null;
	    }
	    length--;
	    return temp;
	}
```

# LL: Binary to Decimal

## My Solution

I've solved this problem. Using `while` loop. The idea of multipling 2 before moving to the next pointer was a good idea. I need to remember that algorithm for other time

```java
   public int binaryToDecimal(){
        int num = 0;
        Node temp = head;
        
        while(temp != null){
            num += temp.value;
            if(temp.next == null)
                break;
            num *= 2;
            temp = temp.next;
        }
        return num;
    }
```

## Solution

There was a simpler answer. Without using `break`, I can just multiply 2 and add the value in one line.

```java
     public int binaryToDecimal() {
        int num = 0;
        Node current = head;
        while (current != null) {
            num = num * 2 + current.value;
            current = current.next;
        }
        return num;
    }
```
