---
layout: single
title:  "Sealant Problem with PyTorch #2"
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
## EfficientNet
EfficientNet is a Artificial Intelligence model and it has a long history. Layers are deep and wide so that it can learn things well. It's capable for classification. Following is the layer of EfficientNet that can be seen on PyTorch. I've used Transfer Learning as I did at ViT.

```python
========================================================================================================================
Layer (type (var_name))                                      Input Shape     Output Shape    Param #         Trainable
========================================================================================================================
EfficientNet (EfficientNet)                                  [1, 3, 2532, 824] [1, 2]          --              Partial
├─Sequential (features)                                      [1, 3, 2532, 824] [1, 1280, 80, 26] --              False
│    └─Conv2dNormActivation (0)                              [1, 3, 2532, 824] [1, 32, 1266, 412] --              False
│    │    └─Conv2d (0)                                       [1, 3, 2532, 824] [1, 32, 1266, 412] (864)           False
│    │    └─BatchNorm2d (1)                                  [1, 32, 1266, 412] [1, 32, 1266, 412] (64)            False
│    │    └─SiLU (2)                                         [1, 32, 1266, 412] [1, 32, 1266, 412] --              --
│    └─Sequential (1)                                        [1, 32, 1266, 412] [1, 16, 1266, 412] --              False
│    │    └─MBConv (0)                                       [1, 32, 1266, 412] [1, 16, 1266, 412] (1,448)         False
│    └─Sequential (2)                                        [1, 16, 1266, 412] [1, 24, 633, 206] --              False
│    │    └─MBConv (0)                                       [1, 16, 1266, 412] [1, 24, 633, 206] (6,004)         False
│    │    └─MBConv (1)                                       [1, 24, 633, 206] [1, 24, 633, 206] (10,710)        False
│    └─Sequential (3)                                        [1, 24, 633, 206] [1, 40, 317, 103] --              False
│    │    └─MBConv (0)                                       [1, 24, 633, 206] [1, 40, 317, 103] (15,350)        False
│    │    └─MBConv (1)                                       [1, 40, 317, 103] [1, 40, 317, 103] (31,290)        False
│    └─Sequential (4)                                        [1, 40, 317, 103] [1, 80, 159, 52] --              False
│    │    └─MBConv (0)                                       [1, 40, 317, 103] [1, 80, 159, 52] (37,130)        False
│    │    └─MBConv (1)                                       [1, 80, 159, 52] [1, 80, 159, 52] (102,900)       False
│    │    └─MBConv (2)                                       [1, 80, 159, 52] [1, 80, 159, 52] (102,900)       False
│    └─Sequential (5)                                        [1, 80, 159, 52] [1, 112, 159, 52] --              False
│    │    └─MBConv (0)                                       [1, 80, 159, 52] [1, 112, 159, 52] (126,004)       False
│    │    └─MBConv (1)                                       [1, 112, 159, 52] [1, 112, 159, 52] (208,572)       False
│    │    └─MBConv (2)                                       [1, 112, 159, 52] [1, 112, 159, 52] (208,572)       False
│    └─Sequential (6)                                        [1, 112, 159, 52] [1, 192, 80, 26] --              False
│    │    └─MBConv (0)                                       [1, 112, 159, 52] [1, 192, 80, 26] (262,492)       False
│    │    └─MBConv (1)                                       [1, 192, 80, 26] [1, 192, 80, 26] (587,952)       False
│    │    └─MBConv (2)                                       [1, 192, 80, 26] [1, 192, 80, 26] (587,952)       False
│    │    └─MBConv (3)                                       [1, 192, 80, 26] [1, 192, 80, 26] (587,952)       False
│    └─Sequential (7)                                        [1, 192, 80, 26] [1, 320, 80, 26] --              False
│    │    └─MBConv (0)                                       [1, 192, 80, 26] [1, 320, 80, 26] (717,232)       False
│    └─Conv2dNormActivation (8)                              [1, 320, 80, 26] [1, 1280, 80, 26] --              False
│    │    └─Conv2d (0)                                       [1, 320, 80, 26] [1, 1280, 80, 26] (409,600)       False
│    │    └─BatchNorm2d (1)                                  [1, 1280, 80, 26] [1, 1280, 80, 26] (2,560)         False
│    │    └─SiLU (2)                                         [1, 1280, 80, 26] [1, 1280, 80, 26] --              --
├─AdaptiveAvgPool2d (avgpool)                                [1, 1280, 80, 26] [1, 1280, 1, 1] --              --
├─Sequential (classifier)                                    [1, 1280]       [1, 2]          --              True
│    └─Dropout (0)                                           [1, 1280]       [1, 1280]       --              --
│    └─Linear (1)                                            [1, 1280]       [1, 2]          2,562           True
========================================================================================================================
Total params: 4,010,110
Trainable params: 2,562
Non-trainable params: 4,007,548
Total mult-adds (G): 16.16
========================================================================================================================
Input size (MB): 25.04
Forward/backward pass size (MB): 4505.09
Params size (MB): 16.04
Estimated Total Size (MB): 4546.17

```


# Results, I guess?
## Transfer Learning with EfficientNet
As I did on ViT, I've made EfficientNet learn on imbalance data. Normal dataset has about 221 images and Defect has about 1300. Results are like following

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

