---
layout: single
title:  "Java Data Structure #4"
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

# What I've Learned


# LL: Binary to Decimal Review

## Solution
 I solved by not seeing the hints or solutions. Multiplying 2 to calculate the binary value is a great idea. I need to keep this in mind.

```java
    public int binaryToDecimal(){
        int num = 0;
        Node temp = head;
        while(temp != null){
            num = num * 2 + temp.value;
            temp = temp.next;
        }
        return num;
    }
```
