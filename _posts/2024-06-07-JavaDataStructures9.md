---
layout: single
title:  "Java Data Structure #9"
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned
**First**, determine whether it's just `Node` or `Node.value`.

## Disclaimer
 For LeetCode, I started learning about data structures on Udemy. I've been studying with lecture named *Java Data Structures & Algorithms + LEETCODE Exercises*. 

# DLL: Palindrome Checker

## My Solution
I've got the solution how to solve it but, there was a simple problem. In `if(p1.value != p2.value) return false;`, I didn't added the `.value`. It's a simple mistake but the code didn't work.

```java
   public boolean isPalindrome(){
	    Node p1 = head;
	    Node p2 = tail;
	    for(int i = 0; i<length/2; i++){
	        if(p1.value != p2.value) return false;
	        p1 = p1.next;
	        p2 = p2.prev;
	    }
	    return true;
	}
```
<br>
