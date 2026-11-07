# Part VI: Generative AI & LLMs

> **112 Interview Questions & Comprehensive Technical Solutions**  
> *Topics: Self-Attention, Prompt Engineering, Context Windows, Decoding Strategies, Fine-Tuning, LoRA/QLoRA, RLHF/DPO*  
> *Part of the [PIXEL CHAMP Master Question Bank](https://github.com/bsaclubmnnit-bot/ML-DS-QUESTIONS)*

---

## LLM-001: Explain self-attention.?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`Explain self-attention.` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-002: What are Query, Key, and Value in attention?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are Query, Key, and Value in attention` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-003: What are function/tool calls?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are function/tool calls` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-004: What are system, human, and Al messages?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are system, human, and Al messages` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-005: What is DPO?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is DPO` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-006: What is JSON mode?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is JSON mode` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-007: What is RLHF?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is RLHF` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-008: What is a foundation model?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a foundation model` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-009: What is a system prompt?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a system prompt` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-010: What is a transformer?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a transformer` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-011: What is alignment?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is alignment` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-012: What is an LLM?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is an LLM` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-013: What is beam search and when is it useful?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is beam search and when is it useful` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-014: What is context engineering?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is context engineering` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-015: What is deterministic generation?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is deterministic generation` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-016: What is hallucination in LLMs?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is hallucination in LLMs` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-017: What is instruction tuning?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is instruction tuning` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-018: What is model latency?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is model latency` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-019: What is positional encoding?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is positional encoding` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-020: What is prompt engineering?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is prompt engineering` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-021: What is structured output?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is structured output` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-022: What is the difference between RLHF and DPO?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is the difference between RLHF and DPO` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-023: What is throughput in LLM inference?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is throughput in LLM inference` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-024: How do you reduce LLM cost?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you reduce LLM cost` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-025: How do you reduce LLM latency?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you reduce LLM latency` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-026: How would you choose an LLM for a production application?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you choose an LLM for a production application` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-027: What is Generative Al, and how is it different from traditional predictive ML?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What is Generative Al, and how is it different from traditional predictive ML` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-028: Why are transformers better suited than RNNs for large-scale language modeling?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Why are transformers better suited than RNNs for large-scale language modeling` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-029: Why do LLMs hallucinate?

**Domain:** Topic 46: Generative AI and LLM Fundamentals &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Why do LLMs hallucinate` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-030: How does tokenization work?

**Domain:** Topic 47: Tokenization, Embeddings and Context Windows &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`How does tokenization work` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-031: What is a context window?

**Domain:** Topic 47: Tokenization, Embeddings and Context Windows &nbsp;|&nbsp; **Priority:** HIGH

A **context window** is the maximum sequence length (number of input tokens) that a Transformer model can process in a single forward pass.

- **Constraint:** In standard full self-attention, memory and compute scale quadratically with context length: $\mathcal{O}(N^2)$.
- **Evolution:**
  - Original Transformer (2017): 512 tokens
  - GPT-3 (2020): 2,048 tokens
  - GPT-4 (2023): 32,768 to 128,000 tokens
  - Modern LLMs (Gemini, Claude 3, LLaMA 3.1): 128,000 to 2,000,000+ tokens
- **Significance:** Determines how much text, documentation, codebase context, or conversational history the model can reason over simultaneously.

---

---

## LLM-032: What is a token?

**Domain:** Topic 47: Tokenization, Embeddings and Context Windows &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a token` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-033: What is time-to-first-token?

**Domain:** Topic 47: Tokenization, Embeddings and Context Windows &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is time-to-first-token` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-034: What is token cost?

**Domain:** Topic 47: Tokenization, Embeddings and Context Windows &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is token cost` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-035: What is tokenization?

**Domain:** Topic 47: Tokenization, Embeddings and Context Windows &nbsp;|&nbsp; **Priority:** HIGH

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

---

## LLM-036: What happens when the context window is exceeded?

**Domain:** Topic 47: Tokenization, Embeddings and Context Windows &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What happens when the context window is exceeded` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-037: How do you defend against prompt injection?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`How do you defend against prompt injection` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-038: What is ReAct prompting?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is ReAct prompting` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-039: What is chain-of-thought prompting?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is chain-of-thought prompting` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-040: What is constrained decoding?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is constrained decoding` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-041: What is context compression?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is context compression` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-042: What is context prioritization?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is context prioritization` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-043: What is few-shot prompting?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is few-shot prompting` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-044: What is indirect prompt injection?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is indirect prompt injection` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-045: What is instruction hierarchy?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is instruction hierarchy` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-046: What is prompt chaining?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is prompt chaining` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-047: What is prompt injection?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is prompt injection` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-048: What is prompt leakage?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is prompt leakage` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-049: What is role prompting?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is role prompting` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-050: What is self-consistency?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is self-consistency` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-051: What is zero-shot prompting?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is zero-shot prompting` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-052: How do you debug a prompt that works on some examples but fails on others?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you debug a prompt that works on some examples but fails on others` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-053: How do you design prompts for reliable classification?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you design prompts for reliable classification` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-054: How do you force an LLM to return valid JSON?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you force an LLM to return valid JSON` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-055: How do you handle ambiguous user queries?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you handle ambiguous user queries` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-056: How do you manage very long context?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you manage very long context` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-057: How do you prevent irrelevant context from degrading an answer?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you prevent irrelevant context from degrading an answer` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-058: How would you A/B test prompts?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you A/B test prompts` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-059: How would you design a prompt for a tool-using agent?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you design a prompt for a tool-using agent` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-060: How would you version prompts in production?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you version prompts in production` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-061: Should chain-of-thought be exposed to users?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Should chain-of-thought be exposed to users` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-062: What makes a good prompt?

**Domain:** Topic 48: Prompt Engineering and Context Engineering &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What makes a good prompt` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-063: What is greedy decoding?

**Domain:** Topic 49: LLM Inference, Decoding and Sampling &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is greedy decoding` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-064: What is temperature?

**Domain:** Topic 49: LLM Inference, Decoding and Sampling &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is temperature` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-065: What is top-k sampling?

**Domain:** Topic 49: LLM Inference, Decoding and Sampling &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is top-k sampling` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-066: How do temperature, top-k, and top-p differ?

**Domain:** Topic 49: LLM Inference, Decoding and Sampling &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do temperature, top-k, and top-p differ` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-067: How do you detect data leakage?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`How do you detect data leakage` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-068: How do you prevent overfitting during fine-tuning?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`How do you prevent overfitting during fine-tuning` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-069: What are LoRA adapters?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are LoRA adapters` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-070: What is LoRA?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is LoRA` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-071: What is PEFT?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is PEFT` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-072: What is QLoRA?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is QLoRA` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-073: What is adapter merging?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is adapter merging` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-074: What is catastrophic forgetting?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is catastrophic forgetting` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-075: What is full fine-tuning?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is full fine-tuning` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-076: What is gradient accumulation?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is gradient accumulation` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-077: What is instruction fine-tuning?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is instruction fine-tuning` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-078: What is learning rate in fine-tuning?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is learning rate in fine-tuning` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-079: What is parameter-efficient fine-tuning?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is parameter-efficient fine-tuning` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-080: What is rank in LoRA?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is rank in LoRA` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-081: What is supervised fine-tuning?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is supervised fine-tuning` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-082: What is train/validation/test splitting for fine-tuning?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is train/validation/test splitting for fine-tuning` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-083: What is warmup?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is warmup` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-084: What is weight decay?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is weight decay` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-085: Can RAG and fine-tuning be used together?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Can RAG and fine-tuning be used together` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-086: How do you choose LoRA rank?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you choose LoRA rank` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-087: How do you choose between multiple adapters?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you choose between multiple adapters` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-088: How do you deploy a LoRA adapter?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you deploy a LoRA adapter` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-089: How do you evaluate a fine-tuned model?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you evaluate a fine-tuned model` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-090: How do you prepare a fine-tuning dataset?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you prepare a fine-tuning dataset` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-091: How do you remove duplicates from training data?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you remove duplicates from training data` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-092: How do you version fine-tuned models?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you version fine-tuned models` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-093: How does LoRA work?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How does LoRA work` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-094: How much data is needed for fine-tuning?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How much data is needed for fine-tuning` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-095: What happens if the fine-tuned model performs worse than the base model?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What happens if the fine-tuned model performs worse than the base model` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-096: What makes a high-quality instruction dataset?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What makes a high-quality instruction dataset` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-097: What metrics should be used for fine-tuning?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What metrics should be used for fine-tuning` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-098: When should you fine-tune an LLM?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`When should you fine-tune an LLM` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-099: Why can fine-tuning improve style but hurt factuality?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Why can fine-tuning improve style but hurt factuality` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-100: Why does QLoRA reduce memory requirements?

**Domain:** Topic 50: Fine-Tuning, PEFT, LoRA and QLoRA &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Why does QLoRA reduce memory requirements` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-101: What are the stages of RLHF?

**Domain:** Topic 51: RLHF, DPO and Model Alignment &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are the stages of RLHF` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-102: What is Constitutional Al?

**Domain:** Topic 51: RLHF, DPO and Model Alignment &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Constitutional Al` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-103: What is PPO?

**Domain:** Topic 51: RLHF, DPO and Model Alignment &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is PPO` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-104: What is a reward model?

**Domain:** Topic 51: RLHF, DPO and Model Alignment &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a reward model` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-105: What is alignment tax?

**Domain:** Topic 51: RLHF, DPO and Model Alignment &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is alignment tax` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-106: What is preference data?

**Domain:** Topic 51: RLHF, DPO and Model Alignment &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is preference data` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-107: What is rejection sampling?

**Domain:** Topic 51: RLHF, DPO and Model Alignment &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is rejection sampling` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-108: What is reward hacking?

**Domain:** Topic 51: RLHF, DPO and Model Alignment &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is reward hacking` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-109: What is specification gaming?

**Domain:** Topic 51: RLHF, DPO and Model Alignment &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is specification gaming` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-110: How do you evaluate safety after fine-tuning?

**Domain:** Topic 51: RLHF, DPO and Model Alignment &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you evaluate safety after fine-tuning` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-111: How do you prevent a fine-tuning dataset from teaching unsafe behavior?

**Domain:** Topic 51: RLHF, DPO and Model Alignment &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you prevent a fine-tuning dataset from teaching unsafe behavior` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

## LLM-112: How does DPO work conceptually?

**Domain:** Topic 51: RLHF, DPO and Model Alignment &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How does DPO work conceptually` is a central concept in modern Large Language Models (LLMs), autoregressive generation, and generative AI systems.

**Technical Mechanics & Architecture:**
- **Attention & Representation:** Projects tokens into Query, Key, and Value spaces, scales attention scores by $1/\sqrt{d_k}$, and applies layer normalization and residual connections.
- **Parameter Efficiency & Scaling:** Optimizes compute, VRAM allocation (KV cache), and parameter updates during pretraining or fine-tuning (e.g., LoRA rank decomposition $W = W_0 + B A$).
- **Alignment:** Aligns raw base model next-token prediction with human preferences using SFT, RLHF, or Direct Preference Optimization (DPO).

**PyTorch / HuggingFace Implementation:**
```python
import torch
import torch.nn as nn

# Causal attention projection
class CausalAttentionBlock(nn.Module):
    def __init__(self, d_model: int, n_heads: int):
        super().__init__()
        self.mha = nn.MultiheadAttention(d_model, n_heads, batch_first=True)
        self.norm = nn.LayerNorm(d_model)
        
    def forward(self, x: torch.Tensor, mask: torch.Tensor) -> torch.Tensor:
        attn_out, _ = self.mha(x, x, x, attn_mask=mask)
        return self.norm(x + attn_out)
```

**Interview Takeaway:**
Explain the exact attention equations, compare decoder-only vs encoder-only models, and discuss quantization (4-bit/8-bit QLoRA) trade-offs.

---

