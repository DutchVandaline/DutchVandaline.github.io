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


# Results, I guess?
## Transfer Learning with ViT
I thought "Why just I give it a shot?" and just did it. Result was astonishing. 
<img src="https://github.com/user-attachments/assets/7b0f5022-3624-41e7-8ab9-2147e276ba1a" width="300" height="300">
<img src="https://github.com/user-attachments/assets/c18bf718-d245-442a-83a1-95441a494acf" width="300" height="300">
<br>
ROC curve is not like what I've learned. When zero, it needs to be zero and graph looks like going up. But, the ROC curve that I've got? It's perfectly 1. How? <br>
At first, I thought it's just perfectly checking. And that thought was wrong. (Actually, ROC Curve doesn't always need to start with (0,0). It's about FPR and TPR so if FPR is zero, then it can start at the top of the graph.) <br>
ViT, Vision Transformer must be way to powerful. I need to check if it is really an overfitting. Every other datum says it's not an overfitting but, I cannot really believe the ROC and Confusion Matrix before it is tested on the real environment. I just need to double check. <br> <br>

```python
from pytorch_modules.pytorch_modules.predictions import pred_and_plot_image
normal_image = "/content/drive/MyDrive/data/test/defect/20240823_105639.jpg"

pred_and_plot_image(model=ViT,
                           image_path=normal_image,
                           class_names=class_names)
```
<br>
I've checked some test data manually, but it wasn't not that correct. Classifing `Defect` was almost perfect, but in the case of `Normal`, not really. I just need to check if it really is Overfitting or just a luck. Next time, I will try EfficientNet. Also, **Data imbalance** can be the problem.<br>

## Progress
**1. Tried ViT (Vision Transformer) to check the Accuracy and it was great.** <br>
**2. There are ROC curves that doesn't start with `(0,0)`** <br>
<br>

## What's Next?
**1. Run EfficientNet to check if it is overfitting or not.**
**2. Data imbalance can be a problem.**

