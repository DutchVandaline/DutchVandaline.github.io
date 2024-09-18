---
layout: single
title:  "Java Data Structure #7"
categories:
  - LeetCode
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned
**First**, Think simple. Questions are not that hard than you think.

## Disclaimer
 For LeetCode, I started learning about data structures on Udemy. I've been studying with lecture named *Java Data Structures & Algorithms + LEETCODE Exercises*. 

# DLL: Swap First and Las

## Solution

 Actually, this question is not a hard one. It's simple as it seems. But, I thought too deep. I thought I need to change the Nodes literally. So, I've used `Node temp` to store the head Nodes, swap using `head.next.prev`... I need to think simpler.

```java
   public void swapFirstLast(){
	    if(length < 2) return;
	    int temp = head.value;
	    head.value = tail.value;
	    tail.value = temp;
	    
	}
```
<br>
