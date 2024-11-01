---
layout: single
title:  "Sealant Problem with PyTorch #1"
categories:
  - AI
---

<br>
![image](https://github.com/user-attachments/assets/ff9c27b0-936b-4913-ad9d-910e3427699b)


# To Start With
 I am a student learning Artificial Intelligence. In class, as a part of LINK program which is connecting companies and universities for solving problem, one company asked for solving computer vision problem.
There are printing errors on sealant. Accuracy needs to be high and speed needs to be fast. Also, there are limitations that we can just use on Google Colab. They gave us as a YOLO format but, it's actually just binary classification.
<br>
 **Consraints**
- Can use only Google Colab Resources.
- Model needs to be fast, accurate at the same time.
- Model needs to be light weight.

# Finding Recommendations
## Transfer Learning
I thought I can just use transfer learning to train the model and test it by just using it. I've learned Transfer Learning via Udemy, so I knew how to do it. The first model I've tried is ViT, the Vision Transformer. Actually it's the most powerful model now in Computer Vision territory.
Also, I've considered EfficientNet, CNN, VGG and so on...


# Results
## Transfer Learning with ViT
I thought "Why just I give it a shot?" and just did it. Result was astonishing. 
![download](https://github.com/user-attachments/assets/7b0f5022-3624-41e7-8ab9-2147e276ba1a)
<br>
![download](https://github.com/user-attachments/assets/c18bf718-d245-442a-83a1-95441a494acf)
<br>
ROC curve is not like what I've learned. When zero, it needs to be zero and graph looks like going up. But, the ROC curve that I've got? It's perfectly 1. How?
At first, I thought it's just perfectly checking. And that thought was wrong. 


<br>

## Progress
**1. Found out that YOLO has it's own Loss Function.** <br>
**2. Modified the Loss Function and made it live between 0 and 1. But not sure whether it's working or not.** <br>
<br>

