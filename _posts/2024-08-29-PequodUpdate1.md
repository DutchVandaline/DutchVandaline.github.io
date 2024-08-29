![image](https://github.com/user-attachments/assets/c1367b13-7658-4d78-9ed1-5a773155f112)---
layout: single
title:  "Pequod Update 1"
---
<br>
![Pequod](https://github.com/user-attachments/assets/8bf45ee3-1001-459a-8db2-f32632e20dfc)

# What is PEQUOD
🐋 Pequod is Environmental habit tracker application made with Flutter. 🚀 Artificial Intelligence verifies your photo and check whether it matches to the habit or not. You have to take photo right there. 🦊 You can add up to 4 animals. These animals are suffering from plastic garbages.

🔗 https://apps.apple.com/kr/app/pequod/id6593668188?l=en-GB
💻 https://github.com/DutchVandaline/Pequod

## Disclaimer
 

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
