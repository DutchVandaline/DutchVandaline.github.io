---
layout: single
title:  "Let's make YOLO! Part 1"
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

# Model
Hard part was matching the padding and stride size. I've calculated to match the size of tensor. Block 7 and Block 8 was hard to match the size.
```
from torch import nn

class YOLOV1(nn.Module):
  def __init__(self, input_shape: int,
               hidden_units: int,
               output_shape: int):
    super().__init__()
    self.block_1 = nn.Sequential(
        nn.Conv2d(in_channels=input_shape,out_channels=hidden_units,kernel_size= 7,stride=2,padding=3),
        nn.LeakyReLU(),
        nn.MaxPool2d(kernel_size=2,stride=2)
    )

    self.block_2 = nn.Sequential(
        nn.Conv2d(in_channels = hidden_units,out_channels = hidden_units,kernel_size = 3,padding=1),
        nn.LeakyReLU(),
        nn.MaxPool2d(kernel_size=2,stride=2),
    )

    self.block_3 = nn.Sequential(
        nn.Conv2d(in_channels = hidden_units,out_channels = 128,kernel_size = 1,padding = 0),
        nn.LeakyReLU(),
        nn.Conv2d(in_channels = 128,out_channels = 256,kernel_size = 3,padding = 1,),
        nn.LeakyReLU(),
        nn.Conv2d(in_channels=256,out_channels = 256,kernel_size = 1,padding = 0),
        nn.LeakyReLU(),
        nn.Conv2d(in_channels=256,out_channels=512,kernel_size = 3,padding = 1),
        nn.LeakyReLU(),
        nn.MaxPool2d(kernel_size =2,stride = 2)
    )

    self.block_4 = nn.Sequential(
        nn.Conv2d(in_channels=512,out_channels=256,kernel_size = 1,padding = 0),
        nn.LeakyReLU(),
        nn.Conv2d(in_channels=256,out_channels=512,kernel_size = 3,padding = 1),
        nn.LeakyReLU(),

        nn.Conv2d(in_channels=512,out_channels=256,kernel_size = 1,padding = 0),
        nn.LeakyReLU(),
        nn.Conv2d(in_channels=256,out_channels=512,kernel_size = 3,padding = 1),
        nn.LeakyReLU(),

        nn.Conv2d(in_channels=512,out_channels=256,kernel_size = 1,padding = 0),
        nn.LeakyReLU(),
        nn.Conv2d(in_channels=256,out_channels=512,kernel_size = 3,padding = 1),
        nn.LeakyReLU(),

        nn.Conv2d(in_channels=512,out_channels=256,kernel_size = 1,padding = 0),
        nn.LeakyReLU(),
        nn.Conv2d(in_channels=256,out_channels=512,kernel_size = 3,padding = 1),
        nn.LeakyReLU(),

        nn.Conv2d(in_channels=512,out_channels=512,kernel_size = 1, padding = 0),
        nn.LeakyReLU(),

        nn.Conv2d(in_channels=512,out_channels=1024,kernel_size = 3,padding = 1),
        nn.LeakyReLU(),
        nn.MaxPool2d(kernel_size =2,stride = 2)
    )

    self.block_5 = nn.Sequential(
      nn.Conv2d(in_channels=1024, out_channels=512, kernel_size=1, padding=0),
      nn.LeakyReLU(),
      nn.Conv2d(in_channels=512, out_channels=1024, kernel_size=3, padding=1),
      nn.LeakyReLU(),

      nn.Conv2d(in_channels=1024, out_channels=512, kernel_size=1, padding=0),
      nn.LeakyReLU(),
      nn.Conv2d(in_channels=512, out_channels=1024, kernel_size=3, padding=1),
      nn.LeakyReLU(),

      nn.Conv2d(in_channels=1024, out_channels=1024, kernel_size=3, padding=1),
      nn.LeakyReLU(),

      nn.Conv2d(in_channels=1024, out_channels=1024, kernel_size=3, padding=1, stride=2),
      nn.LeakyReLU(),
  )
    self.block_6 = nn.Sequential(
        nn.Conv2d(in_channels=1024, out_channels=1024, kernel_size=3, padding=0,),
        nn.LeakyReLU(),
        nn.Conv2d(in_channels=1024, out_channels=1024, kernel_size=3, padding=1,),
        nn.LeakyReLU(),
    )

    self.flatten = nn.Flatten()

    self.block_7 = nn.Linear(in_features=1024 * 5 * 5, out_features=4096)

    self.block_8 = nn.Linear(in_features=4096, out_features=output_shape)


  def forward(self, x:torch.Tensor):
    x = self.block_1(x)
    x = self.block_2(x)
    x = self.block_3(x)
    x = self.block_4(x)
    x = self.block_5(x)
    x = self.block_6(x) 

    x = self.flatten(x)

    x = self.block_7(x)
    x = self.block_8(x)

    return x


```
<br>

# Results
I was glad for model running but the problem is crystal clear. Loss is too big. Accuracy is not the problem. Loss is way too big. I think the problem is the size of training and testing set. Total 300 images are not enough. I have to increase it more. Let's see the loss changes. 
```
100%
 3/3 [02:44<00:00, 55.18s/it]
Epoch: 0
-----
Train loss : 152132862049970552832.00000 | Train acc :  29.69%
Test loss: 12687692382930468864.00000 | Test acc: 26.04% 

Epoch: 1
-----
Train loss : 4341873112951807803392.00000 | Train acc :  28.91%
Test loss: 7534591419435110629376.00000 | Test acc: 54.17% 

Epoch: 2
-----
Train loss : 1530760424756814544896.00000 | Train acc :  38.28%
Test loss: 230886366355576389107712.00000 | Test acc: 26.04% 
```
<br>

## Progress
**1. Model worked, it means a lot to me.** <br>
**2. Problem is the size of training, testing image, I guess.** <br>
<br>


