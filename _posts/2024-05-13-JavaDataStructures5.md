---
layout: single
title:  "Java Data Structure 5"
categories:
  - LeetCode
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned
**First**, I lack the skill of making code simpler. <br>
**Second**, I also reviewed finding middle of the linked list. Using floyd's algorithm.
**Third**, Find the key when moving.

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

# LL: Partition List Review

## Solution

 I've reviewed the *Partition List*. I was wrong of using `Node prev1` and `Node prev2`. I just moved with `dummy1` and `dummy2` directly. Also, `temp` need to move because of `if` statement. The criteria of moving needs to be `temp`. 

```java
     public void partitionList(int x){
        Node dummy1 = new Node(0);
        Node dummy2 = new Node(0);
        Node prev1 = dummy1;
        Node prev2 = dummy2;
        Node temp = head;
        
        while(temp != null){
            if(temp.value < x){
                prev1.next = temp;
                prev1 = temp;
            }
            else{
                prev2.next = temp;
                prev2 = temp;
            }
            temp = temp.next;
        }
        prev2.next = null;
        prev1.next = dummy2.next;
        head = dummy1.next;
    }
```
