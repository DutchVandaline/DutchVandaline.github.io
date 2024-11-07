---
layout: single
title:  "Sealant Problem with PyTorch #3"
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
## UnderSampling and OverSampling
 UnderSampling is sampling the images less than given images due to the imbalance of test and training image. For example, if there are 300 normal image but 1000 defect image, we 'undersample' the test image to 300. In this way, model can learn in balanced way. <br>
  OverSampling is the opposite. It's making 300 normal images into 1000 normal images. But, how? There are several ways to do this. You can use `SMOTE` in case of text datum. It generates new text data based on the other original data. But we are handling with images.

## Data Augmentation
 Data augmentation is the answer. You can augment the image by cropping, exaggerating, giving filters like gausian filter, bluring, edge detecting... sort of ways. I also thougt of generating new images using GAN, but the image was way too big to train and generate the augmented image. So, I am using data augmentation for Oversampling.


# Results, I guess?
## OverSampling using Data Augmentation
 Following is the code for augmenting images on jupyter notebook. I've used slight of image augmentation because, the image I need to classify has a detail. I need to check if it has printing error, or color errors. So, I wasn't able to use grey scaling and cropping at the middle of the image. <br>
 Also, I've extracted 20 `normal` and 20 `defect` images from start to test it at the final level.

 


<div style="display: flex; overflow-x: auto; gap: 10px;">
    <img src="https://github.com/user-attachments/assets/84d7327f-d401-49ec-b5ba-974450f6fe89" width="300" height="300">
    <img src="https://github.com/user-attachments/assets/a9fe5765-2191-4537-a165-658bbd76101f" width="300" height="300">
</div>

<br>
ROC curve is almost similar to what I've got from ViT. When zero, it needs to be zero and graph looks like going up. But, the ROC curve that I've got? It's perfectly 1. How? <br>
At first, I thought it's just perfectly checking. And that thought was wrong. (Actually, ROC Curve doesn't always need to start with (0,0). It's about FPR and TPR so if FPR is zero, then it can start at the top of the graph.) <br>
 I've thought that ViT, Vision Transformer is powerful when I got that similar curve and ratio. But, I cannot believe the result so, checked if it is really an overfitting. <br>
 When I got the similar results from EfficientNet, I thought it can be wrong. What can be the problem? <br>
 What I thought is the imbalance of the `Normal` and `Defect` Images. There are way too much `Defect` images rather than `Normal` Images. Model learns `Defect` data much better and there are less `Normal` data in Test Set too. Then, how can I solve this problem? <br> <br>

## UnderSampling and OverSampling
There are two ways to solve the imbalance of the datasets. One is undersampling which is matching the length of image data on less number. The other is oversampling which is matching the length of image data on biggest number. UnderSampling can use original data but, there can be loss on images. OverSampling however can maintain good learning but, need to augment the data. I am starting with UnderSampling and move to OverSampling.
 
## Progress
**1. Tried EfficientNet to check the Accuracy and it was great.** <br>
**2. There are ROC curves that doesn't start with `(0,0)`** <br>
<br>

## What's Next?
**1. Do the UnderSampling and check the ROC Curve.** <br>
**2. Data imbalance can be a problem.**

