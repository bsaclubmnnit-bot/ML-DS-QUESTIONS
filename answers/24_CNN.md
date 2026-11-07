# Section 24: Convolutional Neural Networks (CNN)

---

## Q321. What is a CNN?

A **Convolutional Neural Network (CNN)** is a deep learning architecture designed for processing **grid-structured data** such as images, video, and audio spectrograms. It uses **convolutional layers** to automatically learn spatial hierarchies of features.

**Key components:**
1. **Convolutional layers** — learn local features via filters
2. **Activation functions** — introduce non-linearity (usually ReLU)
3. **Pooling layers** — downsample spatial dimensions
4. **Fully connected layers** — final classification/regression

```python
import torch.nn as nn

class SimpleCNN(nn.Module):
    def __init__(self, num_classes=10):
        super().__init__()
        self.features = nn.Sequential(
            nn.Conv2d(3, 32, kernel_size=3, padding=1),  # conv layer
            nn.ReLU(),
            nn.MaxPool2d(2, 2),                          # pooling
            nn.Conv2d(32, 64, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(2, 2)
        )
        self.classifier = nn.Sequential(
            nn.Flatten(),
            nn.Linear(64 * 8 * 8, 512),
            nn.ReLU(),
            nn.Linear(512, num_classes)
        )
    
    def forward(self, x):
        return self.classifier(self.features(x))
```

**Famous CNNs:** LeNet, AlexNet, VGG, ResNet, InceptionNet, EfficientNet.

---

## Q322. Why are CNNs effective for images?

CNNs are effective for images because they exploit three key **structural properties** of image data:

1. **Local connectivity (sparse interactions):**
   - Pixels in proximity are strongly correlated
   - Each filter looks at a small local region → more efficient than fully connected

2. **Translation invariance (parameter sharing):**
   - Same filter applied across all positions → learns features regardless of location
   - A cat detector works whether the cat is in top-left or bottom-right

3. **Hierarchical feature learning:**
   - Early layers: edges, corners, colors
   - Middle layers: textures, shapes, parts
   - Deep layers: semantic concepts (faces, objects)

**Comparison with MLP:**
| Property | MLP | CNN |
|----------|-----|-----|
| Parameters for 224×224×3 image | Millions | Far fewer |
| Spatial structure | Ignored | Exploited |
| Translation invariance | No | Yes |
| Feature hierarchy | No | Yes |

> CNNs achieve human-level performance on ImageNet classification — a task where MLPs severely underperform.

---

## Q323. What is convolution?

**Convolution** is the core mathematical operation in CNNs where a **filter (kernel)** slides across the input to produce a feature map.

**Operation:**
```
(f * g)[i, j] = Σₘ Σₙ f[m, n] · g[i+m, j+n]
```

- For each position: element-wise multiply filter with input patch → sum → single value
- Slide filter across entire input → output is a **feature map**

```python
import torch
import torch.nn as nn

# Manual 2D convolution
conv = nn.Conv2d(
    in_channels=1,    # grayscale
    out_channels=1,   # one filter
    kernel_size=3,    # 3×3 filter
    stride=1,
    padding=0
)

import torch
x = torch.randn(1, 1, 5, 5)  # batch=1, channels=1, H=5, W=5
output = conv(x)              # output: (1, 1, 3, 3)

# Output size formula:
# out = floor((in + 2*padding - kernel_size) / stride) + 1
# out = floor((5 + 0 - 3) / 1) + 1 = 3
```

**Example — edge detection kernel:**
```
[-1  0  1]
[-2  0  2]    ← Sobel filter (detects vertical edges)
[-1  0  1]
```

---

## Q324. What is a convolutional filter or kernel?

A **filter** (also called a **kernel**) is a small learnable weight matrix that slides over the input to detect specific patterns.

**Properties:**
- Typically 3×3 or 5×5 (spatial dimensions)
- Depth = number of input channels (e.g., 3 for RGB)
- One filter → one feature map; N filters → N feature maps

```python
import torch.nn as nn

# Layer with 32 filters of size 3×3 applied to 3-channel input
conv = nn.Conv2d(in_channels=3, out_channels=32, kernel_size=3)

# Parameters: 3 × 3 × 3 × 32 + 32 (bias) = 896
print(sum(p.numel() for p in conv.parameters()))  # 896
```

**What filters learn:**
- Filter 1 might detect horizontal edges
- Filter 2 might detect vertical edges
- Filter N might detect complex textures

**Key point:** Filters are **learned automatically** from data via backpropagation — not hand-crafted (unlike traditional computer vision).

---

## Q325. What is stride?

**Stride** is the number of pixels the filter **moves** (slides) at each step across the input.

**Effect of stride:**
- Stride = 1: Filter moves 1 pixel at a time (default, maximum output resolution)
- Stride = 2: Filter jumps 2 pixels → output is roughly half the size
- Larger stride → smaller output, fewer computations

**Output size formula:**
```
out_size = floor((input_size - kernel_size + 2 * padding) / stride) + 1
```

```python
import torch
import torch.nn as nn

x = torch.randn(1, 1, 8, 8)

conv_s1 = nn.Conv2d(1, 1, kernel_size=3, stride=1, padding=0)
conv_s2 = nn.Conv2d(1, 1, kernel_size=3, stride=2, padding=0)

print(conv_s1(x).shape)  # (1, 1, 6, 6)  → (8-3)/1 + 1 = 6
print(conv_s2(x).shape)  # (1, 1, 3, 3)  → (8-3)/2 + 1 = 3
```

**Use cases:**
- Stride > 1 as **alternative to pooling** for downsampling (e.g., strided convolutions in ResNet)
- Preferred over max pooling in some modern architectures

---

## Q326. What is padding?

**Padding** adds extra values (usually zeros) around the border of the input before applying convolution.

**Purpose:**
1. **Control output size** — preserve spatial dimensions
2. **Preserve border information** — without padding, corner pixels are used less

**Types:**
| Type | Description | Output Size |
|------|-------------|------------|
| `padding=0` (Valid) | No padding | Smaller than input |
| `padding='same'` | Pads to maintain size | Same as input |
| `padding=k` | Custom padding | Configurable |

```python
import torch
import torch.nn as nn

x = torch.randn(1, 1, 6, 6)

# No padding — output shrinks
no_pad = nn.Conv2d(1, 1, kernel_size=3, padding=0)
print(no_pad(x).shape)  # (1, 1, 4, 4)

# Padding=1 — output same size
same_pad = nn.Conv2d(1, 1, kernel_size=3, padding=1)
print(same_pad(x).shape)  # (1, 1, 6, 6)
```

**Standard practice:** Use `padding=1` with 3×3 kernels to maintain spatial dimensions throughout the network.

---

## Q327. What is a feature map?

A **feature map** (also called **activation map**) is the output of applying a single convolutional filter to an input. It represents where and how strongly a particular feature (e.g., edge, texture) is detected at each spatial location.

**Properties:**
- One filter → one 2D feature map
- N filters → N feature maps stacked = output volume of shape `(N, H, W)`
- Values represent the strength of feature detection at each position

```python
import torch
import torch.nn as nn
import matplotlib.pyplot as plt

# Single conv layer with 8 filters
conv = nn.Conv2d(1, 8, kernel_size=3, padding=1)

x = torch.randn(1, 1, 28, 28)  # single grayscale image
feature_maps = conv(x)          # shape: (1, 8, 28, 28)

print(f"Number of feature maps: {feature_maps.shape[1]}")  # 8
print(f"Feature map size: {feature_maps.shape[2:]}") # (28, 28)

# Visualize feature maps
fig, axes = plt.subplots(1, 8, figsize=(16, 2))
for i, ax in enumerate(axes):
    ax.imshow(feature_maps[0, i].detach(), cmap='viridis')
    ax.axis('off')
```

> Each feature map captures **one aspect** of the input — early maps detect low-level features; deeper maps detect semantic features.

---

## Q328. What is pooling?

**Pooling** is a downsampling operation that reduces the spatial dimensions of feature maps while retaining the most important information.

**Purpose:**
- **Reduce computation** — fewer parameters downstream
- **Control overfitting** — reduces spatial resolution
- **Translation invariance** — small shifts in input → same output
- **Increase receptive field** — each neuron sees larger area of input

**Types:**
- Max pooling (most common)
- Average pooling
- Global average pooling
- Adaptive pooling

```python
import torch.nn as nn

# Pooling reduces 28×28 → 14×14
max_pool = nn.MaxPool2d(kernel_size=2, stride=2)
avg_pool = nn.AvgPool2d(kernel_size=2, stride=2)

# Global pooling collapses spatial dims entirely
global_avg = nn.AdaptiveAvgPool2d((1, 1))  # (N, C, H, W) → (N, C, 1, 1)
```

**Placement:** Typically after activation functions in convolutional blocks.

---

## Q329. What is max pooling?

**Max pooling** selects the **maximum value** from each pooling window, retaining the most activated (strongest) feature response.

**How it works:**
```
Input patch:    Max Pool (2×2, stride=2):
[1  3  2  4]       [3  4]
[5  6  1  2]  →    [8  6]
[7  8  3  2]
[1  2  4  6]
```

```python
import torch
import torch.nn as nn

x = torch.tensor([[[[1., 3., 2., 4.],
                    [5., 6., 1., 2.],
                    [7., 8., 3., 2.],
                    [1., 2., 4., 6.]]]])

pool = nn.MaxPool2d(kernel_size=2, stride=2)
print(pool(x))
# tensor([[[[6., 4.],
#           [8., 6.]]]])
```

**Advantages:**
- Provides translation invariance (small shifts → same max value)
- Detects presence of features regardless of exact position
- No learnable parameters

**When to use:** Standard choice for most CNNs dealing with image classification.

---

## Q330. What is average pooling?

**Average pooling** computes the **mean value** of each pooling window, providing a smoothed representation.

```python
import torch
import torch.nn as nn

x = torch.tensor([[[[1., 3., 2., 4.],
                    [5., 6., 1., 2.],
                    [7., 8., 3., 2.],
                    [1., 2., 4., 6.]]]])

avg_pool = nn.AvgPool2d(kernel_size=2, stride=2)
print(avg_pool(x))
# tensor([[[[3.75, 2.25],
#           [4.50, 3.75]]]])

# Global Average Pooling (GAP) — replaces FC layers
gap = nn.AdaptiveAvgPool2d(1)  # collapses entire feature map to 1 value
print(gap(x).shape)  # (1, 1, 1, 1)
```

**Comparison with Max Pooling:**
| | Max Pooling | Average Pooling |
|--|-------------|----------------|
| Operation | Maximum | Mean |
| Use case | Feature detection | Smoothing, final layer |
| Common in | Classification layers | Global pooling before classifier |

**Global Average Pooling** (GAP) — used in modern CNNs (ResNet, MobileNet) to replace large fully connected layers, reducing parameters and overfitting.

---

## Q331. What is a receptive field?

The **receptive field** is the region of the **input image** that a particular neuron (or feature map cell) is responsive to — i.e., the area it "sees."

- **Local receptive field:** size of input seen by a single neuron in a given layer
- **Effective receptive field:** total input region influencing a deep layer's output

**How it grows with depth:**
```
Layer 1 (3×3 conv): receptive field = 3×3
Layer 2 (3×3 conv): receptive field = 5×5
Layer 3 (3×3 conv): receptive field = 7×7

With stride 2: grows faster
```

**Formula (with stride=1):**
```
RF_layer = RF_(layer-1) + (kernel_size - 1) × stride_product
```

**Why it matters:**
- Deeper layers "see" more context → can detect larger objects
- Two 3×3 conv layers = one 5×5 conv layer receptively, but with fewer parameters and more non-linearity

```python
# Two 3×3 convs (18 params per channel) vs one 5×5 (25 params per channel)
conv_3x3_x2 = nn.Sequential(
    nn.Conv2d(C, C, 3, padding=1),  # same receptive field as...
    nn.Conv2d(C, C, 3, padding=1)
)
conv_5x5 = nn.Conv2d(C, C, 5, padding=2)  # more parameters, less non-linearity
```

---

## Q332. What is parameter sharing?

**Parameter sharing** means that **the same filter weights** are used across all spatial positions in the input when computing a feature map.

**How it works:**
- One filter: W (e.g., 3×3×3 = 27 weights)
- Applied to ALL positions in the input
- All positions share the same 27 weights → massive parameter reduction

**Benefits:**
- **Huge reduction in parameters** — vs. fully connected layers
- **Translation equivariance** — same features detected at all positions
- **Implicit data augmentation** — each weight trained on many input patches

**Comparison:**
```
Image: 224×224×3

Fully Connected Layer → 224×224×3 = 150,528 params per output neuron
Conv Layer (3×3, 64 filters) → 3×3×3×64 = 1,728 params total
```

```python
import torch.nn as nn

# All these conv operations share the SAME kernel weights
# regardless of where in the 224×224 image they operate
conv = nn.Conv2d(3, 64, kernel_size=3, padding=1)
print(conv.weight.shape)  # (64, 3, 3, 3) — only 1,728 weight values
```

---

## Q333. What is data augmentation?

**Data augmentation** artificially **increases the size and diversity** of the training dataset by applying random, label-preserving transformations to training images.

**Purpose:**
- Reduces overfitting
- Improves generalization
- Makes model invariant to real-world variations

**Common transformations:**

```python
import torchvision.transforms as T

augmentation = T.Compose([
    T.RandomHorizontalFlip(p=0.5),       # flip left-right
    T.RandomVerticalFlip(p=0.2),         # flip up-down
    T.RandomRotation(degrees=30),         # rotate ±30°
    T.RandomCrop(224, padding=20),        # random crop
    T.ColorJitter(brightness=0.2,         # color variation
                  contrast=0.2,
                  saturation=0.2,
                  hue=0.1),
    T.RandomGrayscale(p=0.1),            # occasional grayscale
    T.GaussianBlur(kernel_size=3),        # blur
    T.ToTensor(),
    T.Normalize(mean=[0.485,0.456,0.406],
                std=[0.229,0.224,0.225])
])
```

**Advanced techniques:**
- **Cutout/Random Erasing** — mask out random patches
- **Mixup** — blend two images and interpolate labels
- **CutMix** — paste patch from one image to another
- **AutoAugment** — learned augmentation policies

---

## Q334. What is transfer learning in CNNs?

**Transfer learning** uses a CNN **pre-trained on a large dataset** (e.g., ImageNet) and adapts it to a new, often smaller dataset.

**Motivation:**
- Training deep CNNs requires massive data and compute
- Learned features (edges, textures, shapes) are general and reusable
- Even with few examples, transfer learning achieves high performance

**Strategies:**

```python
import torchvision.models as models
import torch.nn as nn

# Load pre-trained ResNet50
model = models.resnet50(pretrained=True)

# Strategy 1: Feature Extraction — freeze all layers
for param in model.parameters():
    param.requires_grad = False

# Replace final layer for new task (e.g., 5 classes)
model.fc = nn.Linear(model.fc.in_features, 5)
# Only fc layer trains

# Strategy 2: Fine-tuning — unfreeze last few layers
for param in model.layer4.parameters():
    param.requires_grad = True

# Strategy 3: Full fine-tuning (all layers, small LR)
for param in model.parameters():
    param.requires_grad = True
optimizer = torch.optim.Adam(model.parameters(), lr=1e-5)  # small LR
```

**When to use which strategy:**
| Dataset Size | Similar to Source? | Strategy |
|-------------|-------------------|----------|
| Small | Yes | Feature extraction |
| Small | No | Fine-tune last layers |
| Large | Yes | Fine-tune all layers |
| Large | No | Train from scratch |

---

## Q335. What causes overfitting in CNNs?

Overfitting in CNNs occurs when the model **memorizes training data** rather than learning generalizable features.

**Causes:**

1. **Insufficient training data** — most common cause
2. **Model too large** — too many parameters relative to data
3. **No regularization** — no dropout, weight decay
4. **Training too long** — too many epochs without early stopping
5. **High-resolution features memorized** — small dataset + large model

**Signs:**
- Training accuracy: ~99%
- Validation accuracy: ~70% (large gap)

**Solutions:**

```python
import torch.nn as nn

# 1. Dropout
nn.Dropout2d(p=0.25)  # spatial dropout for conv layers
nn.Dropout(p=0.5)      # for FC layers

# 2. L2 Weight Decay (regularization via optimizer)
optimizer = torch.optim.Adam(model.parameters(), lr=1e-3, weight_decay=1e-4)

# 3. Data Augmentation (see Q333)
augmentation = T.Compose([T.RandomHorizontalFlip(), T.RandomCrop(32, padding=4)])

# 4. Batch Normalization
nn.BatchNorm2d(num_features=64)

# 5. Early Stopping
# Monitor val_loss, stop when it starts increasing

# 6. Reduce model complexity
# Use smaller architecture or reduce # of filters

# 7. Transfer Learning
# Use pre-trained features instead of learning from scratch
```

> **Key insight:** The best cure for overfitting in CNNs is **more data** or **data augmentation**.
