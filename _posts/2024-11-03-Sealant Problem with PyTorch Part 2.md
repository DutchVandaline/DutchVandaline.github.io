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
## Transfer Learning with ViT
I thought "Why just I give it a shot?" and the result was astonishing. 
<div style="display: flex; gap: 10px;">
    <img src="https://github.com/user-attachments/assets/7b0f5022-3624-41e7-8ab9-2147e276ba1a" width="300" height="300">
    <img src="https://github.com/user-attachments/assets/c18bf718-d245-442a-83a1-95441a494acf" width="300" height="300">
</div>
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
**1. Run EfficientNet to check if it is overfitting or not.** <br>
**2. Data imbalance can be a problem.**

