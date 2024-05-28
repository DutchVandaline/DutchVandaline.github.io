---
layout: single
title:  "Java Data Structure #2"
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned
**First**, *Floyd's Tortoise and Hare algorithm*. Astonishing Idea, Using two Pointers, one is *slow* and other is *fast*. To find middle, I use *slow* move by 1 and *fast* move by 2. When *fast* reaches, *slow* is pointing the middle.
**Second**, in *Floyd's Tortoise and Hare algorithm*, while loop condition is important. I need to use `while(fast != null && fast.next != null)`. 


## Disclaimer
 For LeetCode, I started learning about data structures on Udemy. I've been studying with lecture named *Java Data Structures & Algorithms + LEETCODE Exercises*. 

# LL: Find Kth Node From End

## Solution
I was able to come up with the idea using *Floyd's Tortoise and Hare algorithm*. 

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
