---
layout: single
title:  "Java Data Structure #4"
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned
**First**, think simple. Algorithms are not that complicated to make. <br>

## Disclaimer
 For LeetCode, I started learning about data structures on Udemy. I've been studying with lecture named *Java Data Structures & Algorithms + LEETCODE Exercises*. 

# LL: Remove Duplicates

## Solution

 I almost got building `removeDuplicates(){}`, but I've missed the last part. It was simple enough to think but, else part and `temp = temp.next` was difficult.

```java
    public void removeDuplicates(){
        if(head == null) return;
        HashSet<Integer> hash = new HashSet<Integer>();
        Node before = null;
        Node temp = head;
        while(temp != null){
            if(hash.contains(temp.value)){
                before.next = temp.next;
                length--;
            } else{
                hash.add(temp.value);
                before = temp;
            }
            temp = temp.next;
        }
        
    }
```
