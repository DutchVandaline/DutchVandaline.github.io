---
layout: single
title:  "Java Data Structure #3"
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned
**First**, think simple. Algorithms are not that complicated to make. <br>

## Disclaimer
 For LeetCode, I started learning about data structures on Udemy. I've been studying with lecture named *Java Data Structures & Algorithms + LEETCODE Exercises*. 

# LL: Partition List

## Solution
I thought of using two different pointers, but I wasn't able to come up with the idea of using two dummy nodes. Initializing dummy node by `Node dummy1 = new Node(0)`. It's not that complicated algorithm. Making two different ArrayList and linking each other.
The confusing part was, I think, *2. The solution should not create a new linked list.* So, I thought I cannot make `Node dummy1 = new Node(0);`. 

```java
    public void partitionList(int x){
        if(head == null) return;
        Node dummy1 = new Node(0);
        Node dummy2 = new Node(0);
        Node prev1 = dummy1;
        Node prev2 = dummy2;
        Node current = head;
        while(current != null){
            if(current.value < x) {
                prev1.next = current;
                prev1 = current;
            } else{
                prev2.next = current;
                prev2 = current;
            }
            current = current.next;
        }
        
        prev2.next = null;
        prev1.next = dummy2.next;
        
        head = dummy1.next;
    }
```
