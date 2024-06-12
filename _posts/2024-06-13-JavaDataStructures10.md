---
layout: single
title:  "Java Data Structure #10"
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned
**First**, determine whether it's just `Node` or `Node.value`.

## Disclaimer
 For LeetCode, I started learning about data structures on Udemy. I've been studying with lecture named *Java Data Structures & Algorithms + LEETCODE Exercises*. 

# Stack: Push for a Stack That Uses an ArrayList

```java
   public void push(T value){
        stackList.add(value);
    }
```
<br>

# Stack: Pop for a Stack That Uses an ArrayList

```java
   public T pop(){
        if(isEmpty()) return null;
        return stackList.remove(stackList.size()-1);
    }
```
<br>
