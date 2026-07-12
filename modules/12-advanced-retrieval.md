---
layout: single
title: Advanced Retrieval & Modern RAG
toc: true
author_profile: true
sidebar:
  nav: "docs"
---

# Module 12: Advanced Retrieval and Modern RAG
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Overview

Explore the latest advances beyond traditional RAG architectures, including agentic retrieval, graph-based approaches, and multimodal patterns.

## Learning Objectives

- Understand modern RAG variants and when to use each
- Learn about Agentic RAG, Self-RAG, and Corrective RAG
- Explore GraphRAG and knowledge graph integration
- Understand multimodal and SQL-based retrieval

## Key Topics

### Advanced RAG Patterns

| Pattern | Description |
|:--------|:------------|
| Agentic RAG | Agent-driven retrieval with reasoning |
| Self-RAG | Model decides when to retrieve |
| Corrective RAG (CRAG) | Self-critique and retrieval correction |
| Adaptive RAG | Dynamic strategy selection based on query |

### Graph-Based RAG

{: .note }
> GraphRAG combines the structured relationships of knowledge graphs with the flexibility of vector-based retrieval, enabling more nuanced and connected answers.

- GraphRAG architecture
- Knowledge Graph RAG
- Entity and relationship extraction
- Graph traversal for retrieval

### Specialized RAG Patterns
- **Multimodal RAG**: Text, images, audio, video
- **SQL RAG**: Natural language to database queries
- **API-based retrieval**: Real-time data from APIs
- **Tool-augmented retrieval**: Using tools during retrieval
- **Long-context retrieval**: Leveraging large context windows

### Emerging Approaches
- Vectorless retrieval
- Markdown-first knowledge bases
- Repository-aware retrieval
- Structured knowledge files
- Hybrid lexical-semantic search

### Choosing the Right Pattern

| Need | Recommended Pattern |
|:-----|:--------------------|
| Up-to-date information | Agentic RAG |
| Complex multi-hop questions | GraphRAG |
| Structured data queries | SQL RAG |
| Image understanding | Multimodal RAG |
| Simple Q&A | Traditional RAG with re-ranking |

## Discussion Questions

- When would GraphRAG provide better answers than vector-based RAG?
- How does Self-RAG reduce unnecessary retrieval calls?
- What challenges does multimodal RAG introduce?

## Previous

[← Module 14: AI Frameworks and Development Ecosystem]({% link modules/11-ai-frameworks.md %})

## Next

[Module 16: AI Applications: Streaming and Real-time →]({% link modules/streaming-realtime.md %})
