![image](https://github.com/user-attachments/assets/449861c7-6ae0-4247-a240-f55f7c30a377)---
layout: single
title:  "Let's make YOLO! Part 2"
categories:
  - AI
---

<br>
![image](https://github.com/user-attachments/assets/ff9c27b0-936b-4913-ad9d-910e3427699b)


# To Start With
Building RayCaster game using C or making bunch of apps and deploying on AppStore were just to improve my coding skills. I had a dream for making an Artificial Intelligence model. Of course I don't know well about Artificial Intelligence also, I'm not that fluent using PyTorch, too. I think it is necessary to hit the wall or dig some place wrong to build my skills. So, I have a challenge for myself. Before that, following is my skill that I can do with PyTorch: <br>
* Can build CNN(Convolutional Neural Network) using PyTorch.
* Can build TinyVGG using PyTorch.
* Can handle datasets and make dataloaders to train and test.
<br>
The reason why instructors or professors begin with Computer Vision problem for teaching how to write code on Artificial Intelligence is that Computer Vision Problem is visual, straight forward and easy to understand. CNN and TinyVGG is the basic of the Computer Vision and I understand it. Now, I wanted to build a SOTA(State-of-the-art) model on Computer Vision field by myself. A YOLO.
<br>

# Finding Recommendations
## YOLO Architectures
Looked up for papers about YOLO, found some blog posts about YOLO Architectures. But the base architecture I've followed was the image in YOLO paper. It seems simple, showing the starting image size of 448,448 using Convolutional Layers.
![image](https://github.com/user-attachments/assets/ed55c98e-ef96-45e6-9488-5409262cd48e)

## Datasets
Shout out to mrdbourke! I am using `pizza-steak-sushi` datasets which mrdbourke made. It's basically Food101 set. It has 225 training set, 75 testing sets. I thought it would be fine... I thought...
<br>

# Update
So, I thought the problem was about lack of training and testing sets but, it wasnt'. I wasn't able to solve the problem so I looked up the paper and found that YOLO has it's own Loss Function. I've been struggling with using CrossEntropyLoss. Following is the image of the Loss function in YOLO paper.
<img width="707" alt="스크린샷 2024-09-29 오후 9 22 23" src="https://github.com/user-attachments/assets/be244047-3ac9-40ce-b6c5-e3e8cd8f11ac">

```
import torch
import torch.nn as nn

class YOLOClassificationLoss(nn.Module):
    def __init__(self):
        super(YOLOClassificationLoss, self).__init__()
        self.mse_loss = nn.MSELoss()  # Mean Squared Error Loss for classification

    def forward(self, predictions, targets):
        """
        predictions: Tensor of shape (batch_size, S*S, num_classes) -> class probabilities for each grid cell
        targets: Tensor of shape (batch_size, S*S, num_classes) -> one-hot encoded true class labels
        """
        targets_one_hot = F.one_hot(targets, num_classes=predictions.size(-1)).float()
        # Apply MSE loss over the predicted and true class probabilities
        loss = self.mse_loss(predictions, targets_one_hot)
        return loss
```

```
loss_fn = YOLOClassificationLoss()
optimizer = torch.optim.Adam(params= model_0.parameters(), lr=0.01)
```

<br>

# Results
I've modified the Loss and made the loss to live between 0 and 1. But, I'm not sure whether it's training well or not.
```
 0%|          | 0/3 [00:00<?, ?it/s]
Epoch: 0
-----
Train loss : 0.46520 | Train acc :  28.12%
Test loss: 0.30556 | Test acc: 54.17% 

Epoch: 1
-----
Train loss : 0.47917 | Train acc :  28.12%
Test loss: 0.30556 | Test acc: 54.17% 

Epoch: 2
-----
Train loss : 0.47917 | Train acc :  28.12%
Test loss: 0.30556 | Test acc: 54.17% 
```
<br>

## Progress
**1. Found out that YOLO has it's own Loss Function.** <br>
**2. Modified the Loss Function and made it live between 0 and 1. But not sure whether it's working or not.** <br>
<br>

