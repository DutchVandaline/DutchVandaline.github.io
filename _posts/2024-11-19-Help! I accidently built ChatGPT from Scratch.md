---
layout: single
title:  "Help! I accidently built ChatGPT from Scratch."
categories:
  - AI
---

<br>
![help-i-accidentally](https://github.com/user-attachments/assets/2639edc0-725c-4799-af24-ed96e51dd52f)


# To Start With
 I am a student learning Artificial Intelligence. I was doing some tests, creating stuff using PyTorch and Jupyter Notebook and accidentally made ChatGPT from Scratch. The initial was my personal study making a Classifier model and I got some urge to make ChatGPT. And yeah. It worked. These were what I can do.
 - I was able to make  `ViT`(Vision Transformer) from Scratch.
 - I was able to make `Encoder block` in `ViT`.

# Finding Recommendations
The biggest Recommendation was `Attention is all you need` and `GPT2` paper. I didn't know how to make decoder block but, I checked the `Attention is all you need` paper so that i can make decoder block. I will make a further notice about that section later on.

# Ways to go
![image](https://github.com/user-attachments/assets/95ee6a93-2409-4a2f-9231-6602c8124986)
<br>
Bert is a stack of Encoder Layer and GPT is a stack of Decoder layer. I knew how to make Encoder layer using Multihead-SelfAttention Layer and MultiLayer Perceptron but, not about Decoder layer. When I saw that image from `Attention is all you need`, I had a instinct that I can make the decoder layer. One thing added was Masked Multihead-SelfAttention layer. Before, let's talk about Tokenization and Preprocessing.<br>

## Tokenization
Tokenization is crutial for the LLM. LLM, a large language model doesn't actually *read* or *understand* the context of sentences. Humans read the line just by looking at the sentence level. Actually, human don't look all the words inside the sentence. **You assume what inner word will be.** On the other hand, computers looks at the words. You can learn by Computer Vision sector for example making CNN or ViT. AI model breaks image into smaller patch of images and analyzes the RGB value. In the same way, sentence needs to be patched, we call it tokenization.


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

