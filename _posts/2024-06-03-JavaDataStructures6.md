---
layout: single
title:  "Java Data Structure #6"
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned
**First**, I can use two `if` statements handling the edge cases.
**Second**, don't forget `length++` in prepend. Also, use `head = newNode`.
**Third**, in DLL get, cut in half and find the index.

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

# DLL: Get

## My Solution

DLL get is little bit different from SLL get. Due to SLL has only one pointer which is `.next`, it needs to move by one side. On the other hand, DLL has two pointers pointing both ways, `.next` and `.prev`, I can cut in half and search. 

```java
   public Node get(int index){
	    Node temp = head;
	    if(index < 0 || index >= length) return null;
	    if(index < length/2){
	        for(int i =0; i < index; i++){
	            temp = temp.next;
	        }
	    } else{
	        temp = tail;
	        for(int i = length-1; i>index;i--){
	            temp = temp.prev;
	        }
	    }
	    return temp;
	}
```

