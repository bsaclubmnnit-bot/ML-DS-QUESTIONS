# Section 25: Recurrent Neural Networks (RNN)

---

## Q336. What is an RNN?

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

## Q337. Why are RNNs useful for sequential data?

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

## Q338. What is a hidden state?

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

## Q339. What is backpropagation through time?

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

## Q340. Why do vanilla RNNs suffer from vanishing gradients?

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

## Q341. What is the exploding gradient problem?

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

## Q342. What are the limitations of vanilla RNNs?

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

## Q343. What is sequence-to-sequence learning?

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

## Q344. What are many-to-one architectures?

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

## Q345. What are many-to-many architectures?

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

## Q346. What applications commonly use RNNs?

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
