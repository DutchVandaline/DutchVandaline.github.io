---
layout: single
title:  "Java Data Structure 5"
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned
**First**, I lack the skill of making code simpler. <br>
**Second**, I also reviewed finding middle of the linked list. Using floyd's algorithm.

## Disclaimer
 For LeetCode, I started learning about data structures on Udemy. I've been studying with lecture named *Java Data Structures & Algorithms + LEETCODE Exercises*. 

# LL: Reverse Between

## Solution

 I came up with the idea but lacked the skill to make a code. I am thinking this problem difficult. But the solution was simple. Make a dummy Node and point to head. Move `previousNode` to the starting point, set `currentNode`
 move for `endIndex - startIndex` into the dummyNode. 

```java
    public void reverseBetween(int startIndex, int endIndex){
        if(head == null) return;
        Node dummyNode = new Node(0);
        dummyNode.next = head;
        Node previousNode = dummyNode;
        
        for(int i =0; i<startIndex; i++){
            previousNode = previousNode.next;
        }
        Node currentNode = previousNode.next;
        
        for(int i =0; i<endIndex-startIndex;i++){
            Node nodeToMove = currentNode.next;
            currentNode.next = nodeToMove.next;
            nodeToMove.next = previousNode.next;
            previousNode.next = nodeToMove;
        }
        head = dummyNode.next;
    }
```

