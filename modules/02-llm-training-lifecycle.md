---
layout: single
title: The LLM Training Lifecycle
toc: true
author_profile: true
sidebar:
  nav: "docs"
---

# Module 2: The LLM Training Lifecycle
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Overview

Explore how large language models are created and refined. Understand the full training pipeline from pre-training to alignment and fine-tuning techniques. This module covers the economics, techniques, and tradeoffs involved in building and customizing LLMs for specific use cases.

## Learning Objectives

- Understand the pre-training process and its data requirements
- Learn post-training techniques: instruction tuning, SFT, RLHF, RLAIF
- Compare fine-tuning approaches: LoRA, QLoRA, PEFT, distillation, quantization
- Know when fine-tuning is preferable to RAG

## Key Topics

### Pre-training

Pre-training is the foundational phase where a language model learns to predict the next token across a massive corpus of text. This is where the model acquires its broad knowledge of language, facts, reasoning patterns, and world knowledge.

#### Training on Massive Datasets

Pre-training datasets contain trillions of tokens sourced from:
- **Web crawls:** Common Crawl, C4, FineWeb — billions of web pages covering every topic imaginable.
- **Books:** Open-source book corpora, academic textbooks, and published works.
- **Code:** GitHub repositories, Stack Overflow, documentation sites — teaching the model programming patterns and technical language.
- **Wikipedia and reference sources:** Structured, high-quality factual content.

Data quality matters enormously. Pre-training pipelines include extensive filtering: removing low-quality text, deduplicating near-identical documents, filtering for toxicity, and balancing topic distribution. The *quality* of training data often matters more than sheer volume.

#### Language Modeling Objectives

The primary training objective is **next-token prediction** (causal language modeling). The model sees a sequence of tokens and learns to predict what comes next. From this single objective, the model learns:
- **Syntax and grammar:** Which word forms follow which.
- **Semantics:** What words mean in context.
- **Factual knowledge:** Information contained in the training text.
- **Reasoning patterns:** How to chain logical steps.
- **Code patterns:** Programming syntax and logic.

Some models also use **masked language modeling** (predicting blanked-out words, as in BERT) or **denoising objectives** (corrupted text reconstruction), though next-token prediction dominates for generative models.

#### Compute Requirements and Scaling Laws

Pre-training is extraordinarily expensive. Training GPT-4 is estimated to have cost over $100 million in compute alone. **Scaling laws** describe the relationship between compute budget, dataset size, model size, and performance. Key insights from the Chinchilla paper (2022):
- For a fixed compute budget, there is an optimal balance between model size and training data.
- Under-trained large models can be outperform by smaller models trained on more data.
- Performance improves predictably with more compute, following power-law relationships.

Practically, this means modern LLM training requires thousands of GPUs running for weeks or months, with careful engineering around distributed training, mixed-precision arithmetic, checkpointing, and fault tolerance.

### Post-training and Alignment

Pre-training produces a powerful but unaligned model. It can predict the next token accurately, but it doesn't know how to be a helpful assistant. Post-training aligns the model's behavior with human preferences and intended use.

#### Instruction Tuning

Instruction tuning is the first step in post-training. The model is fine-tuned on a dataset of (instruction, response) pairs — teaching it to follow directions rather than just continue text. For example, instead of just predicting the next token after "What is the capital of France?", the model learns to produce "The capital of France is Paris" as a complete, helpful response.

#### Supervised Fine-Tuning (SFT)

SFT extends instruction tuning with higher-quality, human-curated examples. Human annotators write ideal responses to various prompts, and the model learns to mimic these demonstrations. SFT teaches the model:
- **Format:** How to structure responses (paragraphs, lists, code blocks).
- **Tone:** Professional, helpful, concise.
- **Scope:** When to answer, when to decline, when to ask for clarification.
- **Accuracy:** Correct facts and reasoning patterns.

The quality of SFT data is critical — research shows that smaller, higher-quality datasets often outperform larger, noisier ones.

#### Reinforcement Learning from Human Feedback (RLHF)

RLHF takes alignment further by learning from *comparative* human judgments rather than absolute demonstrations. The process works in three steps:

1. **Collect comparison data:** Humans rank multiple model responses from best to worst.
2. **Train a reward model:** A separate model learns to predict which response humans would prefer.
3. **Optimize with PPO:** The LLM is fine-tuned using Proximal Policy Optimization to maximize the reward model's score, while staying close to the original model (via a KL-divergence penalty) to avoid degeneration.

RLHF addresses limitations of SFT: it's easier for humans to *rank* responses than to write perfect examples, and it captures subtle preferences (helpfulness, safety, nuance) that are hard to demonstrate.

#### Reinforcement Learning from AI Feedback (RLAIF)

RLAIF replaces some or all human feedback with AI-generated feedback. A larger, more capable model (like GPT-4) evaluates and ranks responses from the model being trained. This:
- **Scales feedback:** AI feedback is cheaper and faster than human annotation.
- **Reduces bottleneck:** Human annotators become the limiting factor in RLHF.
- **Introduces risk:** The AI judge inherits its own biases and may not capture all human preferences.

Many production models use a combination of RLHF and RLAIF, with human feedback for critical areas (safety, accuracy) and AI feedback for broader coverage.

#### Alignment Techniques

Modern alignment combines multiple approaches:
- **Constitutional AI (Anthropic):** The model self-critiques and revises its responses based on a set of principles.
- **DPO (Direct Preference Optimization):** A simpler alternative to RLHF that directly optimizes the model on preference pairs without training a separate reward model.
- **RLVR (RL with Verifiable Rewards):** Using rule-based verification (e.g., math answer checking) as reward signals instead of learned reward models.

### Fine-tuning Approaches

After base model training and alignment, organizations can further customize models for specific domains or tasks. Several techniques exist, ranging from full model retraining to lightweight adaptations.

#### LoRA (Low-Rank Adaptation)

LoRA dramatically reduces the cost of fine-tuning by freezing the original model weights and training only small, low-rank decomposition matrices added to each transformer layer. Instead of updating billions of parameters, you train millions.

Key properties:
- **Memory efficiency:** Requires a fraction of the GPU memory of full fine-tuning.
- **Training speed:** Much faster — hours instead of days.
- **Modularity:** Multiple LoRA adapters can be trained for different tasks and swapped in/out at inference time.
- **Minimal quality loss:** Research shows LoRA achieves performance close to full fine-tuning for most tasks.

#### QLoRA (Quantized LoRA)

QLoRA extends LoRA by quantizing the base model to 4-bit precision before applying LoRA adapters. This further reduces memory requirements, making fine-tuning possible on consumer GPUs (e.g., a single 24GB GPU for a 7B model). The technique combines:
- **NF4 quantization:** A 4-bit data type optimized for normally distributed weights.
- **Double quantization:** Quantizing the quantization constants themselves.
- **Paged optimizers:** Offloading optimizer states to CPU when GPU memory is insufficient.

#### Parameter-Efficient Fine-Tuning (PEFT)

PEFT is the umbrella term for techniques that update only a small subset of parameters. Beyond LoRA, PEFT methods include:
- **Prefix tuning:** Adding learnable "prefix" vectors to the model's inputs.
- **Prompt tuning:** Learning continuous prompt embeddings that guide the frozen model.
- **Adapter layers:** Small neural network modules inserted between transformer layers.
- **IA3:** Learning rescaling vectors for keys, values, and activations.

The choice depends on the specific task, available compute, and whether you need task-specific adapters that can be swapped.

#### Model Distillation

Distillation trains a smaller "student" model to mimic a larger "teacher" model. The student learns from the teacher's soft probability distributions (not just hard labels), capturing nuanced knowledge. Benefits include:
- **Deployment efficiency:** Smaller models require less compute and memory for inference.
- **Cost reduction:** Dramatically lowers inference costs at scale.
- **Latency:** Faster response times for user-facing applications.

#### Quantization

Quantization reduces model precision from 16-bit or 32-bit floating point to 8-bit, 4-bit, or even lower. This is an inference-time optimization that reduces memory and compute requirements:
- **INT8 quantization:** Roughly halves memory with minimal quality loss.
- **INT4 quantization:** Further reduction, with some tradeoff in output quality.
- **GPTQ/AWQ:** Post-training quantization methods optimized for LLMs.

### Fine-tuning vs. RAG

{: .note }
> A common decision point: when to fine-tune a model vs. when to use RAG. Fine-tuning modifies the model's knowledge, while RAG augments its context at inference time.

| Approach | Best For |
|:---------|:---------|
| Fine-tuning | Domain-specific language, style, format |
| RAG | Dynamic knowledge, up-to-date information |
| Both | Domain adaptation + current knowledge |

Additional considerations:
- **Fine-tuning cost:** Requires GPU compute for training, plus data collection and annotation. One-time cost, but ongoing as the model needs updates.
- **RAG cost:** Requires vector database infrastructure, embedding generation, and retrieval pipeline. Ongoing operational cost that scales with usage.
- **Latency:** Fine-tuned models have no retrieval overhead. RAG adds latency from the retrieval step.
- **Data privacy:** Fine-tuning embeds knowledge into weights (harder to audit). RAG uses external documents that can be traced and controlled.
- **Freshness:** Fine-tuned models reflect training-time knowledge. RAG can access real-time information.

In practice, many production systems use **both** — fine-tuning for domain adaptation and style, combined with RAG for current, verifiable knowledge.

## Discussion Questions

- What factors drive the decision between fine-tuning and RAG?
- How does RLHF improve model behavior compared to SFT alone?
- What are the cost tradeoffs between full fine-tuning and LoRA?

## Previous

[← Module 1: Foundations of Generative AI]({% link modules/01-foundations-of-llms.md %})

## Next

[Module 3: Prompt Engineering and Context Engineering →]({% link modules/03-prompt-context-engineering.md %})
