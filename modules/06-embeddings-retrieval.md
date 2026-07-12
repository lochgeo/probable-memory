---
layout: default
title: Embeddings & Retrieval
parent: Day 1 – Foundations of LLMs and RAG
nav_order: 7
---

# Module 6: Embeddings, Vector Databases, and Retrieval
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Overview

Understand how text is converted into embeddings and stored for efficient retrieval. Learn about vector databases, similarity search, and advanced retrieval techniques.

## Learning Objectives

- Understand embedding models and vector representations
- Compare vector databases and indexing methods
- Learn similarity metrics (cosine, dot product, Euclidean, MIPS)
- Master hybrid search, re-ranking, and retrieval evaluation

## Key Topics

### Embeddings
- What embeddings represent
- Embedding models (OpenAI, Cohere, open-source)
- Dense vs. sparse representations

### Vector Databases and Indexing
- Approximate Nearest Neighbor (ANN) algorithms
- Index types: HNSW, IVF, PQ
- Major vector databases: Pinecone, Weaviate, Qdrant, ChromaDB, Milvus, pgvector

### Similarity Metrics

| Metric | Use Case |
|:-------|:---------|
| Cosine Similarity | Most common, magnitude-invariant |
| Dot Product | When magnitude matters |
| Euclidean Distance | Geometric proximity |
| MIPS | Maximum Inner Product Search, scalable |

### Retrieval Strategies
- Dense retrieval (embedding-based)
- Sparse retrieval (BM25, TF-IDF)
- Hybrid search (combining dense + sparse)
- Metadata filtering
- Query rewriting
- HyDE (Hypothetical Document Embeddings)
- Multi-query retrieval

### Re-ranking
- Cross-encoder re-ranking
- ColBERT and late interaction models
- When to use re-ranking

### Retrieval Evaluation

{: .note }
> Good retrieval is the foundation of good RAG. Measure retrieval quality before optimizing generation.

| Metric | What It Measures |
|:-------|:-----------------|
| Precision@K | Relevance of top-K results |
| Recall@K | Coverage of relevant results |
| MRR | Rank of first relevant result |
| NDCG | Graded relevance across positions |

## Discussion Questions

- When would you use hybrid search over pure dense retrieval?
- How does re-ranking improve retrieval quality?
- What retrieval metrics matter most for your use case?

## Previous

[← Module 6: RAG Fundamentals and Document Ingestion]({% link modules/05-rag-fundamentals.md %})

## Next

[Module 8: Context Processing and Response Generation →]({% link modules/07-context-processing.md %})
