![image](https://github.com/user-attachments/assets/c1367b13-7658-4d78-9ed1-5a773155f112)---
layout: single
title:  "Pequod Update 1"
---
<br>
![Pequod](https://github.com/user-attachments/assets/8bf45ee3-1001-459a-8db2-f32632e20dfc)

# What I've Learned
**First**, I can use `Stack<Character>` for stack questions.

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

# Stack: Parentheses Balanced
I know how to solve this. I can just check if there is value in stack and pop when it matches. But, this is a special case. It's little bit different.

```java
   public static boolean isBalancedParentheses(String paren){
        Stack<Character> stack = new Stack<>();
        for(char c : paren.toCharArray()){
            if(c=='(')
                stack.push(c);
            else if(c == ')')
                if(stack.isEmpty() || stack.pop() != '('){
                    return false;
                }
        }
        return stack.isEmpty();
    }
```
<br>
