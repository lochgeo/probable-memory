---
layout: default
title: Prompt & Context Engineering
parent: Day 1 – Foundations of LLMs and RAG
nav_order: 3
---

# Module 3: Prompt Engineering and Context Engineering
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Overview

Study the principles of effective prompting, then move beyond prompts to context engineering — how enterprise AI systems assemble, prioritize, and optimize context before sending it to an LLM.

## Learning Objectives

- Master core prompting techniques (zero-shot through few-shot)
- Apply Chain of Thought and ReAct patterns
- Understand function calling and tool calling
- Learn context engineering principles for enterprise systems
- Grasp token budgeting and the "Lost in the Middle" problem

## Key Topics

### Prompt Engineering Techniques
- Zero-shot prompting
- One-shot prompting
- Few-shot prompting
- Chain of Thought (CoT)
- ReAct (Reasoning + Acting)
- Structured prompting
- Function calling
- Tool calling

### Context Engineering
{: .note }
> Context engineering is becoming one of the most important disciplines in modern AI. It goes beyond prompts to encompass how context is assembled, prioritized, and delivered to the model.

- Assembling context from multiple sources
- Prioritizing and filtering relevant information
- Compressing and ranking context
- Token budgeting strategies
- Long-context models and their tradeoffs
- The "Lost in the Middle" problem

### Prompt vs. Context Engineering

| Aspect | Prompt Engineering | Context Engineering |
|:-------|:-------------------|:--------------------|
| Scope | Single prompt design | Full context pipeline |
| Focus | How you ask | What information is provided |
| Challenge | Clever wording | Information architecture |
| Scale | Per-interaction | System-wide |

## Discussion Questions

- How does the "Lost in the Middle" problem affect RAG system design?
- When is Chain of Thought prompting most effective?
- How would you design a token budgeting strategy for a customer support bot?

## Previous

[← Module 2: The LLM Training Lifecycle]({% link modules/02-llm-training-lifecycle.md %})

## Next

[Module 4: LLMs and the AI Ecosystem →]({% link modules/04-llm-ecosystem.md %})
