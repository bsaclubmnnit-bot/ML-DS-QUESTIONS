# Section 28: Bidirectional LSTM (BiLSTM)

---

## Q367. What is a BiLSTM?

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

## Q368. Why does bidirectional processing help?

In natural language and many real-world sequential signals, the meaning of a word or event often depends heavily on what comes **after** it, not just what preceded it.

**Example 1: Word Sense Disambiguation**
- *"The **bank** of the river was muddy."*
- *"The **bank** approved the home loan."*
A unidirectional model reading the word *"bank"* has no access to *"river"* or *"loan"*, making disambiguation ambiguous. A bidirectional model resolves ambiguity immediately because future tokens inform the current representation.

**Example 2: Named Entity Recognition (NER)**
- *"Apple released the iPhone."* vs *"Apple was sliced into four pieces."*
Having future tokens ("iPhone" vs "sliced") immediately clarifies whether "Apple" is an organization or a fruit.

---

## Q369. What does the forward LSTM capture?

The **forward LSTM** computes hidden states moving chronologically from $t=1$ to $t=T$:
$$\overrightarrow{h}_t = \text{LSTM}_{fwd}(x_t, \overrightarrow{h}_{t-1})$$

**What it captures:**
- **Historical Context:** Preceding tokens, previous events, and causal trends leading up to time $t$.
- **Syntactic Structure from Left to Right:** Subject-verb agreements established earlier in a sentence.
- **Cumulative Trajectory:** The running sequence summary accumulated from the beginning of the input.

---

## Q370. What does the backward LSTM capture?

The **backward LSTM** computes hidden states moving in reverse chronological order from $t=T$ down to $t=1$:
$$\overleftarrow{h}_t = \text{LSTM}_{bwd}(x_t, \overleftarrow{h}_{t+1})$$

**What it captures:**
- **Future Context:** Downstream tokens, outcomes, and concluding remarks occurring after time $t$.
- **Right-to-Left Dependencies:** Clues provided by subsequent objects, prepositions, or sentence endings.
- **Anticipatory Signals:** Resolving forward references (cataphora) and clarifying ambiguous entities early in a sequence.

---

## Q371. When is BiLSTM unsuitable?

BiLSTM is fundamentally unsuitable in situations where future information cannot be accessed at runtime:

1. **Causal Real-Time Forecasting:** Stock price prediction, real-time sensor monitoring, or equipment failure prediction where future timestamps $t+1, t+2$ do not yet exist.
2. **Autoregressive Text Generation:** Next-token generation (such as language models, chat assistants, or auto-complete) where tokens are generated sequentially one by one.
3. **Low-Latency Streaming Speech Recognition:** Real-time speech transcription where waiting for the user to finish speaking introduces unacceptable latency.
4. **Strictly Causal Tasks:** Any task requiring strict adherence to the arrow of time without sequence buffering.

---

## Q372. How does BiLSTM compare with unidirectional LSTM?

| Feature | Unidirectional LSTM | Bidirectional LSTM (BiLSTM) |
|:---|:---|:---|
| **Context Window** | Past only ($t \le \tau$) | Full context: Past and Future ($1 \le t \le T$) |
| **Output Dimension** | $d_h$ | $2 \times d_h$ (when concatenated) |
| **Parameters** | $1 \times$ standard LSTM parameters | Exactly $2 \times$ parameters (two independent LSTM nets) |
| **Inference Latency** | Can process streaming inputs token-by-token | Requires entire sequence before backward pass can execute |
| **Causal Forecasting** | Suitable (strict causal masking) | Unsuitable (data leakage of future observations) |
| **Classification / NER** | Good | Superior (state-of-the-art for RNN-based NLP tasks) |

