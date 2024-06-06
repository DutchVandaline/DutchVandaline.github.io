---
layout: single
title:  "Java Data Structure #8"
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned
**First**, Think simple. Questions are not that hard than you think.

## Disclaimer
 For LeetCode, I started learning about data structures on Udemy. I've been studying with lecture named *Java Data Structures & Algorithms + LEETCODE Exercises*. 

# DLL: Reverse

## Solution
I've dragging this question for long time so, I just saw the result.

```java
   public void reverse() {
        Node current = head;
        Node temp = null;
    
        while (current != null) {
            temp = current.prev;
            current.prev = current.next;
            current.next = temp;
            current = current.prev;
        }
    
        temp = head;
        head = tail;
        tail = temp;
    }
```
<br>
