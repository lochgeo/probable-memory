---
layout: single
title: RAG Fundamentals & Document Ingestion
toc: true
author_profile: true
sidebar:
  nav: "docs"
---

# Module 5: RAG Fundamentals and Document Ingestion
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Overview

Learn the complete Retrieval-Augmented Generation architecture and why RAG has become the standard approach for grounding LLMs in enterprise knowledge.

## Learning Objectives

- Understand the full RAG pipeline architecture
- Master document ingestion for various file formats
- Compare chunking strategies and know when to use each
- Learn metadata extraction and document enrichment

## Key Topics

### RAG Architecture

{: .note }
> RAG has become the standard approach for enterprise AI because it grounds LLM responses in actual organizational knowledge without requiring model retraining.

```
User Query → Retrieval → Context Assembly → LLM → Grounded Response
     ↑                                           |
     └───────────── Knowledge Base ──────────────┘
```

### Document Ingestion Pipeline
Supported formats:
- PDFs (text and scanned)
- Word documents (.docx)
- Presentations (.pptx)
- HTML and Markdown
- Emails
- OCR documents
- Images (multimodal)

### Chunking Strategies

| Strategy | Description | Best For |
|:---------|:------------|:---------|
| Fixed-length | Split every N tokens | Simple, predictable |
| Sliding window | Overlapping fixed chunks | Preserving context |
| Page-based | One chunk per page | Structured documents |
| Paragraph | Split on paragraph boundaries | Natural language text |
| Recursive | Split on multiple delimiters | General purpose |
| Semantic | Split on topic changes | High-quality retrieval |
| Hierarchical | Parent-child chunk relationships | Multi-scale retrieval |
| LLM-assisted | Use LLM to determine boundaries | Complex documents |

### Metadata and Enrichment
- Extracting metadata (author, date, section)
- Document enrichment techniques
- Parent-child document relationships

## Discussion Questions

- How does chunk size affect retrieval quality?
- When would you use semantic chunking vs. recursive chunking?
- What metadata is most valuable for enterprise document retrieval?

## Previous

[← Module 5: LLMs and the AI Ecosystem]({% link modules/04-llm-ecosystem.md %})

## Next

[Module 7: Embeddings, Vector Databases, and Retrieval →]({% link modules/06-embeddings-retrieval.md %})
