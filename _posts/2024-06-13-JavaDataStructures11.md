---
layout: single
title:  "Java Data Structure #11"
---
<br>

![image](https://github.com/DutchVandaline/DutchVandaline.github.io/assets/142364450/b75c9826-3f3f-44ba-9d85-dc8eb7d3aba1)

## Disclaimer
 For LeetCode, I started learning about data structures on Udemy. I've been studying with lecture named *Java Data Structures & Algorithms + LEETCODE Exercises*. 

# Stack: Reverse String
I can use `Stack<Character>` for the Stack questions. I didn't know about Stack.

```java
   public static String reverseString(String myString){
        Stack<Character> stack = new Stack<>();
        String reversedString = "";
        
        for(char c: myString.toCharArray()){
            stack.push(c);
        }
        
        while(!stack.isEmpty()){
            reversedString += stack.pop();
        }
        return reversedString;
    }
```
<br>
