# Part V: Deep Learning

> **100 Interview Questions & Comprehensive Technical Solutions**  
> *Topics: Neural Networks, Backpropagation, CNNs, RNNs, LSTMs, GRUs, BiLSTM, Transformers & Embeddings*  
> *Part of the [PIXEL CHAMP Master Question Bank](https://github.com/bsaclubmnnit-bot/ML-DS-QUESTIONS)*

---

## DL-001: How does gradient descent train a neural network?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Gradient descent** iteratively updates network weights in the direction that minimizes the loss function.

**Update rule:**
```
W = W - η · ∂L/∂W
b = b - η · ∂L/∂b
```
where `η` is the learning rate.

**Variants:**
| Variant | Description |
|---------|-------------|
| Batch GD | Uses all training data per update — stable but slow |
| Stochastic GD (SGD) | Uses one sample per update — noisy but fast |
| Mini-batch GD | Uses small batches — best of both worlds (standard) |

```python
import torch.optim as optim

model = SimpleNet()
optimizer = optim.SGD(model.parameters(), lr=0.01)

# Training loop
for epoch in range(100):
    for X_batch, y_batch in dataloader:
        optimizer.zero_grad()         # clear old gradients
        predictions = model(X_batch)  # forward pass
        loss = criterion(predictions, y_batch)  # compute loss
        loss.backward()               # backpropagation
        optimizer.step()              # update weights
```

**Advanced optimizers:** Adam, RMSProp, AdaGrad — adapt learning rate per parameter.

---

---

## DL-002: What are many-to-many architectures?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Many-to-many** RNN architectures take a **sequence as input** and produce a **sequence as output**. Two variants:

**Variant 1: Synchronized (equal length)**
```
x₁ → [RNN] → h₁ → ŷ₁
x₂ → [RNN] → h₂ → ŷ₂
x₃ → [RNN] → h₃ → ŷ₃
```
Input and output same length — used for **tagging, NER, POS**.

**Variant 2: Encoder-Decoder (variable length)**
```
Encode: x₁,x₂,x₃ → context
Decode: context → ŷ₁,ŷ₂,ŷ₄,ŷ₅
```
Used for **machine translation, summarization**.

```python
import torch.nn as nn

# Synchronized many-to-many: predict label at EACH time step
class NERModel(nn.Module):
    def __init__(self, vocab_size, embed_dim, hidden_size, num_tags):
        super().__init__()
        self.embed = nn.Embedding(vocab_size, embed_dim)
        self.rnn = nn.LSTM(embed_dim, hidden_size, batch_first=True,
                           bidirectional=True)
        self.fc = nn.Linear(hidden_size * 2, num_tags)
    
    def forward(self, x):
        x = self.embed(x)
        output, _ = self.rnn(x)
        return self.fc(output)  # prediction at EACH time step
```

---

---

## DL-003: What are many-to-one architectures?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Many-to-one** RNN architectures take a **sequence as input** and produce a **single output** at the end.

```
x₁ → [RNN] → h₁
x₂ → [RNN] → h₂
x₃ → [RNN] → h₃ → [Output Layer] → ŷ (single output)
```

```python
import torch.nn as nn

class SentimentRNN(nn.Module):
    def __init__(self, vocab_size, embed_dim, hidden_size, num_classes):
        super().__init__()
        self.embed = nn.Embedding(vocab_size, embed_dim)
        self.rnn = nn.LSTM(embed_dim, hidden_size, batch_first=True)
        self.fc = nn.Linear(hidden_size, num_classes)
    
    def forward(self, x):
        x = self.embed(x)
        output, (hn, _) = self.rnn(x)
        # Use only LAST hidden state for classification
        return self.fc(hn[-1])  # many-to-one
```

**Use cases:**
- **Sentiment analysis** — sentence → positive/negative
- **Text classification** — document → category
- **Time series classification** — stock movements → trend label
- **Activity recognition** — video frames → action label

---

---

## DL-004: What are weights and biases?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Weights** and **biases** are the **learnable parameters** of a neural network.

**Weights (`w`):**
- Control the **strength and direction** of the connection between neurons
- Positive weight → activates next neuron; negative → inhibits
- Network learns by adjusting weights to minimize loss

**Bias (`b`):**
- A constant added to the weighted sum: `z = wᵀx + b`
- Allows the activation function to **shift** left or right
- Without bias, the neuron cannot activate unless input is non-zero
- Analogous to the intercept in linear regression

```python
import torch
import torch.nn as nn

linear = nn.Linear(3, 1)
print(linear.weight)  # learnable weights, shape (1, 3)
print(linear.bias)    # learnable bias, shape (1,)

# Forward pass
x = torch.tensor([[1.0, 2.0, 3.0]])
z = linear(x)  # z = w @ x.T + b
```

> **Key insight:** During training, gradient descent updates both weights and biases to minimize the loss function.

---

---

## DL-005: What causes overfitting in CNNs?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-006: What is ReLU?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**ReLU** (Rectified Linear Unit) is the most widely used activation function in deep learning.

**Formula:**
```
ReLU(x) = max(0, x)
```

**Derivative:**
```
ReLU'(x) = 1 if x > 0, else 0
```

**Advantages:**
- Computationally efficient (simple threshold)
- No vanishing gradient for positive values
- Promotes sparse activations (many zeros → efficient)
- Converges faster than sigmoid/tanh

**Disadvantage — Dying ReLU problem:**
- Neurons with `x < 0` always output 0 → gradient = 0 → neuron never updates

**Variants:**
```python
import torch.nn as nn

relu        = nn.ReLU()          # max(0, x)
leaky_relu  = nn.LeakyReLU(0.01) # max(0.01x, x) — fixes dying ReLU
prelu       = nn.PReLU()         # learnable slope for x < 0
elu         = nn.ELU(alpha=1.0)  # smooth negative side
gelu        = nn.GELU()          # used in BERT, GPT
```

---

---

## DL-007: What is a CNN?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-008: What is a convolutional filter or kernel?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-009: What is a feature map?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-010: What is a hidden layer?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

A **hidden layer** is any layer between the input and output layers. It's called "hidden" because its values are not directly observed in input or output.

**Role:**
- Learns **intermediate representations** of the data
- Each successive layer learns increasingly abstract features
- More hidden layers = **deeper network** = more representational power

```python
import torch.nn as nn

model = nn.Sequential(
    nn.Linear(784, 256),  # input → hidden 1
    nn.ReLU(),
    nn.Linear(256, 128),  # hidden 1 → hidden 2
    nn.ReLU(),
    nn.Linear(128, 10),   # hidden 2 → output
)
```

**Number of hidden layers:**
| Depth | Capability |
|-------|-----------|
| 0 | Linear model only |
| 1 | Can approximate any continuous function |
| 2+ | More efficient approximation of complex functions |
| Deep (5+) | Hierarchical feature learning |

> **Rule of thumb:** Start with 1-2 hidden layers; add more if underfitting.

---

---

## DL-011: What is a hidden state?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

The **hidden state** (`hₜ`) is the RNN's internal memory that **summarizes all information** seen up to time step `t`.

**Properties:**
- A fixed-size vector (dimension = `hidden_size`)
- Updated at every time step: `hₜ = f(xₜ, hₜ₋₁)`
- Passed to the next time step (and used for prediction)
- Initialized to zeros at the start of a sequence

```python
import torch
import torch.nn as nn

rnn = nn.RNN(input_size=5, hidden_size=16, batch_first=True)

# Initialize hidden state
batch_size = 3
h0 = torch.zeros(1, batch_size, 16)  # (num_layers, batch, hidden_size)

x = torch.randn(batch_size, 10, 5)   # 10 time steps

output, hn = rnn(x, h0)
# output: (3, 10, 16) — hidden state at EVERY time step
# hn:     (1, 3, 16)  — hidden state at LAST time step only

# Access hidden state at each time step
h_t3 = output[:, 2, :]  # hidden state at t=3
```

**Limitation:** The fixed-size hidden state must compress all history — long sequences → information is lost (long-term dependency problem).

---

---

## DL-012: What is a learning rate?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

The **learning rate (η)** controls **how much weights are updated** during each gradient descent step.

**Effect:**
| Learning Rate | Effect |
|--------------|--------|
| Too high | Diverges — overshoots minimum, loss oscillates or increases |
| Too low | Converges very slowly, may get stuck in local minima |
| Just right | Fast, stable convergence to good minimum |

```python
import torch.optim as optim

# Fixed learning rate
optimizer = optim.SGD(model.parameters(), lr=0.01)

# Learning rate scheduling
scheduler = optim.lr_scheduler.StepLR(optimizer, step_size=10, gamma=0.5)
# Reduces LR by half every 10 epochs

# Cosine annealing
scheduler = optim.lr_scheduler.CosineAnnealingLR(optimizer, T_max=50)
```

**Common strategies:**
- Start with `lr = 0.001` (Adam) or `lr = 0.01` (SGD)
- Use **learning rate warmup** + decay schedules
- Use **cyclical learning rates** to escape local minima
- **Learning rate finder:** sweep LR and pick value before loss flattens

---

---

## DL-013: What is a receptive field?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-014: What is an Artificial Neural Network?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

An **Artificial Neural Network (ANN)** is a computational model inspired by the biological neural networks in the human brain. It consists of layers of interconnected **artificial neurons** (nodes) that learn to map inputs to outputs through training.

**Architecture:**
```
Input Layer → Hidden Layer(s) → Output Layer
```

- **Input layer:** receives raw features
- **Hidden layers:** learn intermediate representations
- **Output layer:** produces predictions

```python
import tensorflow as tf
from tensorflow import keras

model = keras.Sequential([
    keras.layers.Dense(64, activation='relu', input_shape=(10,)),  # hidden
    keras.layers.Dense(32, activation='relu'),                      # hidden
    keras.layers.Dense(1,  activation='sigmoid')                    # output
])
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
```

ANNs are universal function approximators — given enough neurons and layers, they can approximate any continuous function.

---

---

## DL-015: What is an RNN?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

A **Recurrent Neural Network (RNN)** is a type of neural network designed to process **sequential data** by maintaining a **hidden state** that carries information from previous time steps.

**Key idea:** Unlike feedforward networks, RNNs have **loops** — the output at time `t` depends on both the current input and the previous hidden state.

**Equations:**
```
hₜ = tanh(Wₕ · hₜ₋₁ + Wₓ · xₜ + b)
ŷₜ = Wᵧ · hₜ + bᵧ
```

```python
import torch
import torch.nn as nn

# Simple RNN
rnn = nn.RNN(
    input_size=10,    # features per time step
    hidden_size=32,   # hidden state dimension
    num_layers=1,
    batch_first=True  # (batch, seq_len, features)
)

x = torch.randn(4, 8, 10)       # batch=4, seq_len=8, features=10
output, h_n = rnn(x)            # output: (4,8,32), h_n: (1,4,32)
```

**Core property:** The hidden state `hₜ` acts as a **memory** — summarizing information from all past inputs `x₁, x₂, ..., xₜ`.

---

---

## DL-016: What is an activation function?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

An **activation function** determines whether and how strongly a neuron fires given its input. It introduces **non-linearity** into the network.

**Common activation functions:**

| Function | Formula | Range |
|----------|---------|-------|
| Sigmoid | `1 / (1 + e⁻ˣ)` | (0, 1) |
| Tanh | `(eˣ - e⁻ˣ)/(eˣ + e⁻ˣ)` | (-1, 1) |
| ReLU | `max(0, x)` | [0, ∞) |
| Leaky ReLU | `max(0.01x, x)` | (-∞, ∞) |
| Softmax | `eˣᵢ / Σeˣⱼ` | (0,1), sums to 1 |

```python
import torch
import torch.nn.functional as F

x = torch.tensor([-2.0, -1.0, 0.0, 1.0, 2.0])

print(F.sigmoid(x))   # (0,1)
print(torch.tanh(x))  # (-1,1)
print(F.relu(x))      # [0,inf)
print(F.softmax(x, dim=0))  # probabilities summing to 1
```

**Placement guide:**
- Hidden layers: ReLU (default), Leaky ReLU, GELU
- Binary classification output: Sigmoid
- Multi-class output: Softmax
- Regression output: Linear (none)

---

---

## DL-017: What is an artificial neuron?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

An **artificial neuron** (perceptron) is the basic unit of an ANN. It mimics a biological neuron by:

1. **Receiving inputs** `x₁, x₂, ..., xₙ`
2. **Computing weighted sum** `z = Σ(wᵢxᵢ) + b`
3. **Applying activation function** `output = f(z)`

**Diagram:**
```
x₁ —w₁—\
x₂ —w₂—→ [Σwᵢxᵢ + b] → f(z) → output
x₃ —w₃—/
```

```python
import numpy as np

def artificial_neuron(inputs, weights, bias, activation):
    z = np.dot(weights, inputs) + bias
    return activation(z)

# Example: single neuron with ReLU
output = artificial_neuron(
    inputs=np.array([1.0, 2.0, 3.0]),
    weights=np.array([0.5, -0.3, 0.8]),
    bias=0.1,
    activation=lambda z: max(0, z)
)
```

---

---

## DL-018: What is an epoch?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

An **epoch** is one complete pass through the **entire training dataset** during training.

- 1 epoch = every training sample has been seen once
- Training typically requires multiple epochs (10 to 100+)
- More epochs = more weight updates = more learning (but risk of overfitting)

```python
# Training for multiple epochs
n_epochs = 50

for epoch in range(n_epochs):
    total_loss = 0
    for X_batch, y_batch in train_loader:  # iterate all mini-batches
        optimizer.zero_grad()
        loss = criterion(model(X_batch), y_batch)
        loss.backward()
        optimizer.step()
        total_loss += loss.item()
    
    avg_loss = total_loss / len(train_loader)
    print(f"Epoch {epoch+1}/{n_epochs}, Loss: {avg_loss:.4f}")
```

**Monitoring:** Plot training and validation loss per epoch to detect overfitting.

**Early stopping:** Stop training when validation loss stops improving.

```python
from tensorflow.keras.callbacks import EarlyStopping
early_stop = EarlyStopping(monitor='val_loss', patience=5, restore_best_weights=True)
```

---

---

## DL-019: What is average pooling?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-020: What is backpropagation through time?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Backpropagation Through Time (BPTT)** is the algorithm used to train RNNs by unrolling the network across time steps and applying standard backpropagation.

**How it works:**
1. **Unroll** the RNN for `T` time steps (create a computation graph)
2. Compute loss at each time step (or final step)
3. Sum losses: `L = Σₜ Lₜ`
4. Backpropagate gradients through all time steps (backwards)
5. Accumulate gradients for shared weights `Wₕ`, `Wₓ`

**Gradient flow through time:**
```
∂L/∂W = Σₜ ∂Lₜ/∂W

∂L₅/∂h₁ = ∂L₅/∂h₅ · ∂h₅/∂h₄ · ∂h₄/∂h₃ · ∂h₃/∂h₂ · ∂h₂/∂h₁
           = product of Jacobians across 4 time steps
```

```python
import torch.nn as nn

# Truncated BPTT — limit backprop to k steps to reduce computation
# PyTorch handles this via detach()
def truncated_bptt(model, x_seq, k=10):
    h = None
    for i in range(0, len(x_seq), k):
        x_chunk = x_seq[i:i+k]
        out, h = model(x_chunk, h)
        h = h.detach()  # cut gradient flow beyond k steps
        loss = compute_loss(out)
        loss.backward()
```

**Problem:** Gradients multiply many times → **vanishing** or **exploding** gradients.

---

---

## DL-021: What is backpropagation?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Backpropagation** (backprop) is the algorithm used to compute gradients of the loss function with respect to every weight in the network, enabling gradient descent to update weights.

**Steps:**
1. Run **forward pass** → compute predictions and loss
2. Compute gradient of loss w.r.t. output: `∂L/∂ŷ`
3. Apply **chain rule** backwards through each layer
4. Compute `∂L/∂W` and `∂L/∂b` for each layer
5. Optimizer uses these gradients to update weights

**Chain rule:**
```
∂L/∂W₁ = ∂L/∂a₂ · ∂a₂/∂z₂ · ∂z₂/∂a₁ · ∂a₁/∂z₁ · ∂z₁/∂W₁
```

```python
import torch

x = torch.tensor([1.0, 2.0])
w = torch.tensor([0.5, -0.3], requires_grad=True)
b = torch.tensor(0.1, requires_grad=True)

# Forward pass
z = torch.dot(w, x) + b
loss = (z - 1.0) ** 2  # MSE with target=1

# Backward pass (backpropagation)
loss.backward()

print(w.grad)  # ∂L/∂w
print(b.grad)  # ∂L/∂b
```

> Backpropagation is **just the chain rule applied efficiently** using dynamic programming.

---

---

## DL-022: What is batch normalization?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Batch Normalization (BatchNorm)** normalizes the inputs of each layer to have **zero mean and unit variance** across the batch, then applies learnable scale and shift.

**Formula:**
```
x̂ = (x - μ_batch) / √(σ²_batch + ε)
y = γ · x̂ + β
```
where `γ` (scale) and `β` (shift) are learnable parameters.

```python
import torch.nn as nn

model = nn.Sequential(
    nn.Linear(256, 128),
    nn.BatchNorm1d(128),    # normalize after linear, before activation
    nn.ReLU(),
    nn.Linear(128, 64),
    nn.BatchNorm1d(64),
    nn.ReLU()
)
```

**Benefits:**
- Reduces internal covariate shift
- Allows higher learning rates → faster training
- Acts as regularizer → sometimes reduces need for dropout
- Mitigates vanishing/exploding gradients

**Variants:**
- `BatchNorm1d` — for fully connected/1D sequences
- `BatchNorm2d` — for CNN (normalizes per channel)
- `LayerNorm` — normalizes across features (used in Transformers)

---

---

## DL-023: What is batch size?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Batch size** is the number of training samples used in one forward/backward pass before updating weights.

**Types:**
| Batch Size | Type | Pros | Cons |
|-----------|------|------|------|
| 1 | Stochastic GD | Very noisy, can escape local minima | Slow, unstable |
| N (full dataset) | Batch GD | Stable, accurate gradient | Memory-intensive, slow |
| 32–256 | Mini-batch GD | Balanced speed and stability | Hyperparameter to tune |

```python
from torch.utils.data import DataLoader, TensorDataset
import torch

X = torch.randn(1000, 10)
y = torch.randint(0, 2, (1000,))

dataset = TensorDataset(X, y)
train_loader = DataLoader(dataset, batch_size=32, shuffle=True)

# Each iteration: 32 samples used for one gradient update
for X_batch, y_batch in train_loader:
    pass  # batch_size=32
```

**Effects of batch size:**
- **Larger batch:** more stable gradients, faster GPU utilization, but may generalize worse
- **Smaller batch:** more noise (regularizing effect), better generalization, slower
- **Common values:** 32, 64, 128, 256

> **Memory constraint:** Batch size is limited by GPU VRAM.

---

---

## DL-024: What is convolution?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-025: What is data augmentation?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-026: What is dropout?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Dropout** is a regularization technique that **randomly deactivates neurons** during training to prevent overfitting.

**How it works:**
- Each neuron is dropped (set to 0) with probability `p` during training
- At inference, all neurons are active but outputs are scaled by `(1-p)`
- Forces network to learn **redundant representations**

```python
import torch.nn as nn

model = nn.Sequential(
    nn.Linear(784, 512),
    nn.ReLU(),
    nn.Dropout(p=0.5),      # 50% neurons dropped during training
    nn.Linear(512, 256),
    nn.ReLU(),
    nn.Dropout(p=0.3),
    nn.Linear(256, 10)
)

# Dropout is automatically disabled during evaluation
model.train()  # dropout active
model.eval()   # dropout disabled
```

**Benefits:**
- Reduces overfitting effectively
- Acts as ensemble of many different network architectures
- Prevents co-adaptation of neurons

**Common dropout rates:** 0.2–0.5 for hidden layers; lower for convolutional layers.

---

---

## DL-027: What is forward propagation?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Forward propagation** is the process of passing input data through the network layer by layer to compute the output/prediction.

**Steps:**
1. Input `x` enters the network
2. For each layer: `z = Wx + b`, then `a = f(z)`
3. Output from one layer becomes input to next
4. Final layer produces prediction `ŷ`
5. Loss is computed: `L = loss(ŷ, y)`

```python
import torch
import torch.nn as nn

class SimpleNet(nn.Module):
    def __init__(self):
        super().__init__()
        self.fc1 = nn.Linear(4, 8)
        self.fc2 = nn.Linear(8, 1)
    
    def forward(self, x):
        # Forward propagation
        a1 = torch.relu(self.fc1(x))  # layer 1
        out = torch.sigmoid(self.fc2(a1))  # layer 2
        return out

model = SimpleNet()
x = torch.randn(1, 4)
prediction = model(x)  # triggers forward pass
```

> Forward propagation is **inference** — no weights are updated during this step.

---

---

## DL-028: What is max pooling?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-029: What is padding?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-030: What is parameter sharing?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-031: What is pooling?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-032: What is sequence-to-sequence learning?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Sequence-to-sequence (Seq2Seq)** learning maps an **input sequence** of variable length to an **output sequence** of variable length.

**Architecture:**
- **Encoder RNN:** reads input sequence, produces context vector `c`
- **Decoder RNN:** uses context vector to generate output sequence token-by-token

```python
import torch.nn as nn

class Encoder(nn.Module):
    def __init__(self, vocab_size, embed_dim, hidden_size):
        super().__init__()
        self.embedding = nn.Embedding(vocab_size, embed_dim)
        self.rnn = nn.LSTM(embed_dim, hidden_size, batch_first=True)
    
    def forward(self, x):
        x = self.embedding(x)
        output, (hn, cn) = self.rnn(x)
        return hn, cn  # context = final hidden state

class Decoder(nn.Module):
    def __init__(self, vocab_size, embed_dim, hidden_size):
        super().__init__()
        self.embedding = nn.Embedding(vocab_size, embed_dim)
        self.rnn = nn.LSTM(embed_dim, hidden_size, batch_first=True)
        self.fc = nn.Linear(hidden_size, vocab_size)
    
    def forward(self, x, hidden, cell):
        x = self.embedding(x.unsqueeze(1))
        output, (hidden, cell) = self.rnn(x, (hidden, cell))
        prediction = self.fc(output.squeeze(1))
        return prediction, hidden, cell
```

**Applications:** Machine translation, summarization, chatbots, speech-to-text.

---

---

## DL-033: What is sigmoid?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Sigmoid** squashes input to a range of **(0, 1)**, making it ideal for binary probability outputs.

**Formula:**
```
σ(x) = 1 / (1 + e⁻ˣ)
```

**Derivative:**
```
σ'(x) = σ(x) · (1 - σ(x))    [max value: 0.25 at x=0]
```

```python
import torch
import torch.nn.functional as F

x = torch.tensor([-3.0, 0.0, 3.0])
print(F.sigmoid(x))  # tensor([0.0474, 0.5000, 0.9526])
```

**Use cases:**
- Output layer for **binary classification**
- Gates in LSTMs (forget, input, output gates)

**Disadvantages:**
- **Vanishing gradients** — derivative approaches 0 for large |x|
- **Not zero-centered** — outputs always positive → slow convergence
- Computationally expensive (exp operation)

> **Rarely used in hidden layers today** — ReLU is preferred.

---

---

## DL-034: What is stride?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-035: What is tanh?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Tanh** (Hyperbolic Tangent) squashes input to **(-1, 1)**, making it zero-centered unlike sigmoid.

**Formula:**
```
tanh(x) = (eˣ - e⁻ˣ) / (eˣ + e⁻ˣ) = 2σ(2x) - 1
```

**Derivative:**
```
tanh'(x) = 1 - tanh²(x)    [max value: 1 at x=0]
```

```python
import torch

x = torch.tensor([-3.0, 0.0, 3.0])
print(torch.tanh(x))  # tensor([-0.9951,  0.0000,  0.9951])
```

**Advantages over sigmoid:**
- **Zero-centered** → stronger gradients, faster convergence
- Larger gradient range (max 1 vs 0.25)

**Disadvantages:**
- Still suffers from **vanishing gradients** at extremes
- Computationally similar cost to sigmoid

**Use cases:**
- Hidden layers in shallow networks (LSTMs use tanh for cell state output)
- Preferred over sigmoid when zero-centering matters

---

---

## DL-036: What is the exploding gradient problem?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

The **exploding gradient problem** occurs when gradients grow **exponentially** during BPTT, causing extremely large weight updates and unstable training.

**Cause:**
- Same repeated multiplication, but eigenvalues > 1
- `∏|Wₕ| > 1 for T steps → gradient → ∞`

**Symptoms in RNNs:**
- Loss becomes NaN
- Weights blow up
- Model collapses immediately at start of training

**Standard solution — Gradient Clipping:**

```python
import torch

optimizer = torch.optim.Adam(rnn.parameters(), lr=0.001)

for x_seq, y_seq in dataloader:
    output, _ = rnn(x_seq)
    loss = criterion(output, y_seq)
    
    optimizer.zero_grad()
    loss.backward()
    
    # Clip gradients: scale down if norm exceeds threshold
    torch.nn.utils.clip_grad_norm_(rnn.parameters(), max_norm=1.0)
    
    optimizer.step()
```

**How clipping works:**
```
if ||g|| > max_norm:
    g = g * (max_norm / ||g||)
```

> Gradient clipping is **standard practice** for all RNN training.

---

---

## DL-037: What is the vanishing gradient problem?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

The **vanishing gradient problem** occurs when gradients become extremely small as they propagate back through many layers, causing early layers to learn very slowly or not at all.

**Cause:**
- Activation functions like sigmoid/tanh squash derivatives to small values (max 0.25 for sigmoid)
- Chained multiplication via backprop: `∂L/∂W₁ = δₙ · Wₙ · ... · W₂ · δ₁`
- Products of many small values → gradient ≈ 0

**Mathematical example:**
```
If each layer's gradient is 0.25:
10 layers deep: 0.25^10 ≈ 0.000001 → effectively zero
```

**Symptoms:**
- Early layers barely update
- Training loss plateaus early
- Deep networks perform similar to shallow ones

**Solutions:**

```python
# 1. Use ReLU (gradient = 1 for x > 0)
nn.ReLU()

# 2. Batch Normalization
nn.BatchNorm1d(128)

# 3. Residual connections (skip connections)
class ResidualBlock(nn.Module):
    def forward(self, x):
        return x + self.layers(x)  # gradient flows directly through +

# 4. Proper weight initialization (Xavier/He)
nn.init.kaiming_normal_(layer.weight)

# 5. Use LSTM/GRU for sequences (gating mechanisms)
nn.LSTM(input_size, hidden_size)
```

---

---

## DL-038: What is transfer learning in CNNs?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

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

---

## DL-039: What is weight initialization?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** HIGH

**Weight initialization** is the process of setting initial values for network weights before training begins. Bad initialization can cause vanishing/exploding gradients and slow convergence.

**Why it matters:**
- All zeros → all neurons compute same gradient → no learning (symmetry breaking)
- All large values → exploding gradients
- All small values → vanishing gradients

**Common strategies:**

```python
import torch.nn as nn

layer = nn.Linear(256, 128)

# 1. Xavier (Glorot) initialization — for Sigmoid/Tanh
# Var(W) = 2 / (fan_in + fan_out)
nn.init.xavier_uniform_(layer.weight)
nn.init.xavier_normal_(layer.weight)

# 2. He (Kaiming) initialization — for ReLU
# Var(W) = 2 / fan_in
nn.init.kaiming_uniform_(layer.weight, nonlinearity='relu')
nn.init.kaiming_normal_(layer.weight, nonlinearity='relu')

# 3. Orthogonal initialization — for RNNs
nn.init.orthogonal_(layer.weight)

# 4. Zero bias initialization (standard)
nn.init.zeros_(layer.bias)
```

**Guidelines:**
| Activation | Recommended Initialization |
|-----------|---------------------------|
| Sigmoid / Tanh | Xavier (Glorot) |
| ReLU / Leaky ReLU | He (Kaiming) |
| SELU | LeCun Normal |
| RNN/LSTM | Orthogonal |

---

## DL-040: What applications commonly use RNNs?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** MEDIUM

RNNs are well-suited for any task involving **ordered, sequential data**.

| Application | Input | Output | Architecture |
|-------------|-------|--------|--------------|
| **Language Modeling** | Previous words | Next word probability | Many-to-many |
| **Machine Translation** | Source sentence | Target sentence | Seq2Seq |
| **Sentiment Analysis** | Text | Positive/Negative | Many-to-one |
| **Named Entity Recognition** | Words | Entity tags | Many-to-many |
| **Speech Recognition** | Audio frames | Text transcript | Seq2Seq |
| **Text Generation** | Seed text | Generated text | One-to-many |
| **Time Series Forecasting** | Past values | Future values | Many-to-one |
| **Music Generation** | Note sequence | Next notes | Many-to-many |
| **Video Captioning** | Video frames | Caption | Many-to-one |
| **Anomaly Detection** | Sensor readings | Anomaly score | Many-to-one |

```python
# Example: Time series forecasting with RNN
import torch.nn as nn

class TimeSeriesRNN(nn.Module):
    def __init__(self, input_size, hidden_size, num_layers, forecast_horizon):
        super().__init__()
        self.lstm = nn.LSTM(input_size, hidden_size, num_layers, 
                            batch_first=True, dropout=0.2)
        self.fc = nn.Linear(hidden_size, forecast_horizon)
    
    def forward(self, x):
        out, (hn, _) = self.lstm(x)
        return self.fc(hn[-1])  # predict next N steps
```

> **Note:** For many of these tasks, **Transformers** have largely replaced RNNs due to parallelism and better long-range modeling. However, RNNs are still used in resource-constrained or real-time streaming scenarios.

---

## DL-041: Why are CNNs effective for images?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** MEDIUM

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

---

## DL-042: Why are RNNs useful for sequential data?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** MEDIUM

RNNs are useful for sequential data because they can model **temporal dependencies** — relationships between elements at different time steps — which feedforward networks cannot.

**Why standard MLPs fail for sequences:**
- Fixed input size — sequences have variable length
- No memory — each input processed independently
- Cannot capture ordering — word order matters in language

**What RNNs provide:**
- **Variable-length input** — process one step at a time
- **Memory across time** — hidden state carries context
- **Parameter sharing** — same weights applied at every step (efficient)
- **Order sensitivity** — "dog bites man" ≠ "man bites dog"

**Applications:**
| Task | Input | Output |
|------|-------|--------|
| Sentiment analysis | Sentence | Sentiment label |
| Time series forecasting | Past values | Future value |
| Speech recognition | Audio frames | Text |
| Language modeling | Words | Next word probability |
| Machine translation | Source sentence | Target sentence |

---

---

## DL-043: Why are non-linear activation functions required?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** MEDIUM

Without non-linear activation functions, a neural network — **no matter how many layers** — collapses into a single linear transformation.

**Mathematical proof:**
```
Layer 1: z₁ = W₁x + b₁
Layer 2: z₂ = W₂z₁ + b₂ = W₂(W₁x + b₁) + b₂ = (W₂W₁)x + (W₂b₁ + b₂)
         ↳ This is just: z₂ = W'x + b'  — still linear!
```

**Why non-linearity matters:**
- Enables the network to learn **complex, non-linear decision boundaries**
- Allows approximation of any function (Universal Approximation Theorem)
- Enables hierarchical feature learning (edges → shapes → objects in vision)

```python
# Without activation: stacked linear layers = one linear layer
import torch.nn as nn

# These two are equivalent (no non-linearity):
bad_model = nn.Sequential(nn.Linear(10, 64), nn.Linear(64, 1))

# This one can learn non-linear functions:
good_model = nn.Sequential(
    nn.Linear(10, 64), nn.ReLU(),
    nn.Linear(64, 1)
)
```

---

---

## DL-044: Why do vanilla RNNs suffer from vanishing gradients?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** MEDIUM

Vanilla RNNs suffer from vanishing gradients because during BPTT, gradients are multiplied by the **weight matrix** at each time step — and if these values are less than 1, gradients shrink exponentially.

**Mathematical cause:**
```
∂hₜ/∂h₁ = ∏ᵢ₌₁ᵗ⁻¹ ∂hᵢ₊₁/∂hᵢ = ∏ᵢ₌₁ᵗ⁻¹ (Wₕᵀ · diag(tanh'(hᵢ)))

If |eigenvalue of Wₕ| < 1 and |tanh'| < 1:
  product → 0 exponentially fast as t grows
```

**Consequence:**
- Gradient of loss w.r.t. early hidden states ≈ 0
- Network cannot learn **long-range dependencies**
- For sequence of length 100: the 1st word barely affects the gradient

**Practical symptom:**
```python
# RNN "forgets" early tokens in long sequences
sentence = "The cat that was chased by the dog ___ happy"
# Vanilla RNN struggles to connect "cat" to "was"
```

**Solutions:**
- LSTM / GRU — gating mechanisms maintain gradient flow
- Gradient clipping — limit exploding case
- Careful weight initialization

---

---

## DL-045: What are the limitations of vanilla RNNs?

**Domain:** Topic 40: Neural Networks and Backpropagation &nbsp;|&nbsp; **Priority:** LOWER

Vanilla (simple) RNNs have several critical limitations:

**1. Vanishing Gradient / Long-Term Dependencies:**
- Cannot remember information from many steps ago
- Effective memory is short (~10-20 steps)

**2. Exploding Gradients:**
- Requires gradient clipping to stabilize

**3. Sequential computation:**
- Cannot parallelize across time steps
- Slow to train on long sequences

**4. Fixed hidden state size:**
- All history compressed into one vector
- Information bottleneck for complex sequences

**5. No explicit forgetting mechanism:**
- No way to selectively remember or forget — all history blended equally

**6. Sensitive to hyperparameters:**
- Learning rate, initialization very sensitive

**Summary Table:**
| Limitation | Impact | Solution |
|-----------|--------|----------|
| Vanishing gradients | Can't learn long-range deps | LSTM, GRU |
| Exploding gradients | Unstable training | Gradient clipping |
| Sequential computation | Slow training | Transformers |
| Information bottleneck | Long sequences compress poorly | Attention mechanisms |

---

---

## DL-046: What are GRU advantages?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** HIGH

1. **Higher Efficiency:** Requires 25% fewer parameters and fewer tensor operations per sequence step.
2. **Faster Convergence:** Often reaches target validation loss faster than LSTM due to fewer optimization variables.
3. **Strong Generalization on Small Datasets:** Lower risk of overfitting when sequence data is scarce compared to more heavily parameterized LSTMs.
4. **Competitive Empirical Accuracy:** Benchmarks consistently show GRU achieves comparable performance to LSTM across machine translation, text classification, and time series tasks.

---

---

## DL-047: What are update and reset gates?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** HIGH

GRUs regulate information flow using two specific gating vectors:

### 1. Reset Gate ($r_t$)
Controls **how much of the previous hidden state to forget** when computing new candidate representations:
$$r_t = \sigma(W_r \cdot [h_{t-1}, x_t] + b_r)$$
- If $r_t \approx 0$, the unit ignores past hidden state $h_{t-1}$ and computes candidates using only the current input $x_t$ (acting like a fresh start).

### 2. Update Gate ($z_t$)
Controls **how much past information is retained versus replaced** with the new candidate state:
$$z_t = \sigma(W_z \cdot [h_{t-1}, x_t] + b_z)$$

The candidate state $\tilde{h}_t$ and updated hidden state $h_t$ are computed as:
$$\tilde{h}_t = \tanh(W_h \cdot [r_t \odot h_{t-1}, x_t] + b_h)$$
$$h_t = (1 - z_t) \odot h_{t-1} + z_t \odot \tilde{h}_t$$

The update gate effectively couples the roles of the LSTM's forget gate and input gate into a single convex combination ($1 - z_t$ and $z_t$).

---

---

## DL-048: What is a BiLSTM?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** HIGH

A **Bidirectional Long Short-Term Memory (BiLSTM)** network is a recurrent architecture that processes sequence data in both directions simultaneously:
1. **Forward LSTM:** Reads sequence from start to finish ($x_1 \to x_2 \to \dots \to x_T$).
2. **Backward LSTM:** Reads sequence from finish to start ($x_T \to x_{T-1} \to \dots \to x_1$).

At each time step $t$, the hidden states from both directions are concatenated (or combined):
$$h_t = [\overrightarrow{h}_t \,;\, \overleftarrow{h}_t]$$
This allows the representation of each token to incorporate both past context and future context.

```
                  Backward LSTM:   h_back(1) ◄─── h_back(2) ◄─── h_back(3) ◄─── h_back(T)
                                        │              │              │              │
                                      [Concat]       [Concat]       [Concat]       [Concat]
                                        │              │              │              │
                  Forward LSTM:    h_fwd(1)  ───► h_fwd(2)  ───► h_fwd(3)  ───► h_fwd(T)
                                        ▲              ▲              ▲              ▲
                                        │              │              │              │
                  Input Sequence:      x_1            x_2            x_3            x_T
```

**PyTorch Implementation:**
```python
import torch
import torch.nn as nn

bilstm = nn.LSTM(
    input_size=128,
    hidden_size=256,
    num_layers=1,
    batch_first=True,
    bidirectional=True  # Enables bidirectional processing
)

x = torch.randn(32, 20, 128)  # (batch, seq_len, features)
output, (h_n, c_n) = bilstm(x)

# Hidden dimension is doubled due to concatenation [forward; backward]
print("Output shape:", output.shape)  # torch.Size([32, 20, 512])
print("Final hidden state:", h_n.shape)  # torch.Size([2, 32, 256]) -> [num_directions, batch, hidden]
```

---

---

## DL-049: What is a GRU?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** HIGH

A **Gated Recurrent Unit (GRU)** is a simplified variant of the LSTM architecture proposed by Kyunghyun Cho et al. in 2014. 

Like LSTM, GRU mitigates the vanishing gradient problem in recurrent networks, but achieves this with a streamlined architecture featuring:
- **No separate cell state:** Uses only a single hidden state vector ($h_t$).
- **Only two gates:** An **Update Gate ($z_t$)** and a **Reset Gate ($r_t$)**.
- Fewer parameters and faster computational speed than an LSTM while achieving comparable empirical performance.

```
                    Hidden State h(t-1) ────────┬─────────────────────────[ x ]─────────────(+)────► h(t)
                                                │                           ▲                ▲
                                                │                  (1 - z_t)│                │ z_t
                                                │                           │         ┌──────┴──────┐
                                                │                     Update Gate     │  Candidate  │
                                                │                     ┌─────┴─────┐   │   h~_t      │
                                                │                     │  σ (z_t)  │   │  (tanh)     │
                                                │                     └───────────┘   └──────┬──────┘
                                                │                                            │
                                                │            Reset Gate                      │
                                                │            ┌─────┴─────┐                   │
                                                └───────────►│  σ (r_t)  ├───[ x ]───────────┘
                                                             └───────────┘     ▲
                                                                               │
                    Input x(t) ────────────────────────────────────────────────┴──────────────────────
```

**PyTorch Implementation:**
```python
import torch
import torch.nn as nn

gru = nn.GRU(
    input_size=64,
    hidden_size=128,
    num_layers=2,
    batch_first=True
)

x = torch.randn(16, 50, 64)
output, h_n = gru(x)

print("Output shape:", output.shape)  # torch.Size([16, 50, 128])
print("Final hidden state:", h_n.shape)  # torch.Size([2, 16, 128])
```

---

---

## DL-050: What is a cell state?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** HIGH

The **cell state** ($C_t$) is the internal long-term memory backbone of an LSTM unit. It acts like a persistent highway running through the sequence chain, with only minimal linear interactions.

**Key characteristics:**
- **Additive Updates:** While standard hidden states are recomputed at every step via non-linear activations ($\tanh(W x + U h)$), the cell state is updated via linear addition:
  $$C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t$$
- **Protected Gradient Path:** Backpropagation along $C_t$ involves additions and gate multiplications without squashing activations, preventing gradient vanishing over extended horizons.
- **Segregated Memory:** Separates persistent background information from short-term context ($h_t$).

---

---

## DL-051: What is an LSTM?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** HIGH

A **Long Short-Term Memory (LSTM)** network is a specialized recurrent neural network (RNN) architecture designed to capture long-term dependencies in sequential data while mitigating the vanishing gradient problem.

Introduced by Sepp Hochreiter and Jürgen Schmidhuber in 1997, LSTMs replace standard recurrent hidden units with dedicated **memory cells** regulated by **three gating mechanisms**:
1. **Forget Gate ($f_t$):** Controls what past information to discard from the cell state.
2. **Input Gate ($i_t$):** Controls what new candidate information to write into the cell state.
3. **Output Gate ($o_t$):** Controls what information from the cell state to emit as the hidden state output.

```
                    Cell State C(t-1) ───────────[ x ]────────────────(+)─────────► C(t)
                                                   ▲                   ▲
                                                   │                   │
                                            Forget │            Input  │ Candidate
                                             Gate  │             Gate  │  State
                                            ┌──────┴──────┐    ┌───────┴──────┐
                    Hidden State h(t-1) ───►│  σ (f_t)    │    │  σ (i_t)     │
                                            └─────────────┘    └──────────────┘
                                                                       │
                                                               ┌───────┴──────┐
                                                               │  tanh (C~_t) │
                                                               └──────────────┘
                                                                       │
                                            ┌─────────────┐            │
                                            │  σ (o_t)    ├──────────[ x ]────────► h(t)
                                            └──────┬──────┘            ▲
                                            Output │            tanh   │
                                             Gate  └───────────────────┘
                    Input x(t) ────────────────────┘
```

**PyTorch Implementation:**
```python
import torch
import torch.nn as nn

# Define LSTM model
lstm = nn.LSTM(
    input_size=64,     # feature dimension per token/step
    hidden_size=128,   # hidden state / cell dimension
    num_layers=2,      # stacked 2 layers
    batch_first=True   # batch shape: (batch_size, seq_len, features)
)

# Dummy sequence: batch=16, seq_len=50, input_dim=64
x = torch.randn(16, 50, 64)
output, (h_n, c_n) = lstm(x)

print("Output shape:", output.shape)  # torch.Size([16, 50, 128])
print("Final hidden state:", h_n.shape)  # torch.Size([2, 16, 128])
print("Final cell state:", c_n.shape)    # torch.Size([2, 16, 128])
```

---

---

## DL-052: What is the difference between hidden state and cell state?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** HIGH

| Dimension | Cell State ($C_t$) | Hidden State ($h_t$) |
|:---|:---|:---|
| **Role** | Long-term memory storage | Short-term memory & current output |
| **Visibility** | Internal to the LSTM unit; not passed to external dense/output layers | Exposed as output to downstream layers, higher LSTM stacks, and classification heads |
| **Transformations** | Linear interactions (element-wise addition and gating) | Non-linear squashed representation ($h_t = o_t \odot \tanh(C_t)$) |
| **Gradient Flow** | Highway for backpropagation; prevents vanishing gradients | Standard recurrent feedback path |
| **Analogy** | Hard drive / internal database | Working memory / RAM / screen output |

---

---

## DL-053: What is the forget gate?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** HIGH

The **forget gate** ($f_t$) determines what proportion of the previous cell state ($C_{t-1}$) should be retained or erased.

**Mathematical Formulation:**
$$f_t = \sigma(W_f \cdot [h_{t-1}, x_t] + b_f)$$

Where:
- $\sigma$ is the sigmoid activation function, outputting values between $0$ and $1$.
- $0$: Completely drop / discard this component of the past memory.
- $1$: Completely keep / preserve this component of the past memory.
- $W_f$, $b_f$ are learnable weights and biases.

**Intuitive Example:**
In language modeling, when the subject switches from singular ("The doctor ...") to plural ("... and the nurses"), the forget gate outputs values close to $0$ for the singular grammatical gender/number flags, clearing out obsolete state.

---

---

## DL-054: What is the input gate?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** HIGH

The **input gate** ($i_t$) determines which new information from the current input ($x_t$) and previous hidden state ($h_{t-1}$) should be stored into the updated cell state.

It operates in two coordinated phases:
1. **Input Gate Activation ($i_t$):** A sigmoid layer deciding which dimensions to update (values between 0 and 1):
   $$i_t = \sigma(W_i \cdot [h_{t-1}, x_t] + b_i)$$
2. **Candidate Vector ($\tilde{C}_t$):** A $\tanh$ layer creating a vector of new candidate values that could be added to the state:
   $$\tilde{C}_t = \tanh(W_c \cdot [h_{t-1}, x_t] + b_c)$$

The new memory is combined with the preserved memory:
$$C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t$$

---

---

## DL-055: What is the output gate?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** HIGH

The **output gate** ($o_t$) determines what information from the current cell state ($C_t$) should be emitted as the observable hidden state ($h_t$) to downstream layers or time steps.

**Mathematical Formulation:**
1. **Gate Activation:**
   $$o_t = \sigma(W_o \cdot [h_{t-1}, x_t] + b_o)$$
2. **Filtered Hidden State Output:**
   $$h_t = o_t \odot \tanh(C_t)$$

**Role:**
The cell state contains full long-term historical records, but downstream tasks (such as predicting the next immediate word) only require a focused subset. The output gate filters out irrelevant internal memory so that $h_t$ exposes only context-relevant signals.

---

---

## DL-056: How can dropout be applied to recurrent networks?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

Applying naive dropout to recurrent state transitions ($h_{t-1} \to h_t$) destroys memory retention because random zeroing cascades over time steps, effectively wiping out the internal memory.

Modern recurrent architectures apply dropout via two primary techniques:

### 1. Inter-Layer Dropout (Standard PyTorch Approach)
Dropout is applied only **between vertical recurrent layers** ($h_t^{(l)} \to x_t^{(l+1)}$), **never** along the horizontal recurrent connections across time ($t-1 \to t$).
```python
# PyTorch builtin applies dropout between recurrent layers only
lstm = nn.LSTM(input_size=100, hidden_size=200, num_layers=3, dropout=0.5)
```

### 2. Variational Recurrent Dropout (Gal & Ghahramani)
If dropout is needed on the recurrent connections ($h_{t-1} \to h_t$):
- Sample a random dropout mask **once** at time $t=0$.
- Reuse the **exact same dropout mask** across all time steps $t=1, 2, \dots, T$ for that sequence.
- This prevents the cumulative memory destruction caused by sampling new masks at every single time step.

---

## DL-057: How do you choose between GRU and LSTM?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

| Scenario / Criterion | Preferred Architecture | Rationale |
|:---|:---:|:---|
| **Small to Moderate Dataset** | **GRU** | Fewer parameters reduce the likelihood of overfitting |
| **Constrained Compute / Edge Devices** | **GRU** | Lower memory footprint and faster inference speed |
| **Fast Prototyping & Iteration** | **GRU** | Trains faster with fewer hyperparameter adjustments |
| **Complex Sequences with Ultra-Long Dependencies** | **LSTM** | Dedicated cell state provides better information retention |
| **Large-Scale Data & Sufficient Compute** | **LSTM** | Greater expressive capacity can exploit large datasets |
| **Language Modeling with Counting/Tracking** | **LSTM** | Separate output gate allows hidden state to selectively emit specific features |

**Practical Rule of Thumb:**
Start with **GRU** as a baseline for quick training. If the model suffers from underfitting or struggles with long-range dependencies, switch to **LSTM**.

---

## DL-058: How does BiLSTM compare with unidirectional LSTM?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

| Feature | Unidirectional LSTM | Bidirectional LSTM (BiLSTM) |
|:---|:---|:---|
| **Context Window** | Past only ($t \le \tau$) | Full context: Past and Future ($1 \le t \le T$) |
| **Output Dimension** | $d_h$ | $2 \times d_h$ (when concatenated) |
| **Parameters** | $1 \times$ standard LSTM parameters | Exactly $2 \times$ parameters (two independent LSTM nets) |
| **Inference Latency** | Can process streaming inputs token-by-token | Requires entire sequence before backward pass can execute |
| **Causal Forecasting** | Suitable (strict causal masking) | Unsuitable (data leakage of future observations) |
| **Classification / NER** | Good | Superior (state-of-the-art for RNN-based NLP tasks) |

---

## DL-059: How does GRU differ from LSTM?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

1. **State Count:**
   - LSTM maintains two distinct state vectors: cell state $C_t$ and hidden state $h_t$.
   - GRU maintains only one state vector: hidden state $h_t$.
2. **Gate Count:**
   - LSTM uses 3 gates: Forget ($f_t$), Input ($i_t$), and Output ($o_t$).
   - GRU uses 2 gates: Reset ($r_t$) and Update ($z_t$).
3. **Coupled Forget & Input:**
   - In LSTM, forget and input gates are independent: $C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t$.
   - In GRU, they are strictly coupled: $h_t = (1 - z_t) \odot h_{t-1} + z_t \odot \tilde{h}_t$.
4. **No Output Gate:**
   - In GRU, the entire calculated hidden state is visible to subsequent layers without an output filtering gate.

---

---

## DL-060: How does LSTM address vanishing gradients?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

LSTM solves vanishing gradients primarily through the **Constant Error Carousel (CEC)** and additive cell updates.

**Mechanisms:**
1. **Additive Error Propagation:**
   $$\frac{\partial C_t}{\partial C_{t-1}} = f_t$$
   When the forget gate $f_t \approx 1$, the gradient of error flowing backward along the cell state is:
   $$\frac{\partial \mathcal{L}}{\partial C_{t-1}} = \frac{\partial \mathcal{L}}{\partial C_t} \cdot f_t$$
   Because this is direct multiplication by $f_t$ (rather than repeated non-linear matrix products $W_{hh}^T \cdot \text{diag}(1 - \tanh^2)$), the gradient does not automatically vanish over time steps.
2. **Unimpeded Gradient Flow:** The error can travel backwards across hundreds of steps intact as long as the forget gates stay near 1.
3. **Controlled Learning:** The gates themselves are learnable functions of input and context, allowing the network to explicitly decide when to maintain gradient flow and when to cut it off.

---

---

## DL-061: How does LSTM compare with GRU?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

| Attribute | LSTM | GRU (Gated Recurrent Unit) |
|:---|:---|:---|
| **Number of Gates** | 3 (Forget, Input, Output) | 2 (Reset, Update) |
| **State Vectors** | 2 separate states ($C_t, h_t$) | 1 unified state ($h_t$) |
| **Parameter Count** | Higher ($4 \times$ gate parameters) | Lower (~25% fewer parameters, $3 \times$ gates) |
| **Training Speed** | Slower per epoch | Faster per epoch due to fewer matrix multiplications |
| **Data Efficiency** | Excels on larger, longer, or more complex sequence datasets | Excels on smaller datasets; less prone to overfitting |
| **Control Granularity** | Fine-grained (separate memory storage and output gating) | Coarse-grained (direct blend between old and new state) |

---

## DL-062: How does LSTM compare with vanilla RNN?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

| Feature | Vanilla RNN | LSTM |
|:---|:---|:---|
| **Memory Mechanism** | Single recurrent hidden state ($h_t$) | Dual states: Cell state ($C_t$) + Hidden state ($h_t$) |
| **Gating System** | None | 3 gates (Forget, Input, Output) |
| **Gradient Propagation** | Vanishes or explodes quickly; limited to ~5–10 steps | Stable error carousel; scales to hundreds of steps |
| **Parameter Count** | $1 \times (d_h \cdot d_{in} + d_h^2 + d_h)$ | $4 \times (d_h \cdot d_{in} + d_h^2 + d_h)$ |
| **Computational Speed** | Fast per step | ~4x slower per step |
| **Long-Term Context** | Extremely poor | Strong |

---

---

## DL-063: How does stacking recurrent layers increase capacity?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

Stacking recurrent layers increases representation capacity through **hierarchical temporal abstraction**:

1. **Depth Creates Non-Linear Feature Hierarchies:** Just as deep CNNs learn low-level edges in early layers and high-level concepts in deep layers, deep RNNs create functional hierarchies over sequential signals.
   - **Layer 1:** Captures low-level token/character transitions, phonemes, or local spikes.
   - **Layer 2:** Captures syntactic groupings, phrases, or short trends.
   - **Layer 3+:** Captures semantic meaning, overall intent, topic, or long-term seasonality.
2. **Multi-Scale Temporal Dynamics:** Higher layers often naturally operate on slower, broader temporal scales than lower layers.
3. **Exponential Hypothesis Space:** Deep models can represent certain mathematical functions with exponentially fewer parameters than shallow (single-layer) wide models.

---

---

## DL-064: What does the backward LSTM capture?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

The **backward LSTM** computes hidden states moving in reverse chronological order from $t=T$ down to $t=1$:
$$\overleftarrow{h}_t = \text{LSTM}_{bwd}(x_t, \overleftarrow{h}_{t+1})$$

**What it captures:**
- **Future Context:** Downstream tokens, outcomes, and concluding remarks occurring after time $t$.
- **Right-to-Left Dependencies:** Clues provided by subsequent objects, prepositions, or sentence endings.
- **Anticipatory Signals:** Resolving forward references (cataphora) and clarifying ambiguous entities early in a sequence.

---

---

## DL-065: What does the forward LSTM capture?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

The **forward LSTM** computes hidden states moving chronologically from $t=1$ to $t=T$:
$$\overrightarrow{h}_t = \text{LSTM}_{fwd}(x_t, \overrightarrow{h}_{t-1})$$

**What it captures:**
- **Historical Context:** Preceding tokens, previous events, and causal trends leading up to time $t$.
- **Syntactic Structure from Left to Right:** Subject-verb agreements established earlier in a sentence.
- **Cumulative Trajectory:** The running sequence summary accumulated from the beginning of the input.

---

---

## DL-066: When is BiLSTM unsuitable?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

BiLSTM is fundamentally unsuitable in situations where future information cannot be accessed at runtime:

1. **Causal Real-Time Forecasting:** Stock price prediction, real-time sensor monitoring, or equipment failure prediction where future timestamps $t+1, t+2$ do not yet exist.
2. **Autoregressive Text Generation:** Next-token generation (such as language models, chat assistants, or auto-complete) where tokens are generated sequentially one by one.
3. **Low-Latency Streaming Speech Recognition:** Real-time speech transcription where waiting for the user to finish speaking introduces unacceptable latency.
4. **Strictly Causal Tasks:** Any task requiring strict adherence to the arrow of time without sequence buffering.

---

---

## DL-067: When might GRU train faster than LSTM?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

GRU trains noticeably faster than LSTM under the following conditions:
1. **Compute-Bound Training:** With 25% fewer matrix multiplications per time step, forward and backward passes execute in fewer FLOPs.
2. **Resource-Constrained Environments:** Embedded systems, mobile processors, or single-GPU setups where smaller memory footprints yield higher GPU batch throughput.
3. **Long Sequence Batches:** Fewer tensor allocations and intermediate cache buffers allow larger batch sizes, accelerating overall convergence time.
4. **Fast Prototyping:** Quicker feedback loops on experimental models where the expressive advantage of LSTM is negligible.

---

---

## DL-068: When should you use LSTM?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

LSTMs are recommended in scenarios characterized by:
1. **Sequential Data with Long-Range Dependencies:** Text, audio streams, sensor telemetry, and complex financial time series where context from 50–200 steps ago dictates current meaning.
2. **Streaming or Low-Latency Inference:** Applications requiring single-token-at-a-time streaming updates on edge hardware without keeping an entire attention context matrix in memory.
3. **Small to Medium Datasets:** When training large Transformer models from scratch is impractical due to lack of massive datasets or GPU compute.
4. **Time Series Forecasting:** Sensor predictive maintenance, IoT telemetry, stock volatility modeling where sequential recurrent priors provide effective inductive bias.

---

---

## DL-069: Why does GRU have fewer parameters?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

A standard recurrent layer maps input size $d_{in}$ and hidden size $d_h$.
- **LSTM requires 4 gate projections:**
  - Forget gate ($f$), Input gate ($i$), Candidate cell ($\tilde{C}$), Output gate ($o$).
  - Total parameters $\approx 4 \times (d_{in} \cdot d_h + d_h^2 + d_h)$
- **GRU requires only 3 projections:**
  - Reset gate ($r$), Update gate ($z$), Candidate hidden state ($\tilde{h}$).
  - Total parameters $\approx 3 \times (d_{in} \cdot d_h + d_h^2 + d_h)$

**Parameter Reduction:**
GRU has exactly **25% fewer parameters** than an equivalent LSTM with the same hidden dimension, lowering memory usage and reducing overfitting risks on small datasets.

---

---

## DL-070: Why does bidirectional processing help?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

In natural language and many real-world sequential signals, the meaning of a word or event often depends heavily on what comes **after** it, not just what preceded it.

**Example 1: Word Sense Disambiguation**
- *"The **bank** of the river was muddy."*
- *"The **bank** approved the home loan."*
A unidirectional model reading the word *"bank"* has no access to *"river"* or *"loan"*, making disambiguation ambiguous. A bidirectional model resolves ambiguity immediately because future tokens inform the current representation.

**Example 2: Named Entity Recognition (NER)**
- *"Apple released the iPhone."* vs *"Apple was sliced into four pieces."*
Having future tokens ("iPhone" vs "sliced") immediately clarifies whether "Apple" is an organization or a fruit.

---

---

## DL-071: Why was LSTM introduced?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** MEDIUM

Standard (vanilla) RNNs suffer severely from the **vanishing and exploding gradient problem** during Backpropagation Through Time (BPTT). 

When backpropagating gradients over numerous time steps ($T$ steps), the repeated multiplication of recurrent weight matrices ($W_{hh}^T$) and derivatives of tanh activation functions causes the gradient to decay exponentially towards zero or explode to infinity:
$$\frac{\partial h_T}{\partial h_t} = \prod_{k=t+1}^T \frac{\partial h_k}{\partial h_{k-1}} = \prod_{k=t+1}^T \text{diag}(1 - \tanh^2(\cdot)) W_{hh}^T$$

**Consequences in Vanilla RNNs:**
- Inability to retain context beyond 5–10 steps.
- Inability to bridge long-distance dependencies (e.g., matching a subject at the start of a paragraph with a verb at the end).
- Instability during parameter updates.

**Why LSTM solves this:**
LSTMs introduce a linear "conveyor belt" known as the **Cell State ($C_t$)**. Because information passes down the cell state with additive updates rather than purely multiplicative transformations, gradients can flow back across hundreds of time steps with minimal decay.

---

---

## DL-072: What are GRU limitations?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** LOWER

1. **Less Fine-Grained Memory Control:** Because it lacks an independent output gate, all internal representations are exposed immediately.
2. **Harder to Control Long Horizons:** On complex, lengthy sequence tasks (>200 time steps) where separate storage and read mechanisms are vital, LSTM often outperforms GRU.
3. **Coupled Updating:** The update gate forces an exact trade-off between keeping past state and adding new state ($1 - z_t$ vs $z_t$), whereas an LSTM can independently forget nothing and add new information simultaneously.
4. **Sequential Nature:** Like LSTM, it cannot be trained in parallel across sequence steps, making it slower than Transformers on massive training datasets.

---

---

## DL-073: What are LSTM limitations?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** LOWER

1. **Sequential Processing Bottleneck:** Recurrent computation is inherently sequential ($h_t$ strictly requires $h_{t-1}$). Training cannot be fully parallelized across time steps, unlike self-attention in Transformers.
2. **Computational and Parameter Overhead:** Each LSTM cell contains 4 linear transformations ($W_f, W_i, W_c, W_o$), requiring $4 \times (d_{in} \cdot d_h + d_h^2 + d_h)$ parameters per layer—4x more than standard RNNs.
3. **Finite Effective Memory Limit:** While theoretically capable of infinite memory, practical LSTMs struggle to retain precise information across sequences exceeding 200–500 steps due to noise accumulation.
4. **Hardware Underutilization:** Cannot saturate modern massively parallel GPU tensor cores as efficiently as matrix multiplication-based Transformer architectures.

---

---

## DL-074: What are the advantages of Deep RNNs?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** LOWER

1. **Hierarchical Sequence Representations:** Learns multi-level abstractions (low-level syntax to high-level semantics).
2. **Higher Model Capacity:** Solves complex sequence modeling problems that cannot be solved by single-layer shallow RNNs regardless of hidden layer width.
3. **Decoupled Temporal & Feature Processing:** Separates time-stepping transitions from deep non-linear feature transformations.
4. **Superior Empirical Performance:** Historically provided the backbone for breakthrough machine translation (e.g., Google's 8-layer GNMT), speech recognition, and complex language modeling.

---

---

## DL-075: What are the disadvantages of Deep RNNs?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** LOWER

1. **High Computational Cost:** Stacking $L$ layers multiplies both forward and backward pass FLOPs linearly by $L$.
2. **Severe Vanishing/Exploding Gradients Across Depth:** In addition to backpropagation through time, gradients must backpropagate through vertical layers, compounding stability issues.
3. **Increased Training Time & Latency:** Cannot compute layer $l+1$ until representations for layer $l$ are available, compounding sequential latency.
4. **Proneness to Overfitting:** More parameters require significantly larger datasets and heavy regularization (dropout, weight decay).

---

---

## DL-076: What is a Deep RNN?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** LOWER

A **Deep Recurrent Neural Network (Deep RNN / Stacked RNN)** is an architecture where multiple recurrent layers (RNN, LSTM, or GRU) are stacked vertically on top of one another.

In a stacked RNN:
- The **first recurrent layer** takes the raw sequence inputs $x_t$ and outputs hidden representations $h_t^{(1)}$.
- The **intermediate layers** take the hidden sequence of the layer below ($h_t^{(l-1)}$) as their sequential input and output $h_t^{(l)}$.
- The **final recurrent layer** produces outputs $h_t^{(L)}$ that are routed to task-specific prediction heads.

```
          Layer 3:  h_1^(3) ───► h_2^(3) ───► h_3^(3) ───► Output / Loss
                      ▲            ▲            ▲
                      │            │            │
          Layer 2:  h_1^(2) ───► h_2^(2) ───► h_3^(2)
                      ▲            ▲            ▲
                      │            │            │
          Layer 1:  h_1^(1) ───► h_2^(1) ───► h_3^(1)
                      ▲            ▲            ▲
                      │            │            │
          Inputs:    x_1          x_2          x_3
```

**PyTorch Implementation:**
```python
import torch
import torch.nn as nn

# Stacked LSTM with 3 layers
stacked_lstm = nn.LSTM(
    input_size=64,
    hidden_size=128,
    num_layers=3,        # 3 stacked recurrent layers
    batch_first=True,
    dropout=0.3          # Dropout applied between layers
)

x = torch.randn(16, 40, 64)
output, (h_n, c_n) = stacked_lstm(x)

print("Output shape:", output.shape)  # torch.Size([16, 40, 128])
print("h_n shape:", h_n.shape)        # torch.Size([3, 16, 128]) -> [num_layers, batch, hidden]
```

---

---

## DL-077: What training challenges occur in Deep RNNs?

**Domain:** Topic 42: RNNs, LSTM, GRU and BiLSTM &nbsp;|&nbsp; **Priority:** LOWER

1. **Dual Gradient Degradation:** Gradients vanish or explode along two axes:
   - **Horizontal axis:** Across sequence time steps $T$ (BPTT).
   - **Vertical axis:** Across depth layers $L$.
2. **Internal Covariate Shift:** Changes in distributions of lower recurrent layers during training continuously destabilize higher layers.
3. **Solutions:**
   - **Residual / Skip Connections:** Adding shortcut connections ($h_t^{(l)} + h_t^{(l-1)}$) allows gradients to flow directly between distant layers.
   - **Gradient Clipping:** Setting `torch.nn.utils.clip_grad_norm_(model.parameters(), max_norm=1.0)` prevents exploding gradients.
   - **Layer Normalization:** Normalizing activations across hidden features stabilizes internal layer dynamics.
   - **LSTM/GRU Units:** Using gated units instead of vanilla RNN layers ensures horizontal gradient stability.

---

---

## DL-078: What are Query, Key, and Value?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

Inspired by information retrieval and database search systems, self-attention maps inputs to three distinct projection spaces:

1. **Query ($Q$):** Represents what the current token is *searching for* or asking about other tokens.
2. **Key ($K$):** Represents what the token *contains* or offers to match incoming queries.
3. **Value ($V$):** The actual substantive information/content that gets retrieved and aggregated if the query matches the key.

For input sequence matrix $X \in \mathbb{R}^{N \times d_{\text{model}}}$:
$$Q = X W_Q, \quad K = X W_K, \quad V = X W_V$$
where $W_Q, W_K \in \mathbb{R}^{d_{\text{model}} \times d_k}$ and $W_V \in \mathbb{R}^{d_{\text{model}} \times d_v}$ are learnable projection weights.

---

---

## DL-079: What is BERT?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

**BERT (Bidirectional Encoder Representations from Transformers)** is an encoder-only Transformer architecture introduced by Devlin et al. (Google, 2018).

**Key Innovations:**
1. **Bidirectional Context:** Unlike autoregressive models that read strictly left-to-right, BERT conditions on both left and right context simultaneously across all layers.
2. **Pretraining Objectives:**
   - **Masked Language Modeling (MLM):** 15% of tokens are randomly masked (`[MASK]`), and the model learns to predict them using bidirectional context.
   - **Next Sentence Prediction (NSP):** Binary classification predicting whether sentence B follows sentence A.
3. **Usage:** Primarily fine-tuned for extractive tasks: classification, NER, question answering, semantic search.

---

---

## DL-080: What is GPT?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

**GPT (Generative Pre-trained Transformer)** is a decoder-only Transformer family developed by OpenAI (Radford et al., 2018–present).

**Key Innovations:**
1. **Autoregressive Causal Modeling:** Pretrained to predict the next token given preceding context:
   $$\mathcal{L}_{GPT} = -\sum_{i=1}^N \log P(x_i \mid x_1, x_2, \dots, x_{i-1})$$
2. **Causal Masking:** Strict lower-triangular attention masks ensure no future leakage.
3. **Emergent Capabilities & Scaling Laws:** Demonstrates that scaling model parameters and pretraining tokens yields zero-shot and few-shot reasoning, translation, and code generation capabilities without task-specific architectural changes.

---

---

## DL-081: What is a Transformer architecture?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

The **Transformer** is a deep learning architecture introduced in the 2017 paper *"Attention Is All You Need"* by Vaswani et al. It completely dispenses with recurrence and convolutions, relying entirely on **self-attention mechanisms** to capture dependencies between input and output tokens.

**Key Components of Transformer Architecture:**
1. **Input & Positional Embeddings:** Token embeddings combined with position vectors.
2. **Encoder Blocks:** Multi-Head Self-Attention followed by Position-wise Feed-Forward Networks (FFN), with residual connections and layer normalization.
3. **Decoder Blocks:** Masked Multi-Head Self-Attention, Cross-Attention (attending to encoder outputs), and FFN layers.
4. **Output Linear & Softmax Head:** Projects decoder states to vocabulary logits.

```
                      OUTPUT PROBABILITIES
                               ▲
                            [Softmax]
                               ▲
                            [Linear]
                               ▲
             ┌─────────────────┴─────────────────┐
             │       DECODER (Nx blocks)         │
             │  ┌─────────────────────────────┐  │
             │  │   Feed-Forward Network      │  │
             │  ├─────────────────────────────┤  │
    ┌────────┼─►│   Cross-Attention (Enc-Dec) │  │
    │        │  ├─────────────────────────────┤  │
    │        │  │  Masked Self-Attention      │  │
    │        │  └─────────────────────────────┘  │
    │        └─────────────────▲─────────────────┘
    │                          │
┌───┴─────────────────┐   [Output Shifted Right]
│ ENCODER (Nx blocks) │
│ ┌─────────────────┐ │
│ │  Feed-Forward   │ │
│ ├─────────────────┤ │
│ │ Self-Attention  │ │
│ └─────────────────┘ │
└──────────▲──────────┘
           │
     [Input Tokens]
```

---

---

## DL-082: What is a decoder?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

The **Decoder** generates output sequences token-by-token (autoregressively) conditioned on the encoder outputs and prior generated tokens.

Each decoder layer contains **three sublayers**:
1. **Masked Multi-Head Self-Attention:** Attends only to previous positions in the output sequence, preventing tokens from attending to future positions during training.
2. **Cross-Attention (Encoder-Decoder Attention):** Queries come from the previous decoder layer, while Keys and Values come from the encoder output. This transfers input knowledge to the generation process.
3. **Position-wise Feed-Forward Network:** Dense transformation layers.

*Decoder-only models:* GPT series, LLaMA, Claude, Mistral (standard for generative tasks).

---

---

## DL-083: What is an encoder?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

In the Transformer architecture, the **Encoder** processes the input sequence and produces rich contextual representations.

An encoder is a stack of $N$ identical blocks (typically 6 to 32 layers). Each block contains:
1. **Multi-Head Self-Attention:** Computes pairwise context across the entire input sequence simultaneously (bidirectional).
2. **Add & Norm (Residual Connection + LayerNorm):** $x + \text{Sublayer}(x)$, facilitating deep gradient flow.
3. **Position-wise Feed-Forward Network:** Two linear layers with non-linear activation ($\text{ReLU}$ or $\text{GELU}$).
4. **Add & Norm:** Second residual connection followed by layer normalization.

*Encoder-only models:* BERT, RoBERTa, DeBERTa (primarily used for classification, NER, and extractive QA).

---

---

## DL-084: What is cross-attention?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Cross-attention** (or Encoder-Decoder Attention) connects the decoder with the encoder representations.

In self-attention, Queries, Keys, and Values all originate from the **same** sequence:
$$Q = X W_Q, \quad K = X W_K, \quad V = X W_V$$

In cross-attention:
- **Queries ($Q$)** originate from the **decoder's previous layer**: $Q = H_{\text{dec}} W_Q$
- **Keys ($K$) and Values ($V$)** originate from the **encoder's final output**: $K = H_{\text{enc}} W_K, \quad V = H_{\text{enc}} W_V$

This enables the decoder to query the source document to decide what information to generate at each output step (e.g., in machine translation or summarization).

---

---

## DL-085: What is fine-tuning?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Fine-tuning** is the adaptation phase where a pretrained base model is specialized for specific downstream tasks or human alignment:

1. **Supervised Fine-Tuning (SFT):** Training on high-quality curated prompt-response pairs to teach instruction-following behavior.
2. **Reinforcement Learning from Human Feedback (RLHF / DPO):** Aligning model outputs with human preferences regarding helpfulness, accuracy, and safety.
3. **Parameter-Efficient Fine-Tuning (PEFT / LoRA):** Freezing base weights and training low-rank adapter matrices ($W = W_0 + B A$), drastically reducing GPU memory requirements during fine-tuning.

---

---

## DL-086: What is layer normalization?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Layer Normalization (LayerNorm)** normalizes the activations across the **feature dimension** (hidden channels) for each individual sample and token independently:

$$\text{LayerNorm}(x) = \frac{x - \mu}{\sqrt{\sigma^2 + \epsilon}} \odot \gamma + \beta$$
where $\mu$ and $\sigma$ are the mean and standard deviation computed across all hidden features $d$ of a single token:
$$\mu = \frac{1}{d}\sum_{i=1}^d x_i, \quad \sigma^2 = \frac{1}{d}\sum_{i=1}^d (x_i - \mu)^2$$

**Why LayerNorm over BatchNorm:**
- **Batch independence:** Does not depend on batch size or other samples in the batch.
- Works seamlessly with variable-length sequences.
- Supports batch size of 1 during autoregressive inference without requiring running statistics.

---

---

## DL-087: What is masked self-attention?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Masked self-attention** (or causal self-attention) prevents each token in a generative decoder from attending to future tokens ($j > i$).

During training, target sequences are passed all at once to enable parallel training. To preserve the autoregressive property (predicting token $t$ using only tokens $1$ to $t-1$), future positions are masked by setting their pre-softmax attention scores to $-\infty$:

$$\text{Attention Matrix} = \begin{bmatrix} 
\text{score}_{11} & -\infty & -\infty \\
\text{score}_{21} & \text{score}_{22} & -\infty \\
\text{score}_{31} & \text{score}_{32} & \text{score}_{33}
\end{bmatrix}$$

Applying $\text{softmax}$ turns $-\infty$ into $0$ probability, ensuring zero attention flow from future positions.

---

---

## DL-088: What is multi-head attention?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

Rather than performing a single attention function with $d_{\text{model}}$-dimensional queries, keys, and values, **Multi-Head Attention (MHA)** projects $Q, K, V$ into $h$ distinct lower-dimensional subspaces, performs attention in parallel across each "head", and concatenates the results:

$$\text{MultiHead}(Q, K, V) = \text{Concat}(\text{head}_1, \dots, \text{head}_h) W_O$$
$$\text{where } \text{head}_i = \text{Attention}(Q W_i^Q, K W_i^K, V W_i^V)$$

**Why Multi-Head Attention helps:**
A single attention head tends to average out multiple semantic relationships. Multi-head attention allows different heads to simultaneously focus on different types of information:
- Head 1: Syntactic subject-verb dependencies.
- Head 2: Coreference resolution (pronouns to nouns).
- Head 3: Positional proximity (immediate neighbors).
- Head 4: Long-distance semantic themes.

---

---

## DL-089: What is pretraining?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Pretraining** is the first phase of the modern two-stage LLM paradigm:
1. **Data:** Unsupervised or self-supervised training on massive web-scale corpora (trillions of tokens consisting of text, books, articles, code).
2. **Objective:** Next-token prediction (causal LM) or masked token recovery (MLM).
3. **Outcome:** The model learns grammar, syntax, world knowledge, reasoning heuristics, common sense, and representation manifolds.
4. **Compute:** Extremely resource-intensive (requires thousands of GPUs for weeks or months).

Pretraining builds the foundational base model upon which specialized behaviors can be added.

---

---

## DL-090: What is scaled dot-product attention?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Scaled Dot-Product Attention** is the core mathematical formulation computing attention outputs:

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{Q K^T}{\sqrt{d_k}}\right) V$$

**Step-by-step breakdown:**
1. **Dot-Product Compatibility ($Q K^T$):** Computes pairwise alignment scores between every query and key token.
2. **Scaling Factor ($\frac{1}{\sqrt{d_k}}$):** Divides by the square root of the key dimension ($d_k$). For large $d_k$, the dot product grows large in magnitude, pushing the softmax function into regions with extremely small gradients. The scaling factor maintains unit variance and gradient stability.
3. **Softmax Normalization:** Converts raw similarity scores into non-negative probability weights that sum to 1 across rows.
4. **Weighted Value Sum ($(\cdot) V$):** Computes a weighted sum of the values based on attention probabilities.

**PyTorch Implementation:**
```python
import torch
import torch.nn.functional as F
import math

def scaled_dot_product_attention(Q, K, V, mask=None):
    d_k = Q.size(-1)
    scores = torch.matmul(Q, K.transpose(-2, -1)) / math.sqrt(d_k)
    
    if mask is not None:
        scores = scores.masked_fill(mask == 0, -1e9)
        
    attn_weights = F.softmax(scores, dim=-1)
    return torch.matmul(attn_weights, V), attn_weights
```

---

---

## DL-091: What is self-attention?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Self-attention** is a mechanism that allows each token in a sequence to attend to, weigh, and aggregate information from **every other token in the same sequence**.

Rather than processing each token in isolation, self-attention computes an attention weight between token $i$ and token $j$, determining how much token $i$ should factor in the representation of token $j$.

**Intuitive Example:**
In the sentence:
> *"The animal didn't cross the street because **it** was too tired."*

When self-attention processes the word **"it"**, it computes attention scores with all other words. The highest attention score is assigned to **"animal"**, enabling the model to dynamically resolve the pronoun reference.

---

---

## DL-092: What is the feed-forward network in a Transformer block?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

Each Transformer encoder and decoder block contains a **Position-wise Feed-Forward Network (FFN)** applied identically and separately to each position:

$$\text{FFN}(x) = \max(0, x W_1 + b_1) W_2 + b_2 = \text{GELU}(x W_1 + b_1) W_2 + b_2$$

**Architecture characteristics:**
- **Dimension Expansion:** Projects hidden dimension $d_{\text{model}}$ to an intermediate dimension $d_{ff}$ (typically $4 \times d_{\text{model}}$), then projects back to $d_{\text{model}}$.
- **Parameter Concentration:** Accounts for roughly two-thirds of the total parameters in a Transformer block.
- **Role:** While self-attention aggregates information across tokens (routing/communication), the FFN processes, synthesizes, and stores factual knowledge within the parameters (computation/storage).

---

---

## DL-093: What is the quadratic complexity problem?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** HIGH

The **quadratic complexity problem** refers to the $\mathcal{O}(N^2)$ scaling of computation time and memory consumption with respect to sequence length $N$ in standard self-attention:

$$\text{Time Complexity} = \mathcal{O}(N^2 \cdot d)$$
$$\text{Memory Complexity} = \mathcal{O}(N^2 + N \cdot d)$$

| Sequence Length ($N$) | Operations ($N^2$) | Relative Cost |
|:---|:---|:---|
| 1,024 | $1.05 \times 10^6$ | $1\times$ |
| 4,096 | $1.68 \times 10^7$ | $16\times$ |
| 16,384 | $2.68 \times 10^8$ | $256\times$ |
| 131,072 | $1.72 \times 10^{10}$ | $16,384\times$ |

This quadratic wall makes naive full attention computationally prohibitive for book-length documents, long audio files, or high-resolution images without architectural innovations.

---

---

## DL-094: How do Transformers differ from LSTMs?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** MEDIUM

| Feature | LSTM | Transformer |
|:---|:---|:---|
| **Core Architecture** | Gated memory cell ($f_t, i_t, o_t, C_t$) | Multi-head self-attention + MLP feed-forward |
| **Sequence Processing** | Step-by-step sequential processing | Entire sequence processed simultaneously |
| **Long-Distance Dependencies**| Limited beyond 200–500 steps | Scales to thousands or millions of tokens |
| **Positional Awareness** | Implicitly encoded via step order | Explicitly injected via positional encodings |
| **Inference Scalability** | Low memory footprint; fixed hidden state | Requires KV cache for efficient autoregression |
| **Empirical State-of-the-Art**| Obsolete for large-scale foundation models | Dominant architecture across NLP, Vision, Audio |

---

---

## DL-095: How do Transformers differ from RNNs?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** MEDIUM

| Dimension | Recurrent Neural Network (RNN) | Transformer |
|:---|:---|:---|
| **Computation Mechanism** | Sequential recurrence ($h_t = f(h_{t-1}, x_t)$) | Parallel self-attention across all tokens |
| **Training Parallelization** | Incompatible; strictly sequential | Fully parallelizable across sequence length |
| **Max Information Path** | $O(N)$ steps across sequence length | $O(1)$ direct connection between any two tokens |
| **Memory Bottleneck** | Fixed-size vector compression causes decay | Full attention matrix retains pairwise context |
| **Computational Complexity** | $O(N \cdot d^2)$ per sequence | $O(N^2 \cdot d)$ per sequence |
| **Hardware Saturation** | Low GPU utilization | High GPU tensor core utilization |

---

---

## DL-096: How do modern architectures handle long contexts?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** MEDIUM

Modern architectures overcome the quadratic attention bottleneck using a combination of algorithmic, mathematical, and hardware optimizations:

1. **FlashAttention (Dao et al.):** An exact attention algorithm that tiles the computation into GPU SRAM blocks, eliminating the need to read/write the full $N \times N$ attention matrix from high-bandwidth memory (HBM). Reduces memory from $\mathcal{O}(N^2)$ to $\mathcal{O}(N)$ and speeds up computation by 2–4x.
2. **Rotary Position Embeddings (RoPE) & YaRN:** Encodes relative position by rotating queries and keys in the complex plane; enables context window extension via frequency interpolation without catastrophic perplexity degradation.
3. **Multi-Query Attention (MQA) & Grouped-Query Attention (GQA):** Shares key and value heads across multiple query heads, slashing KV cache memory footprint by 4x to 8x during autoregressive decoding.
4. **Sparse & Linear Attention:**
   - **Local / Sliding Window Attention:** Tokens attend only to neighbors within a fixed window $W$, achieving $\mathcal{O}(N \cdot W)$ complexity (e.g., Mistral, Longformer).
   - **State Space Models (SSMs) & Hybrid Architectures:** Models like Mamba and RWKV achieve true $\mathcal{O}(N)$ linear time and constant $\mathcal{O}(1)$ inference memory through continuous state-space recurrences.

---

## DL-097: Why are positional encodings needed?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** MEDIUM

Because self-attention operations are **permutation invariant** (i.e., $\text{Attention}(P X) = P \text{Attention}(X)$ where $P$ is a permutation matrix), a Transformer without position signals treats the sequence as an unordered "bag of words":
> *"Dog bites man"* would produce identical representations to *"Man bites dog"*.

Since Transformers contain no recurrent step transitions or convolutions, positional encodings must be injected directly into the input embeddings to provide token order awareness:
$$X_{\text{input}} = \text{Embedding}(X) + \text{PositionalEncoding}$$

**Sinusoidal Positional Encoding (Vaswani et al.):**
$$PE_{(pos, 2i)} = \sin\left(\frac{pos}{10000^{2i/d_{\text{model}}}}\right)$$
$$PE_{(pos, 2i+1)} = \cos\left(\frac{pos}{10000^{2i/d_{\text{model}}}}\right)$$
Allows the model to easily learn relative positions because $PE_{pos + k}$ can be expressed as a linear function of $PE_{pos}$.

---

---

## DL-098: Why is standard attention computationally expensive?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** MEDIUM

Standard scaled dot-product attention requires computing the inner product between every query token and every key token:

$$\text{Attention Matrix} = \text{Softmax}\left(\frac{Q K^T}{\sqrt{d_k}}\right) \in \mathbb{R}^{B \times H \times N \times N}$$

For sequence length $N$:
1. $Q K^T$ requires $N \times N$ matrix multiplications.
2. Storing the $N \times N$ attention weight matrix in GPU memory requires $\mathcal{O}(N^2)$ storage per head and per layer.
3. For long sequences (e.g., $N = 100,000$), $N^2 = 10^{10}$ elements per attention head. At 16-bit precision across 32 layers and 32 heads, this demands hundreds of gigabytes of VRAM just to store intermediate attention maps.

---

---

## DL-099: Why were Transformers introduced?

**Domain:** Topic 43: Attention and Transformer Architecture &nbsp;|&nbsp; **Priority:** MEDIUM

Transformers were introduced to overcome the fundamental bottlenecks of recurrent architectures (RNNs, LSTMs, GRUs) and convolutional sequence models:

1. **Lack of Parallelization in RNNs:** RNNs process sequences token-by-token sequentially ($h_t$ strictly requires $h_{t-1}$). Training cannot be parallelized across the time dimension, preventing full utilization of modern GPU/TPU hardware.
2. **Degradation Over Long Horizons:** Even with gating (LSTM/GRU), RNNs compress all prior information into fixed-size vectors, resulting in information loss over long sequences (>100 tokens).
3. **High Path Length for Gradient Flow:** In an RNN, gradients must traverse $O(N)$ sequential steps to connect tokens separated by distance $N$. Transformers provide direct $O(1)$ connections between any pair of tokens via self-attention.
4. **Scalability:** Transformers scale efficiently with both data volume and compute parameters, enabling modern Foundation Models (LLMs).

---

---

## DL-100: What are embeddings?

**Domain:** Topic 44: Embeddings and Representation Learning &nbsp;|&nbsp; **Priority:** HIGH

An **embedding** is a learned, dense, low-dimensional continuous vector representation of discrete entities (words, subword tokens, sentences, or images):
$$\mathbf{e} \in \mathbb{R}^d \quad (\text{typically } d \in [768, 4096])$$

**Properties:**
- **Semantic Proximity:** Words with similar meanings or grammatical roles map to nearby points in vector space (e.g., $\text{cosine\_similarity}(\mathbf{e}_{\text{king}}, \mathbf{e}_{\text{queen}}) \approx 1$).
- **Vector Arithmetic:** Captures relational analogies:
  $$\mathbf{e}_{\text{king}} - \mathbf{e}_{\text{man}} + \mathbf{e}_{\text{woman}} \approx \mathbf{e}_{\text{queen}}$$
- **Differentiable Lookup:** Implemented in PyTorch as `nn.Embedding(vocab_size, embedding_dim)`.

---

---

