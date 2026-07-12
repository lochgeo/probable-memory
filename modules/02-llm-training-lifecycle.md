---
layout: default
title: The LLM Training Lifecycle
parent: Day 1 – Foundations of LLMs and RAG
nav_order: 2
---

# Module 2: The LLM Training Lifecycle
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Overview

Explore how large language models are created and refined. Understand the full training pipeline from pre-training to alignment and fine-tuning techniques.

## Learning Objectives

- Understand the pre-training process and its data requirements
- Learn post-training techniques: instruction tuning, SFT, RLHF, RLAIF
- Compare fine-tuning approaches: LoRA, QLoRA, PEFT, distillation, quantization
- Know when fine-tuning is preferable to RAG

## Key Topics

### Pre-training
- Training on massive datasets
- Language modeling objectives
- Compute requirements and scaling laws

### Post-training and Alignment
- Instruction tuning
- Supervised Fine-Tuning (SFT)
- Reinforcement Learning from Human Feedback (RLHF)
- Reinforcement Learning from AI Feedback (RLAIF)
- Alignment techniques

### Fine-tuning Approaches
- LoRA (Low-Rank Adaptation)
- QLoRA (Quantized LoRA)
- Parameter-Efficient Fine-Tuning (PEFT)
- Model distillation
- Quantization

### Fine-tuning vs. RAG

{: .note }
> A common decision point: when to fine-tune a model vs. when to use RAG. Fine-tuning modifies the model's knowledge, while RAG augments its context at inference time.

| Approach | Best For |
|:---------|:---------|
| Fine-tuning | Domain-specific language, style, format |
| RAG | Dynamic knowledge, up-to-date information |
| Both | Domain adaptation + current knowledge |

## Discussion Questions

- What factors drive the decision between fine-tuning and RAG?
- How does RLHF improve model behavior compared to SFT alone?
- What are the cost tradeoffs between full fine-tuning and LoRA?

## Previous

[← Module 1: Foundations of Generative AI]({% link modules/01-foundations-of-llms.md %})

## Next

[Module 3: Prompt Engineering and Context Engineering →]({% link modules/03-prompt-context-engineering.md %})
