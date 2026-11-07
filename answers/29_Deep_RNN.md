# Section 29: Deep RNN

---

## Q373. What is a Deep RNN?

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

## Q374. How does stacking recurrent layers increase capacity?

Stacking recurrent layers increases representation capacity through **hierarchical temporal abstraction**:

1. **Depth Creates Non-Linear Feature Hierarchies:** Just as deep CNNs learn low-level edges in early layers and high-level concepts in deep layers, deep RNNs create functional hierarchies over sequential signals.
   - **Layer 1:** Captures low-level token/character transitions, phonemes, or local spikes.
   - **Layer 2:** Captures syntactic groupings, phrases, or short trends.
   - **Layer 3+:** Captures semantic meaning, overall intent, topic, or long-term seasonality.
2. **Multi-Scale Temporal Dynamics:** Higher layers often naturally operate on slower, broader temporal scales than lower layers.
3. **Exponential Hypothesis Space:** Deep models can represent certain mathematical functions with exponentially fewer parameters than shallow (single-layer) wide models.

---

## Q375. What are the advantages of Deep RNNs?

1. **Hierarchical Sequence Representations:** Learns multi-level abstractions (low-level syntax to high-level semantics).
2. **Higher Model Capacity:** Solves complex sequence modeling problems that cannot be solved by single-layer shallow RNNs regardless of hidden layer width.
3. **Decoupled Temporal & Feature Processing:** Separates time-stepping transitions from deep non-linear feature transformations.
4. **Superior Empirical Performance:** Historically provided the backbone for breakthrough machine translation (e.g., Google's 8-layer GNMT), speech recognition, and complex language modeling.

---

## Q376. What are the disadvantages of Deep RNNs?

1. **High Computational Cost:** Stacking $L$ layers multiplies both forward and backward pass FLOPs linearly by $L$.
2. **Severe Vanishing/Exploding Gradients Across Depth:** In addition to backpropagation through time, gradients must backpropagate through vertical layers, compounding stability issues.
3. **Increased Training Time & Latency:** Cannot compute layer $l+1$ until representations for layer $l$ are available, compounding sequential latency.
4. **Proneness to Overfitting:** More parameters require significantly larger datasets and heavy regularization (dropout, weight decay).

---

## Q377. What training challenges occur in Deep RNNs?

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

## Q378. How can dropout be applied to recurrent networks?

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

