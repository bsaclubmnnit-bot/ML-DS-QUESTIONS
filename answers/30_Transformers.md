# Section 30: Transformers

---

## Q379. What is a Transformer architecture?

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

## Q380. Why were Transformers introduced?

Transformers were introduced to overcome the fundamental bottlenecks of recurrent architectures (RNNs, LSTMs, GRUs) and convolutional sequence models:

1. **Lack of Parallelization in RNNs:** RNNs process sequences token-by-token sequentially ($h_t$ strictly requires $h_{t-1}$). Training cannot be parallelized across the time dimension, preventing full utilization of modern GPU/TPU hardware.
2. **Degradation Over Long Horizons:** Even with gating (LSTM/GRU), RNNs compress all prior information into fixed-size vectors, resulting in information loss over long sequences (>100 tokens).
3. **High Path Length for Gradient Flow:** In an RNN, gradients must traverse $O(N)$ sequential steps to connect tokens separated by distance $N$. Transformers provide direct $O(1)$ connections between any pair of tokens via self-attention.
4. **Scalability:** Transformers scale efficiently with both data volume and compute parameters, enabling modern Foundation Models (LLMs).

---

## Q381. What is self-attention?

**Self-attention** is a mechanism that allows each token in a sequence to attend to, weigh, and aggregate information from **every other token in the same sequence**.

Rather than processing each token in isolation, self-attention computes an attention weight between token $i$ and token $j$, determining how much token $i$ should factor in the representation of token $j$.

**Intuitive Example:**
In the sentence:
> *"The animal didn't cross the street because **it** was too tired."*

When self-attention processes the word **"it"**, it computes attention scores with all other words. The highest attention score is assigned to **"animal"**, enabling the model to dynamically resolve the pronoun reference.

---

## Q382. What are Query, Key, and Value?

Inspired by information retrieval and database search systems, self-attention maps inputs to three distinct projection spaces:

1. **Query ($Q$):** Represents what the current token is *searching for* or asking about other tokens.
2. **Key ($K$):** Represents what the token *contains* or offers to match incoming queries.
3. **Value ($V$):** The actual substantive information/content that gets retrieved and aggregated if the query matches the key.

For input sequence matrix $X \in \mathbb{R}^{N \times d_{\text{model}}}$:
$$Q = X W_Q, \quad K = X W_K, \quad V = X W_V$$
where $W_Q, W_K \in \mathbb{R}^{d_{\text{model}} \times d_k}$ and $W_V \in \mathbb{R}^{d_{\text{model}} \times d_v}$ are learnable projection weights.

---

## Q383. What is scaled dot-product attention?

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

## Q384. What is multi-head attention?

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

## Q385. Why are positional encodings needed?

Because self-attention operations are **permutation invariant** (i.e., $\text{Attention}(P X) = P \text{Attention}(X)$ where $P$ is a permutation matrix), a Transformer without position signals treats the sequence as an unordered "bag of words":
> *"Dog bites man"* would produce identical representations to *"Man bites dog"*.

Since Transformers contain no recurrent step transitions or convolutions, positional encodings must be injected directly into the input embeddings to provide token order awareness:
$$X_{\text{input}} = \text{Embedding}(X) + \text{PositionalEncoding}$$

**Sinusoidal Positional Encoding (Vaswani et al.):**
$$PE_{(pos, 2i)} = \sin\left(\frac{pos}{10000^{2i/d_{\text{model}}}}\right)$$
$$PE_{(pos, 2i+1)} = \cos\left(\frac{pos}{10000^{2i/d_{\text{model}}}}\right)$$
Allows the model to easily learn relative positions because $PE_{pos + k}$ can be expressed as a linear function of $PE_{pos}$.

---

## Q386. What is an encoder?

In the Transformer architecture, the **Encoder** processes the input sequence and produces rich contextual representations.

An encoder is a stack of $N$ identical blocks (typically 6 to 32 layers). Each block contains:
1. **Multi-Head Self-Attention:** Computes pairwise context across the entire input sequence simultaneously (bidirectional).
2. **Add & Norm (Residual Connection + LayerNorm):** $x + \text{Sublayer}(x)$, facilitating deep gradient flow.
3. **Position-wise Feed-Forward Network:** Two linear layers with non-linear activation ($\text{ReLU}$ or $\text{GELU}$).
4. **Add & Norm:** Second residual connection followed by layer normalization.

*Encoder-only models:* BERT, RoBERTa, DeBERTa (primarily used for classification, NER, and extractive QA).

---

## Q387. What is a decoder?

The **Decoder** generates output sequences token-by-token (autoregressively) conditioned on the encoder outputs and prior generated tokens.

Each decoder layer contains **three sublayers**:
1. **Masked Multi-Head Self-Attention:** Attends only to previous positions in the output sequence, preventing tokens from attending to future positions during training.
2. **Cross-Attention (Encoder-Decoder Attention):** Queries come from the previous decoder layer, while Keys and Values come from the encoder output. This transfers input knowledge to the generation process.
3. **Position-wise Feed-Forward Network:** Dense transformation layers.

*Decoder-only models:* GPT series, LLaMA, Claude, Mistral (standard for generative tasks).

---

## Q388. What is masked self-attention?

**Masked self-attention** (or causal self-attention) prevents each token in a generative decoder from attending to future tokens ($j > i$).

During training, target sequences are passed all at once to enable parallel training. To preserve the autoregressive property (predicting token $t$ using only tokens $1$ to $t-1$), future positions are masked by setting their pre-softmax attention scores to $-\infty$:

$$\text{Attention Matrix} = \begin{bmatrix} 
\text{score}_{11} & -\infty & -\infty \\
\text{score}_{21} & \text{score}_{22} & -\infty \\
\text{score}_{31} & \text{score}_{32} & \text{score}_{33}
\end{bmatrix}$$

Applying $\text{softmax}$ turns $-\infty$ into $0$ probability, ensuring zero attention flow from future positions.

---

## Q389. What is cross-attention?

**Cross-attention** (or Encoder-Decoder Attention) connects the decoder with the encoder representations.

In self-attention, Queries, Keys, and Values all originate from the **same** sequence:
$$Q = X W_Q, \quad K = X W_K, \quad V = X W_V$$

In cross-attention:
- **Queries ($Q$)** originate from the **decoder's previous layer**: $Q = H_{\text{dec}} W_Q$
- **Keys ($K$) and Values ($V$)** originate from the **encoder's final output**: $K = H_{\text{enc}} W_K, \quad V = H_{\text{enc}} W_V$

This enables the decoder to query the source document to decide what information to generate at each output step (e.g., in machine translation or summarization).

---

## Q390. What is layer normalization?

**Layer Normalization (LayerNorm)** normalizes the activations across the **feature dimension** (hidden channels) for each individual sample and token independently:

$$\text{LayerNorm}(x) = \frac{x - \mu}{\sqrt{\sigma^2 + \epsilon}} \odot \gamma + \beta$$
where $\mu$ and $\sigma$ are the mean and standard deviation computed across all hidden features $d$ of a single token:
$$\mu = \frac{1}{d}\sum_{i=1}^d x_i, \quad \sigma^2 = \frac{1}{d}\sum_{i=1}^d (x_i - \mu)^2$$

**Why LayerNorm over BatchNorm:**
- **Batch independence:** Does not depend on batch size or other samples in the batch.
- Works seamlessly with variable-length sequences.
- Supports batch size of 1 during autoregressive inference without requiring running statistics.

---

## Q391. What is the feed-forward network in a Transformer block?

Each Transformer encoder and decoder block contains a **Position-wise Feed-Forward Network (FFN)** applied identically and separately to each position:

$$\text{FFN}(x) = \max(0, x W_1 + b_1) W_2 + b_2 = \text{GELU}(x W_1 + b_1) W_2 + b_2$$

**Architecture characteristics:**
- **Dimension Expansion:** Projects hidden dimension $d_{\text{model}}$ to an intermediate dimension $d_{ff}$ (typically $4 \times d_{\text{model}}$), then projects back to $d_{\text{model}}$.
- **Parameter Concentration:** Accounts for roughly two-thirds of the total parameters in a Transformer block.
- **Role:** While self-attention aggregates information across tokens (routing/communication), the FFN processes, synthesizes, and stores factual knowledge within the parameters (computation/storage).

---

## Q392. How do Transformers differ from RNNs?

| Dimension | Recurrent Neural Network (RNN) | Transformer |
|:---|:---|:---|
| **Computation Mechanism** | Sequential recurrence ($h_t = f(h_{t-1}, x_t)$) | Parallel self-attention across all tokens |
| **Training Parallelization** | Incompatible; strictly sequential | Fully parallelizable across sequence length |
| **Max Information Path** | $O(N)$ steps across sequence length | $O(1)$ direct connection between any two tokens |
| **Memory Bottleneck** | Fixed-size vector compression causes decay | Full attention matrix retains pairwise context |
| **Computational Complexity** | $O(N \cdot d^2)$ per sequence | $O(N^2 \cdot d)$ per sequence |
| **Hardware Saturation** | Low GPU utilization | High GPU tensor core utilization |

---

## Q393. How do Transformers differ from LSTMs?

| Feature | LSTM | Transformer |
|:---|:---|:---|
| **Core Architecture** | Gated memory cell ($f_t, i_t, o_t, C_t$) | Multi-head self-attention + MLP feed-forward |
| **Sequence Processing** | Step-by-step sequential processing | Entire sequence processed simultaneously |
| **Long-Distance Dependencies**| Limited beyond 200–500 steps | Scales to thousands or millions of tokens |
| **Positional Awareness** | Implicitly encoded via step order | Explicitly injected via positional encodings |
| **Inference Scalability** | Low memory footprint; fixed hidden state | Requires KV cache for efficient autoregression |
| **Empirical State-of-the-Art**| Obsolete for large-scale foundation models | Dominant architecture across NLP, Vision, Audio |

---

## Q394. What is BERT?

**BERT (Bidirectional Encoder Representations from Transformers)** is an encoder-only Transformer architecture introduced by Devlin et al. (Google, 2018).

**Key Innovations:**
1. **Bidirectional Context:** Unlike autoregressive models that read strictly left-to-right, BERT conditions on both left and right context simultaneously across all layers.
2. **Pretraining Objectives:**
   - **Masked Language Modeling (MLM):** 15% of tokens are randomly masked (`[MASK]`), and the model learns to predict them using bidirectional context.
   - **Next Sentence Prediction (NSP):** Binary classification predicting whether sentence B follows sentence A.
3. **Usage:** Primarily fine-tuned for extractive tasks: classification, NER, question answering, semantic search.

---

## Q395. What is GPT?

**GPT (Generative Pre-trained Transformer)** is a decoder-only Transformer family developed by OpenAI (Radford et al., 2018–present).

**Key Innovations:**
1. **Autoregressive Causal Modeling:** Pretrained to predict the next token given preceding context:
   $$\mathcal{L}_{GPT} = -\sum_{i=1}^N \log P(x_i \mid x_1, x_2, \dots, x_{i-1})$$
2. **Causal Masking:** Strict lower-triangular attention masks ensure no future leakage.
3. **Emergent Capabilities & Scaling Laws:** Demonstrates that scaling model parameters and pretraining tokens yields zero-shot and few-shot reasoning, translation, and code generation capabilities without task-specific architectural changes.

---

## Q396. What is pretraining?

**Pretraining** is the first phase of the modern two-stage LLM paradigm:
1. **Data:** Unsupervised or self-supervised training on massive web-scale corpora (trillions of tokens consisting of text, books, articles, code).
2. **Objective:** Next-token prediction (causal LM) or masked token recovery (MLM).
3. **Outcome:** The model learns grammar, syntax, world knowledge, reasoning heuristics, common sense, and representation manifolds.
4. **Compute:** Extremely resource-intensive (requires thousands of GPUs for weeks or months).

Pretraining builds the foundational base model upon which specialized behaviors can be added.

---

## Q397. What is fine-tuning?

**Fine-tuning** is the adaptation phase where a pretrained base model is specialized for specific downstream tasks or human alignment:

1. **Supervised Fine-Tuning (SFT):** Training on high-quality curated prompt-response pairs to teach instruction-following behavior.
2. **Reinforcement Learning from Human Feedback (RLHF / DPO):** Aligning model outputs with human preferences regarding helpfulness, accuracy, and safety.
3. **Parameter-Efficient Fine-Tuning (PEFT / LoRA):** Freezing base weights and training low-rank adapter matrices ($W = W_0 + B A$), drastically reducing GPU memory requirements during fine-tuning.

---

## Q398. What are embeddings?

An **embedding** is a learned, dense, low-dimensional continuous vector representation of discrete entities (words, subword tokens, sentences, or images):
$$\mathbf{e} \in \mathbb{R}^d \quad (\text{typically } d \in [768, 4096])$$

**Properties:**
- **Semantic Proximity:** Words with similar meanings or grammatical roles map to nearby points in vector space (e.g., $\text{cosine\_similarity}(\mathbf{e}_{\text{king}}, \mathbf{e}_{\text{queen}}) \approx 1$).
- **Vector Arithmetic:** Captures relational analogies:
  $$\mathbf{e}_{\text{king}} - \mathbf{e}_{\text{man}} + \mathbf{e}_{\text{woman}} \approx \mathbf{e}_{\text{queen}}$$
- **Differentiable Lookup:** Implemented in PyTorch as `nn.Embedding(vocab_size, embedding_dim)`.

---

## Q399. What is a context window?

A **context window** is the maximum sequence length (number of input tokens) that a Transformer model can process in a single forward pass.

- **Constraint:** In standard full self-attention, memory and compute scale quadratically with context length: $\mathcal{O}(N^2)$.
- **Evolution:**
  - Original Transformer (2017): 512 tokens
  - GPT-3 (2020): 2,048 tokens
  - GPT-4 (2023): 32,768 to 128,000 tokens
  - Modern LLMs (Gemini, Claude 3, LLaMA 3.1): 128,000 to 2,000,000+ tokens
- **Significance:** Determines how much text, documentation, codebase context, or conversational history the model can reason over simultaneously.

---

## Q400. What is tokenization?

**Tokenization** is the process of segmenting raw text strings into discrete atomic units (tokens) that can be mapped to integers (token IDs) for model ingestion:

$$\text{"Understanding tokenization"} \longrightarrow [18452,\, 11241,\, 1634]$$

**Modern Approaches: Subword Tokenization**
1. **Byte-Pair Encoding (BPE):** Iteratively merges the most frequent pairs of bytes or characters (used in GPT, LLaMA).
2. **WordPiece:** Merges characters based on likelihood maximization (used in BERT).
3. **SentencePiece:** Treats raw text as a sequence of bytes without requiring whitespace splitting, handling multilingual inputs seamlessly.

**Benefits of Subword Tokenization:**
- Avoids Out-Of-Vocabulary (OOV) errors: rare or novel words are decomposed into familiar subwords or bytes.
- Compact vocabulary size (typically 32,000 to 128,000 tokens).

---

## Q401. Why is standard attention computationally expensive?

Standard scaled dot-product attention requires computing the inner product between every query token and every key token:

$$\text{Attention Matrix} = \text{Softmax}\left(\frac{Q K^T}{\sqrt{d_k}}\right) \in \mathbb{R}^{B \times H \times N \times N}$$

For sequence length $N$:
1. $Q K^T$ requires $N \times N$ matrix multiplications.
2. Storing the $N \times N$ attention weight matrix in GPU memory requires $\mathcal{O}(N^2)$ storage per head and per layer.
3. For long sequences (e.g., $N = 100,000$), $N^2 = 10^{10}$ elements per attention head. At 16-bit precision across 32 layers and 32 heads, this demands hundreds of gigabytes of VRAM just to store intermediate attention maps.

---

## Q402. What is the quadratic complexity problem?

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

## Q403. How do modern architectures handle long contexts?

Modern architectures overcome the quadratic attention bottleneck using a combination of algorithmic, mathematical, and hardware optimizations:

1. **FlashAttention (Dao et al.):** An exact attention algorithm that tiles the computation into GPU SRAM blocks, eliminating the need to read/write the full $N \times N$ attention matrix from high-bandwidth memory (HBM). Reduces memory from $\mathcal{O}(N^2)$ to $\mathcal{O}(N)$ and speeds up computation by 2–4x.
2. **Rotary Position Embeddings (RoPE) & YaRN:** Encodes relative position by rotating queries and keys in the complex plane; enables context window extension via frequency interpolation without catastrophic perplexity degradation.
3. **Multi-Query Attention (MQA) & Grouped-Query Attention (GQA):** Shares key and value heads across multiple query heads, slashing KV cache memory footprint by 4x to 8x during autoregressive decoding.
4. **Sparse & Linear Attention:**
   - **Local / Sliding Window Attention:** Tokens attend only to neighbors within a fixed window $W$, achieving $\mathcal{O}(N \cdot W)$ complexity (e.g., Mistral, Longformer).
   - **State Space Models (SSMs) & Hybrid Architectures:** Models like Mamba and RWKV achieve true $\mathcal{O}(N)$ linear time and constant $\mathcal{O}(1)$ inference memory through continuous state-space recurrences.

