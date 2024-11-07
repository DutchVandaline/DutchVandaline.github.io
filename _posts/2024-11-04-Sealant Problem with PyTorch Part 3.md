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

#### Data Augmentation
```python
normal_folder = os.path.join(image_path, "normal")
save_dir = normal_folder

# 증강된 이미지 저장 폴더 생성
if not os.path.exists(save_dir):
    os.makedirs(save_dir)


# 증강 변환 설정 (가우시안 노이즈 포함)
def augment_image(image):
    augmentation = transforms.Compose([
        transforms.RandomAffine(
            degrees=8,  # ±8도 회전
            translate=(0.03, 0.03),  # ±3% 범위 이동
            scale=(0.95, 1.05),  # ±5% 범위 스케일 조절
        ),
        transforms.ToTensor(),
        transforms.Lambda(lambda x: x + 0.02 * torch.randn_like(x)),  # 가우시안 노이즈 추가
        transforms.ToPILImage()
    ])
    return augmentation(image)


# 폴더 내 모든 이미지에 대해 무작위 증강 수행
for filename in os.listdir(normal_folder):
    if filename.endswith(".jpg") or filename.endswith(".png"):
        img_path = os.path.join(normal_folder, filename)
        original_image = Image.open(img_path)
        base_name = os.path.splitext(filename)[0]

        # 각 이미지에 대해 랜덤 증강 개수 지정 (예: 5~10 사이 랜덤 증강)
        num_augments = random.randint(5, 10)
        for i in range(num_augments):
            augmented_image = augment_image(original_image)
            save_path = os.path.join(save_dir, f"{base_name}_aug_{i + 1}.jpg")
            augmented_image.save(save_path)
            print(f"Saved augmented image: {save_path}")

print("All images have been randomly augmented and saved.")

```
 #### Split data by 80% / 20%
```python
base_dir = 'C:/junha/Personal_Notebook/oversampling_data'
train_dir = 'C:/junha/Personal_Notebook/oversampling_data/train'
test_dir = 'C:/junha/Personal_Notebook/oversampling_data/test'

# Create train and test directories
os.makedirs(os.path.join(train_dir, 'defect'), exist_ok=True)
os.makedirs(os.path.join(train_dir, 'normal'), exist_ok=True)
os.makedirs(os.path.join(test_dir, 'defect'), exist_ok=True)
os.makedirs(os.path.join(test_dir, 'normal'), exist_ok=True)


# Function to split the dataset
def split_data(source_dir, train_dir, test_dir, split_ratio=0.8):
    # Get all files in the source directory
    files = os.listdir(source_dir)
    random.shuffle(files)

    # Split the files based on the ratio
    train_size = int(len(files) * split_ratio)

    train_files = files[:train_size]
    test_files = files[train_size:]

    # Copy files to the train directory
    for file in train_files:
        shutil.copy(os.path.join(source_dir, file), os.path.join(train_dir, file))

    # Copy files to the test directory
    for file in test_files:
        shutil.copy(os.path.join(source_dir, file), os.path.join(test_dir, file))


# Split defect and normal datasets
split_data(os.path.join(base_dir, 'defect'), os.path.join(train_dir, 'defect'), os.path.join(test_dir, 'defect'))
split_data(os.path.join(base_dir, 'normal'), os.path.join(train_dir, 'normal'), os.path.join(test_dir, 'normal'))

print("Data split completed successfully.")
```
<br>, <br>

## Progress
**1. Added Data Augmentation for OverSampling** <br>
**2. I've used GAN too, I will attatch at the bottom.** <br>
<br>

## What's Next?
**1. Train with OverSampling Data** 
<br>
<br>

## GAN
Generating Image based on (2352,824) was impossible for Google Colab so, I've made it to quarter size.
#### Discriminator
```python
class Discriminator(nn.Module):
    def __init__(self):
        super().__init__()
        image_size = 3 * 633 * 206  # 1/4 크기

        self.model = nn.Sequential(
            nn.Linear(image_size, 1024),
            nn.LeakyReLU(0.2, inplace=True),
            nn.Dropout(0.3),
            nn.Linear(1024, 512),
            nn.LeakyReLU(0.2, inplace=True),
            nn.Dropout(0.3),
            nn.Linear(512, 256),
            nn.LeakyReLU(0.2, inplace=True),
            nn.Dropout(0.3),
            nn.Linear(256, 1),
            nn.Sigmoid()
        )

    def forward(self, x):
        x = x.view(x.size(0), 3 * 633 * 206)
        out = self.model(x)
        return out.squeeze()

```
<br>

#### Generator
```python
# 이미지가 커서 안뽑히므로 1/4 크기로 수정
class Generator(nn.Module):
    def __init__(self):
        super().__init__()
        # 새로운 이미지 크기: 3채널 * 412 * 1266
        image_size = 3 * 633 * 206  # 1/4 크기

        self.model = nn.Sequential(
            nn.Linear(100, 1024),
            nn.LeakyReLU(0.2, inplace=True),
            nn.Linear(1024, 2048),
            nn.LeakyReLU(0.2, inplace=True),
            nn.Linear(2048, 4096),
            nn.LeakyReLU(0.2, inplace=True),
            nn.Linear(4096, image_size),
            nn.Tanh()
        )

    def forward(self, z):
        out = self.model(z)
        # 절반 크기의 이미지를 생성 (Batch_size, 3, 633, 206)
        return out.view(z.size(0), 3, 633, 206)


```
<br>

#### Train Step
```python
num_epochs = 30
n_critic = 5
display_step = 300

for epoch in range(num_epochs):
    print('Starting epoch {}...'.format(epoch))
    for i, (images, _) in enumerate(data_loader):
        real_images = Variable(images).to(device)
        generator.train()
        batch_size = real_images.size(0)
        d_loss = discriminator_train_step(batch_size, discriminator,
                                          generator, d_optimizer, criterion,
                                          real_images)

        g_loss = generator_train_step(batch_size, discriminator, generator, g_optimizer, criterion)

    generator.eval()
    print('g_loss: {}, d_loss: {}'.format(g_loss, d_loss))

    z = Variable(torch.randn(9, 100)).to(device)
    sample_images = generator(z).data.cpu()

    grid = make_grid(sample_images, nrow=3, normalize=True)

    grid = grid.permute(1, 2, 0).numpy()

    plt.imshow(grid)
    plt.axis('off')
    plt.show()

```
![image](https://github.com/user-attachments/assets/5a3ed9ec-1535-49d6-b9ef-d84d257d1e96)

