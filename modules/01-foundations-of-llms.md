---
layout: single
title: Foundations of Generative AI
toc: true
author_profile: true
sidebar:
  nav: "docs"
---

# Module 1: Foundations of Generative AI
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Overview

Begin by understanding the evolution from Artificial Intelligence to Machine Learning, Deep Learning, and finally Generative AI. Learn how transformer models work at a conceptual level, including the attention mechanism, tokenization, embeddings, and next-token prediction. This module establishes the conceptual foundation for everything that follows in this course.

## Learning Objectives

- Trace the evolution from AI → ML → Deep Learning → Generative AI
- Understand transformer architecture fundamentals
- Grasp key concepts: attention, tokenization, embeddings, positional encoding
- Understand context windows and next-token prediction
- Explain why LLMs hallucinate and what reasoning means in an LLM
- Recognize the limitations of relying solely on parametric knowledge

## Key Topics

### The AI Evolution

Artificial Intelligence is a broad field concerned with creating systems that can perform tasks requiring human-like intelligence. Machine Learning is a subset of AI where systems learn patterns from data rather than being explicitly programmed. Deep Learning is a subset of ML that uses neural networks with many layers to learn hierarchical representations. Generative AI is the latest evolution — systems that can create new content (text, images, code, audio) rather than just classifying or predicting.

Each paradigm builds on the previous one:

- **AI (1950s–2000s):** Rule-based systems, expert systems, search algorithms. Programs followed hand-crafted rules.
- **Machine Learning (1990s–2010s):** Statistical learning from data. Algorithms like decision trees, SVMs, and random forests. Required feature engineering by domain experts.
- **Deep Learning (2010s):** Neural networks with many layers learn features automatically from raw data. Breakthroughs in image recognition (AlexNet, 2012), speech (WaveNet, 2016), and translation.
- **Generative AI (2020s):** Models that generate new content. GPT-3 (2020) demonstrated that large language models could produce human-quality text. ChatGPT (2022) brought generative AI to mainstream adoption.

Generative AI represents a fundamental shift because it moves from *discriminative* models (classifying inputs) to *generative* models (producing outputs). A classifier answers "which category does this belong to?" while a generative model answers "what should come next?"

### Transformer Architecture

The transformer, introduced in the 2017 paper *"Attention Is All You Need"* by Vaswani et al., is the architecture behind virtually all modern LLMs. Understanding it at a conceptual level is essential for working with AI systems.

#### Self-Attention Mechanism

Self-attention is the core innovation of the transformer. It allows each token in a sequence to attend to every other token, computing a relevance score for each pair. This gives the model a way to understand relationships between words regardless of their distance in the text.

For example, in the sentence *"The cat sat on the mat because it was tired,"* self-attention helps the model determine that "it" refers to "cat" rather than "mat." The mechanism computes three vectors for each token — a **query** (what am I looking for?), a **key** (what do I contain?), and a **value** (what do I provide?) — and uses dot-product attention to determine how much each token should attend to every other token.

Multi-head attention runs this process in parallel across multiple "heads," allowing the model to capture different types of relationships simultaneously — one head might track syntactic structure while another tracks semantic similarity.

#### Tokenization and Embeddings

Before processing, text is broken into **tokens** — subword units. Modern tokenizers like BPE (Byte-Pair Encoding) split common words into single tokens and rare words into multiple subword pieces. For example, "understanding" might become ["under", "stand", "ing"]. This allows the model to handle any text, including words it hasn't seen before.

Each token is then converted into an **embedding** — a high-dimensional vector (e.g., 4096 numbers) that captures the token's meaning. Similar words have similar embeddings. The embedding space encodes syntactic and semantic relationships: vectors for king/queen,Paris/France, running/jogging form analogous patterns.

#### Positional Encoding

Unlike recurrent networks, transformers process all tokens in parallel, which means they have no inherent sense of word order. **Positional encoding** injects position information into the embeddings so the model knows that "dog bites man" is different from "man bites dog." Modern transformers use techniques like RoPE (Rotary Position Embeddings) or ALiBi to encode position.

#### Context Windows

The **context window** (or context length) is the maximum number of tokens a model can process in a single forward pass. Early GPT models had context windows of ~2K tokens. Modern models support 128K, 200K, or even 1M tokens. Everything the model "sees" — the prompt, retrieved documents, conversation history — must fit within this window.

#### Next-Token Prediction

At its core, an LLM is a next-token prediction machine. Given a sequence of tokens, it predicts the probability distribution over the next token. During training, the model learns to minimize the difference between its predictions and the actual next tokens in the training data. This deceptively simple objective — predicting the next word — turns out to require learning grammar, facts, reasoning patterns, and world knowledge.

### Understanding LLM Behavior

#### What Hallucination Means and Why It Happens

**Hallucination** refers to an LLM generating content that is fluent and plausible but factually incorrect or fabricated. The model might confidently state a false fact, invent a citation, or describe something that never happened.

Hallucinations occur because LLMs optimize for *statistical plausibility*, not *truthfulness*. The training process teaches the model to produce text that looks like its training data, not text that is verifiably correct. When the model encounters a query where its training data is sparse or ambiguous, it fills in gaps with statistically likely but potentially false completions.

Common causes include:
- **Training data gaps:** The model hasn't seen reliable information about a topic and generates plausible-sounding but incorrect content.
- **Ambiguous queries:** The model interprets a vague question in an unexpected way.
- **Overconfidence:** LLMs don't have a built-in "I don't know" mechanism. They will attempt to answer any question with equal confidence.
- **Distribution shift:** The model generates content for distributions not well-represented in training data.

#### Reasoning in LLMs

Modern LLMs can perform multi-step reasoning — breaking down complex problems into intermediate steps. This includes mathematical reasoning, logical deduction, and chain-of-thought problem solving. However, this reasoning is *pattern-based* rather than *symbolic*. The model has learned reasoning patterns from training data but doesn't have a formal logic engine underneath.

This distinction matters: LLMs can solve many reasoning problems reliably, but they can fail on novel reasoning patterns or problems that require precise multi-step logic, especially as step count increases.

#### Parametric Knowledge vs. External Knowledge

An LLM's **parametric knowledge** is the information encoded in its weights during training. This knowledge is:
- **Static:** Frozen at training time. It doesn't update as the world changes.
- **Opaque:** You can't query it directly or know exactly what it contains.
- **Implicit:** Facts are distributed across billions of parameters, not stored as discrete records.

**External knowledge** comes from augmenting the model at inference time — providing relevant documents, database lookups, API responses, or search results as part of the prompt. This approach (which leads to RAG, covered later) provides:
- **Dynamic information:** Up-to-date facts from external sources.
- **Verifiability:** Citations and source documents that can be checked.
- **Control:** The ability to determine exactly what information the model has access to.

#### Limitations of Standalone LLMs

LLMs used without augmentation have several practical limitations:
- **Knowledge cutoff:** They cannot know about events after their training date.
- **No access to private data:** They don't have access to your organization's documents, databases, or APIs.
- **Hallucination risk:** Without grounding, fabricated content goes undetected.
- **No computation:** They can't perform real-time calculations, look up current prices, or execute code.
- **No memory:** Each conversation starts fresh without persistence (unless managed externally).

These limitations are precisely what the rest of this course addresses — through prompt engineering, RAG, agentic systems, and enterprise architecture.

## Discussion Questions

- Why has the transformer architecture become the dominant paradigm?
- What are the practical implications of LLM hallucinations in production systems?
- When would you rely on parametric knowledge vs. external retrieval?

## Next

[Module 2: The LLM Training Lifecycle →]({% link modules/02-llm-training-lifecycle.md %})
