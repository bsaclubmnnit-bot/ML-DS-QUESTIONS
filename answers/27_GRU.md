# Section 27: Gated Recurrent Unit (GRU)

---

## Q359. What is a GRU?

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

## Q360. What are update and reset gates?

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

## Q361. How does GRU differ from LSTM?

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

## Q362. Why does GRU have fewer parameters?

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

## Q363. When might GRU train faster than LSTM?

GRU trains noticeably faster than LSTM under the following conditions:
1. **Compute-Bound Training:** With 25% fewer matrix multiplications per time step, forward and backward passes execute in fewer FLOPs.
2. **Resource-Constrained Environments:** Embedded systems, mobile processors, or single-GPU setups where smaller memory footprints yield higher GPU batch throughput.
3. **Long Sequence Batches:** Fewer tensor allocations and intermediate cache buffers allow larger batch sizes, accelerating overall convergence time.
4. **Fast Prototyping:** Quicker feedback loops on experimental models where the expressive advantage of LSTM is negligible.

---

## Q364. What are GRU advantages?

1. **Higher Efficiency:** Requires 25% fewer parameters and fewer tensor operations per sequence step.
2. **Faster Convergence:** Often reaches target validation loss faster than LSTM due to fewer optimization variables.
3. **Strong Generalization on Small Datasets:** Lower risk of overfitting when sequence data is scarce compared to more heavily parameterized LSTMs.
4. **Competitive Empirical Accuracy:** Benchmarks consistently show GRU achieves comparable performance to LSTM across machine translation, text classification, and time series tasks.

---

## Q365. What are GRU limitations?

1. **Less Fine-Grained Memory Control:** Because it lacks an independent output gate, all internal representations are exposed immediately.
2. **Harder to Control Long Horizons:** On complex, lengthy sequence tasks (>200 time steps) where separate storage and read mechanisms are vital, LSTM often outperforms GRU.
3. **Coupled Updating:** The update gate forces an exact trade-off between keeping past state and adding new state ($1 - z_t$ vs $z_t$), whereas an LSTM can independently forget nothing and add new information simultaneously.
4. **Sequential Nature:** Like LSTM, it cannot be trained in parallel across sequence steps, making it slower than Transformers on massive training datasets.

---

## Q366. How do you choose between GRU and LSTM?

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
