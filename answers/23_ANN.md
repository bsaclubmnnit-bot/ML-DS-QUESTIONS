# Section 23: Artificial Neural Networks (ANN)

---

## Q301. What is an Artificial Neural Network?

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

## Q302. What is an artificial neuron?

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

## Q303. What are weights and biases?

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

## Q304. What is an activation function?

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

## Q305. Why are non-linear activation functions required?

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

## Q306. What is ReLU?

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

## Q307. What is sigmoid?

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

## Q308. What is tanh?

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

## Q309. What is a hidden layer?

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

## Q310. What is forward propagation?

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

## Q311. What is backpropagation?

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

## Q312. How does gradient descent train a neural network?

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

## Q313. What is a learning rate?

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

## Q314. What is an epoch?

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

## Q315. What is batch size?

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

## Q316. What is dropout?

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

## Q317. What is batch normalization?

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

## Q318. What is the vanishing gradient problem?

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

## Q319. What is the exploding gradient problem?

The **exploding gradient problem** occurs when gradients grow exponentially during backpropagation, causing extremely large weight updates and destabilizing training.

**Cause:**
- Opposite of vanishing gradient
- Occurs when weight matrices have eigenvalues > 1
- Products of large values → gradient → ∞

**Symptoms:**
- Loss becomes NaN or Inf
- Weights blow up to very large values
- Very unstable training behavior

**Solutions:**

```python
# 1. Gradient Clipping (most effective)
optimizer = torch.optim.SGD(model.parameters(), lr=0.01)

for batch in dataloader:
    loss = compute_loss(batch)
    loss.backward()
    
    # Clip gradients before optimizer step
    torch.nn.utils.clip_grad_norm_(model.parameters(), max_norm=1.0)
    
    optimizer.step()
    optimizer.zero_grad()

# 2. Proper weight initialization
nn.init.xavier_uniform_(layer.weight)

# 3. Batch Normalization
nn.BatchNorm1d(128)

# 4. Smaller learning rate
optimizer = torch.optim.Adam(model.parameters(), lr=1e-4)

# 5. LSTM/GRU for recurrent networks
```

> **Gradient clipping** is the standard solution for recurrent networks; it caps the gradient norm to prevent catastrophic updates.

---

## Q320. What is weight initialization?

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
