---
layout: default
title: Evaluation and Testing
parent: Day 2 – Building AI Applications
nav_order: 2
---

# Module 9: Evaluation and Testing
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Overview

Learn how to systematically evaluate LLM outputs, RAG pipelines, and agent performance. Master the tools and frameworks that make AI systems measurable and reliable.

## Learning Objectives

- Design evaluation strategies for LLM applications
- Measure RAG quality (faithfulness, relevance, context accuracy)
- Evaluate agent task completion and tool usage
- Use evaluation frameworks in practice

## Key Topics

### LLM Evaluation

{: .note }
> You can't improve what you can't measure. Evaluation is the foundation of reliable AI — it turns subjective quality into objective metrics.

| Method | Description | When to Use |
|:-------|:------------|:------------|
| LLM-as-Judge | Use a strong model to grade outputs | Scalable, versatile |
| Human Evaluation | Expert review of outputs | Gold standard, expensive |
| Automated Metrics | BLEU, ROUGE, BERTScore | Quick baseline |
| Task-Based | Measure end task success | Real-world validation |

### RAG Evaluation

| Metric | What It Measures |
|:-------|:-----------------|
| Context Precision | Are retrieved chunks relevant? |
| Context Recall | Are all relevant chunks found? |
| Faithfulness | Is the answer grounded in context? |
| Answer Relevance | Does the answer address the question? |

### Agent Evaluation
- Task completion rate
- Tool usage accuracy
- Step efficiency
- Error recovery
- Cost per task

### Evaluation Frameworks

| Framework | Focus |
|:----------|:------|
| RAGAS | RAG pipeline evaluation |
| DeepEval | End-to-end LLM evaluation |
| LangSmith | Tracing, evaluation, monitoring |
| Phoenix (Arize) | Observability and evaluation |
| promptfoo | Prompt testing and red-teaming |

### Building Evaluation Pipelines
- Golden dataset creation and maintenance
- Automated evaluation on every deployment
- Continuous evaluation in production
- Drift detection and alerting

## Discussion Questions

- How do you create a golden evaluation dataset for a new domain?
- When would you use LLM-as-Judge vs. human evaluation?
- How do you evaluate an agent that interacts with real external systems?

## Previous

[← Module 8: Context Processing and Response Generation]({% link modules/07-context-processing.md %})

## Next

[Module 10: Memory and State Management →]({% link modules/memory-state.md %})
