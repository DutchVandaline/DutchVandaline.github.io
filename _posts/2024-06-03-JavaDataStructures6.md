---
layout: single
title:  "Java Data Structure #6"
categories:
  - LeetCode
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned
**First**, I can use two `if` statements handling the edge cases.<br>
**Second**, don't forget `length++` in prepend. Also, use `head = newNode`.<br>
**Third**, in DLL get, cut in half and find the index. It's more efficient than SLL.<br>
**Fourth**, remove can be done by using `temp.next.prev = temp.prev` and `temp.prev.next = temp.next`. Not using two different pointers.<br>

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
<br>
# DLL: Get

## My Solution

DLL get is little bit different from SLL get. Due to SLL has only one pointer which is `.next`, it needs to move by one side. On the other hand, DLL has two pointers pointing both ways, `.next` and `.prev`, I can cut in half and search. Also, `set` method in DLL will be same as `set` method in SLL, but it will be more efficient.

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
<br>

# DLL: Insert

## My Solution

DLL Insert has the same formation of SLL Insert. I've missed the `if(... || index > length)`. I've written `if(...|| index >= length)`. 

```java
   public boolean insert(int index, int value){
	    Node newNode = new Node(value);
	    if(index < 0 || index > length) return false;
	    if(index == 0){
	        prepend(value);
	        return true;
	    }
	    if(index == length){
	        append(value);
	        return true;
	    } 
	    Node before = get(index -1);
	    Node after = before.next;
	    newNode.prev = before;
	    newNode.next = after;
	    before.next = newNode;
	    after.prev = newNode;
	    length++;
	    return true;
	    
	}
```

# DLL: Remove

## My Solution

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/a1d8810c-c8bf-469f-b0a1-a38f94184749)

Here is a astonishing idea. Without using `after` and `before` pointer, I can remove the Node using only one pointer. `temp.next.prev = temp.prev` and `temp.prev.next = temp.next`. This is a great idea. Of course it is not that readable.

```java
   public Node remove(int index){
	    Node temp = get(index);
	    if(index < 0 || index >= length) return null;
	    if(index == 0) return removeFirst();
	    if(index == length -1) return removeLast();
	    
	    temp.next.prev = temp.prev;
	    temp.prev.next = temp.next;
	    temp.next = null;
	    temp.prev = null;
	    length--;
	    return temp;
	}
```

