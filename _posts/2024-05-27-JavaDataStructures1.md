---
layout: single
title:  "Java Data Structure #1"
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned
**First**, *Floyd's Tortoise and Hare algorithm*. Astonishing Idea, Using two Pointers, one is *slow* and other is *fast*. To find middle, I use *slow* move by 1 and *fast* move by 2. When *fast* reaches, *slow* is pointing the middle.
**Second**, in *Floyd's Tortoise and Hare algorithm*, while loop condition is important. I need to use `while(fast != null && fast.next != null)`. 


## Disclaimer
 For LeetCode, I started learning about data structures on Udemy. I've been studying with lecture named *Java Data Structures & Algorithms + LEETCODE Exercises*. 

# LL: Find Middle Node

## My Solution
I've solved it. Used 2 different pointers to point middle. `temp` counts the full length of linkedlist and `mid` moves to the center of linkedlist. I guess this has O(n).

 ```java
	public Node findMiddleNode(){
	    Node mid = head;
	    Node temp = head;
	    int count = 0;
	    if(head == null) return null;
	    while(temp.next != null){
	        temp = temp.next;
	        count++;
	        System.out.println(count);
	    }
	    for(int i =0; i<(count+1)/2; i++){
	        mid = mid.next;
	    }
	    return mid;
	}
```
<br>
## Solution
But here's an astonishing Idea. Moving two pointers in different rate can easily point the middle of the linkedlist. Pointer `late` is moving rate of 1, `fast` is moving in rate of 2. If `fast` reaches the end, `late` is pointing the middle of array. What a graceful code.

```java
	public Node findMiddleNode(){
	    Node late = head;
      Node fast = head;

      while(fast.next != null && fast != null){
          late = late.next;
          fast = fast.next.next;
      }
      return late;
	}
```

# LL: Has Loop

## Solution
This was the idea about finding loop in a linkedlist. *Floyd's Tortoise and Hare algorithm* is astonishing. `Node slow` is moving by one and `Node fast` is moving by two. It will eventually meet when there is a loop. What I missed was `while` loop's condition. I wasn't able to come up with `(fast != null && fast.next != null)`. 

```java
public boolean hasLoop(){
	    Node slow = head;
	    Node fast = head;
	    
	    while(fast != null && fast.next != null){
	        slow = slow.next;
	        fast = fast.next.next;
	        if(slow == fast) return true;
	    }
	    return false;
	}
```
