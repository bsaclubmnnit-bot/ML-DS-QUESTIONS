# Part VII: RAG & Information Retrieval

> **124 Interview Questions & Comprehensive Technical Solutions**  
> *Topics: RAG Pipelines, Chunking, Embeddings, Vector DBs, Hybrid Search, Reranking, GraphRAG, RAG Evaluation*  
> *Part of the [PIXEL CHAMP Master Question Bank](https://github.com/bsaclubmnnit-bot/ML-DS-QUESTIONS)*

---

## RAG-001: Explain a RAG pipeline end to end.?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`Explain a RAG pipeline end to end.` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-002: What is Agentic RAG?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Agentic RAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-003: What is GraphRAG?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is GraphRAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-004: What is Retrieval-Augmented Generation?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Retrieval-Augmented Generation` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-005: What is a document loader?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a document loader` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-006: What is context injection?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is context injection` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-007: What is conversational RAG?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is conversational RAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-008: What is document ingestion?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is document ingestion` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-009: What is metadata enrichment?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is metadata enrichment` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-010: What is multi-document RAG?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is multi-document RAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-011: What is multi-hop RAG?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is multi-hop RAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-012: What is overlap and why is it used?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is overlap and why is it used` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-013: What is query embedding?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is query embedding` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-014: What is recursive character splitting?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is recursive character splitting` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-015: What is text splitting?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is text splitting` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-016: How is retrieval different from generation?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How is retrieval different from generation` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-017: When should you combine RAG and fine-tuning?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`When should you combine RAG and fine-tuning` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-018: When should you use GraphRAG?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`When should you use GraphRAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-019: Why do we need RAG if an LLM already has knowledge?

**Domain:** Topic 52: RAG Fundamentals and Architecture &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Why do we need RAG if an LLM already has knowledge` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-020: What are the indexing and query-time stages of RAG?

**Domain:** Topic 53: Document Parsing, Chunking and Indexing &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What are the indexing and query-time stages of RAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-021: What is chunking?

**Domain:** Topic 53: Document Parsing, Chunking and Indexing &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is chunking` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-022: What is fixed-size chunking?

**Domain:** Topic 53: Document Parsing, Chunking and Indexing &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is fixed-size chunking` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-023: What is parent-child chunking?

**Domain:** Topic 53: Document Parsing, Chunking and Indexing &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is parent-child chunking` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-024: What is semantic chunking?

**Domain:** Topic 53: Document Parsing, Chunking and Indexing &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is semantic chunking` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-025: How do you choose chunk size?

**Domain:** Topic 53: Document Parsing, Chunking and Indexing &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you choose chunk size` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-026: What happens if chunks are too small?

**Domain:** Topic 53: Document Parsing, Chunking and Indexing &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What happens if chunks are too small` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-027: What metadata should be stored with chunks?

**Domain:** Topic 53: Document Parsing, Chunking and Indexing &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What metadata should be stored with chunks` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-028: Why is chunking important?

**Domain:** Topic 53: Document Parsing, Chunking and Indexing &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Why is chunking important` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-029: How are text embeddings generated?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`How are text embeddings generated` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-030: How do you update embeddings when documents change?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`How do you update embeddings when documents change` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-031: What is BM25?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is BM25` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-032: What is HNSW?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is HNSW` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-033: What is IVF?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is IVF` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-034: What is MRR?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is MRR` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-035: What is PQ/product quantization?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is PQ/product quantization` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-036: What is Precision@K?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Precision@K` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-037: What is Recall@K?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Recall@K` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-038: What is a vector database?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a vector database` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-039: What is an embedding model?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is an embedding model` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-040: What is an embedding?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is an embedding` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-041: What is cosine similarity?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is cosine similarity` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-042: What is dense retrieval?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is dense retrieval` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-043: What is hybrid retrieval?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is hybrid retrieval` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-044: What is nDCG?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is nDCG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-045: What is nearest-neighbor search?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is nearest-neighbor search` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-046: What is semantic similarity?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is semantic similarity` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-047: What is sparse retrieval?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is sparse retrieval` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-048: How do you evaluate retrieval quality?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you evaluate retrieval quality` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-049: How do you handle duplicate documents?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you handle duplicate documents` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-050: How do you handle multi-tenant vector stores?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you handle multi-tenant vector stores` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-051: How do you select an embedding model?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you select an embedding model` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-052: How does embedding drift affect a production RAG system?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How does embedding drift affect a production RAG system` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-053: What does embedding dimensionality mean?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What does embedding dimensionality mean` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-054: What happens if documents and queries use incompatible embedding models?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What happens if documents and queries use incompatible embedding models` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-055: When does keyword search outperform vector search?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`When does keyword search outperform vector search` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-056: Why use a vector database instead of a relational database? What are metadata filters?

**Domain:** Topic 54: Embedding Models and Vector Databases &nbsp;|&nbsp; **Priority:** LOWER

**Concept Overview:**
`Why use a vector database instead of a relational database? What are metadata filters` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-057: What is hybrid search?

**Domain:** Topic 55: Sparse Retrieval, BM25 and Hybrid Search &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is hybrid search` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-058: How would you combine BM25 and vector search?

**Domain:** Topic 55: Sparse Retrieval, BM25 and Hybrid Search &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you combine BM25 and vector search` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-059: What is reranking?

**Domain:** Topic 56: Reranking and Advanced Retrieval &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is reranking` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-060: Why is reranking useful?

**Domain:** Topic 56: Reranking and Advanced Retrieval &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Why is reranking useful` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-061: What is HYDE?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is HYDE` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-062: What is Self-RAG?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is Self-RAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-063: What is adaptive RAG?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is adaptive RAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-064: What is contextual compression?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is contextual compression` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-065: What is contextual retrieval?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is contextual retrieval` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-066: What is corrective RAG?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is corrective RAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-067: What is filtered vector search?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is filtered vector search` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-068: What is hierarchical retrieval?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is hierarchical retrieval` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-069: What is late interaction retrieval?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is late interaction retrieval` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-070: What is metadata-based retrieval?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is metadata-based retrieval` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-071: What is multi-query retrieval?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is multi-query retrieval` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-072: What is parent-document retrieval?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is parent-document retrieval` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-073: What is query expansion?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is query expansion` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-074: What is query rewriting?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is query rewriting` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-075: What is reciprocal rank fusion?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is reciprocal rank fusion` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-076: What is routing in RAG?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is routing in RAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-077: How do you combine SQL retrieval and vector retrieval?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you combine SQL retrieval and vector retrieval` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-078: How do you debug high retrieval recall but poor answers?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you debug high retrieval recall but poor answers` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-079: How do you debug low retrieval recall?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you debug low retrieval recall` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-080: How do you handle PDFs with images?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you handle PDFs with images` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-081: How do you handle code repositories with RAG?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you handle code repositories with RAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-082: How do you handle conflicting documents?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you handle conflicting documents` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-083: How do you handle scanned documents?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you handle scanned documents` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-084: How do you handle stale documents?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you handle stale documents` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-085: How do you handle structured databases in RAG?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you handle structured databases in RAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-086: How do you handle tables in RAG?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you handle tables in RAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-087: How do you implement access-control-aware retrieval?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you implement access-control-aware retrieval` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-088: How do you prevent irrelevant chunks from entering the context?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you prevent irrelevant chunks from entering the context` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-089: How do you reduce RAG cost?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you reduce RAG cost` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-090: How do you reduce RAG latency?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you reduce RAG latency` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-091: How would you route queries across multiple indexes?

**Domain:** Topic 57: Advanced RAG, GraphRAG and Multi-Hop RAG &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you route queries across multiple indexes` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-092: What is RAG evaluation?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is RAG evaluation` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-093: What is RAGAS?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is RAGAS` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-094: What is a golden dataset?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is a golden dataset` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-095: What is an evaluation dataset?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is an evaluation dataset` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-096: What is answer relevance?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is answer relevance` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-097: What is citation correctness?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is citation correctness` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-098: What is context precision?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is context precision` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-099: What is context recall?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is context recall` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-100: What is context relevance?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is context relevance` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-101: What is faithfulness?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is faithfulness` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-102: What is generation evaluation?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is generation evaluation` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-103: What is groundedness?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is groundedness` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-104: What is pairwise evaluation?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is pairwise evaluation` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-105: What is regression testing for LLM applications?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is regression testing for LLM applications` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-106: What is retrieval evaluation?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`What is retrieval evaluation` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-107: How do latency, cost, and quality trade off?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do latency, cost, and quality trade off` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-108: How do you create a golden set for RAG?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you create a golden set for RAG` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-109: How do you evaluate a RAG system without human labels?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you evaluate a RAG system without human labels` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-110: How do you evaluate retrieval independently from generation?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How do you evaluate retrieval independently from generation` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-111: How would you debug a RAG system that hallucinates?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you debug a RAG system that hallucinates` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-112: How would you detect retrieval drift?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you detect retrieval drift` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-113: How would you monitor RAG quality in production?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`How would you monitor RAG quality in production` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-114: What if answers are incomplete?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What if answers are incomplete` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-115: What if answers are too verbose?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What if answers are too verbose` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-116: What if answers cite the wrong source?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What if answers cite the wrong source` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-117: What if retrieval is correct but the model ignores the context?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What if retrieval is correct but the model ignores the context` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-118: What if retrieval returns the wrong documents?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What if retrieval returns the wrong documents` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-119: What if the model answers questions that are not supported by the documents?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`What if the model answers questions that are not supported by the documents` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-120: When should LLM-as-a-judge be used?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`When should LLM-as-a-judge be used` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-121: Which RAG metrics would you track?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** MEDIUM

**Concept Overview:**
`Which RAG metrics would you track` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-122: What are the limitations of LLM-as-a-judge?

**Domain:** Topic 58: RAG Evaluation and Troubleshooting &nbsp;|&nbsp; **Priority:** LOWER

**Concept Overview:**
`What are the limitations of LLM-as-a-judge` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-123: Can RAG completely eliminate hallucination?

**Domain:** Topic 59: Hallucination Reduction, Grounding and Citations &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`Can RAG completely eliminate hallucination` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

## RAG-124: How does RAG reduce hallucination?

**Domain:** Topic 59: Hallucination Reduction, Grounding and Citations &nbsp;|&nbsp; **Priority:** HIGH

**Concept Overview:**
`How does RAG reduce hallucination` is a critical component in Retrieval-Augmented Generation (RAG) architectures designed to ground LLMs in external proprietary knowledge bases.

**System Architecture & Pipeline Flow:**
1. **Ingestion & Chunking:** Parses documents into semantic chunks with metadata preservation and sliding windows.
2. **Dense & Sparse Embedding:** Projects text into dense vectors paired with sparse lexical inverted indexes (BM25).
3. **Hybrid Search & Fusion:** Combines dense cosine similarity with BM25 keyword retrieval using Reciprocal Rank Fusion (RRF).
4. **Cross-Encoder Reranking:** Scores candidate chunks with a dense cross-encoder before prompt synthesis.

**Production RAG Snippet:**
```python
# Hybrid retrieval and reranking logic
def hybrid_retrieval(query: str, dense_retriever, sparse_retriever, reranker, top_k=5):
    dense_docs = dense_retriever.search(query, k=top_k * 2)
    sparse_docs = sparse_retriever.search(query, k=top_k * 2)
    fused_candidates = list({d.id: d for d in (dense_docs + sparse_docs)}.values())
    reranked = reranker.rank(query=query, documents=fused_candidates, top_k=top_k)
    return reranked
```

**Interview Takeaway:**
Highlight the retrieval-generation trade-off, chunk size dilemmas (small for precise retrieval vs large for context retention), and RAG evaluation frameworks (faithfulness, answer relevance, context recall via Ragas).

---

