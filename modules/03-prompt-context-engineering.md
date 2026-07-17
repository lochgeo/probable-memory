---
layout: single
title: Prompt & Context Engineering
toc: true
author_profile: true
sidebar:
  nav: "docs"
---

# Module 3: Prompt Engineering and Context Engineering
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Overview

Study the principles of effective prompting, then move beyond prompts to context engineering — how enterprise AI systems assemble, prioritize, and optimize context before sending it to an LLM. This module bridges the gap between basic prompt crafting and the systematic information architecture required for production AI systems.

## Learning Objectives

- Master core prompting techniques (zero-shot through few-shot)
- Apply Chain of Thought and ReAct patterns
- Understand function calling and tool calling
- Learn context engineering principles for enterprise systems
- Grasp token budgeting and the "Lost in the Middle" problem

## Key Topics

### Prompt Engineering Techniques

Prompt engineering is the art and science of designing inputs to LLMs that elicit desired outputs. While it may seem straightforward, effective prompting requires understanding how models process information and what patterns they respond to.

#### Zero-Shot Prompting

Zero-shot prompting asks the model to perform a task without any examples. The prompt describes the task entirely through natural language:

```
Classify the following review as positive, negative, or neutral:
"This phone has an amazing camera but the battery life is terrible."
```

Zero-shot works well for straightforward tasks where the model has strong pre-training knowledge — sentiment analysis, translation, summarization, and general question answering. It breaks down for domain-specific tasks, unusual output formats, or tasks where the model's default behavior diverges from your requirements.

#### One-Shot Prompting

One-shot provides a single example of the desired input-output mapping:

```
Classify reviews as positive or negative.

Review: "Absolutely love this product!"
Sentiment: Positive

Review: "This phone has an amazing camera but the battery life is terrible."
Sentiment:
```

A single example establishes the pattern — the task, the output format, and the expected style. This is often enough for simple classification or formatting tasks.

#### Few-Shot Prompting

Few-shot provides multiple examples, typically 3–7, to establish a robust pattern:

```
Classify customer intent.

Message: "I want to return the jacket I bought yesterday"
Intent: return_request

Message: "Can you tell me if you have this in blue?"
Intent: product_inquiry

Message: "I've been waiting 2 hours for my order"
Intent: complaint

Message: "How do I apply a discount code?"
Intent:
```

Few-shot is powerful because it:
- **Demonstrates edge cases:** Multiple examples can cover variations and ambiguities.
- **Establishes format:** The model learns exactly how to structure its output.
- **Reduces ambiguity:** Clear patterns minimize misinterpretation.
- **Controls output classes:** Particularly useful for classification tasks where you need specific labels.

The main tradeoff is **context window consumption** — each example takes up tokens that could be used for the actual task or retrieved information.

#### Chain of Thought (CoT)

Chain of Thought prompting asks the model to show its reasoning process step by step. Rather than jumping directly to an answer, the model works through the problem:

```
A store has 5 boxes of apples. Each box contains 12 apples.
They sell 23 apples in the morning and 31 in the afternoon.
How many apples are left?

Let me work through this step by step:
1. Total apples: 5 boxes × 12 apples = 60 apples
2. Sold in morning: 23 apples
3. Sold in afternoon: 31 apples
4. Total sold: 23 + 31 = 54 apples
5. Remaining: 60 - 54 = 6 apples

Answer: 6 apples
```

CoT significantly improves performance on:
- **Mathematical reasoning:** Multi-step calculations.
- **Logical deduction:** Following conditional rules.
- **Complex analysis:** Breaking down multifaceted questions.
- **Code debugging:** Tracing execution step by step.

CoT works because it forces the model to externalize intermediate reasoning, making it less likely to skip steps or make arithmetic errors. However, it increases output length and latency.

#### ReAct (Reasoning + Acting)

ReAct combines reasoning with external actions in an interleaved loop. The model reasons about what it needs, takes an action (like calling a tool), observes the result, and continues reasoning:

```
Question: What is the population of the capital of France?

Thought: I need to find the capital of France first.
Action: search("capital of France")
Observation: Paris is the capital of France.

Thought: Now I need to find the population of Paris.
Action: search("population of Paris 2024")
Observation: Paris has approximately 2.1 million people in the city proper,
or 12.2 million in the metropolitan area.

Thought: I now have the answer.
Answer: The population of Paris is approximately 2.1 million (city proper)
or 12.2 million (metropolitan area).
```

ReAct is the foundation for most modern AI agent architectures, where models must decide what tools to use, when to stop and gather information, and how to integrate multiple sources into a coherent response.

#### Structured Prompting

Structured prompting explicitly specifies the output format using templates, XML tags, JSON schemas, or markdown:

```
Extract the following fields from the job posting and return as JSON:
- title
- company
- location
- salary_range (if mentioned)
- required_skills (as an array)

Job posting:
{job_text}
```

This technique is essential for production systems where LLM output feeds into downstream processing — APIs, databases, or UI components that expect specific formats. It reduces parsing errors and makes outputs more reliable.

#### Function Calling

Function calling (also called tool use) allows models to generate structured calls to external functions. Instead of producing free text, the model outputs a function name and arguments:

```json
{
  "function": "get_weather",
  "arguments": {
    "location": "Paris, France",
    "unit": "celsius"
  }
}
```

The model doesn't execute the function itself — it generates a structured request that your application code handles. This bridges the gap between natural language understanding and deterministic system operations.

#### Tool Calling

Tool calling extends function calling by providing models with a catalog of available tools and letting them decide when and how to use them. The model reasons about which tool to invoke, with what parameters, and how to incorporate the results. This is the foundation for:
- **AI assistants** that can search the web, query databases, and manage calendars.
- **Coding agents** that can read files, run code, and debug errors.
- **Customer support bots** that can look up orders, process refunds, and update account information.

### Context Engineering

{: .note }
> Context engineering is becoming one of the most important disciplines in modern AI. It goes beyond prompts to encompass how context is assembled, prioritized, and delivered to the model.

While prompt engineering focuses on crafting the *instructions*, context engineering focuses on what *information* surrounds those instructions. In enterprise systems, the model's prompt is typically a small fraction of the total context — the rest is retrieved documents, conversation history, system configuration, tool outputs, and metadata.

#### Assembling Context from Multiple Sources

In production AI systems, context is rarely a single piece of text. It's assembled from multiple heterogeneous sources:
- **System prompts:** Role definition, behavioral instructions, guardrails.
- **User messages:** The current query and conversation history.
- **Retrieved documents:** RAG results from vector search or keyword search.
- **Tool outputs:** Results from API calls, database queries, or web searches.
- **Metadata:** Timestamps, user profiles, session information.
- **Knowledge base entries:** Curated facts, procedures, or policies.

The challenge is integrating these diverse sources into a coherent, well-organized context that helps the model produce the best possible response.

#### Prioritizing and Filtering Relevant Information

Not all retrieved information is equally useful. Context engineering involves:
- **Relevance scoring:** Ranking retrieved chunks by semantic similarity or other relevance signals.
- **Deduplication:** Removing overlapping or redundant information.
- **Freshness weighting:** Prioritizing more recent information when time-sensitivity matters.
- **Source authority:** Weighting trusted sources more heavily.
- **Conflict resolution:** When sources disagree, deciding which to prioritize or how to present the disagreement.

#### Compressing and Ranking Context

Context windows are finite, and stuffing too much information degrades performance. Compression techniques include:
- **Summarization:** Condensing retrieved documents into key points.
- **Extractive selection:** Keeping only the most relevant sentences or paragraphs.
- **Hierarchical aggregation:** Summarizing at multiple levels of detail.
- **Progressive disclosure:** Providing brief answers with links to detailed sources.

#### Token Budgeting Strategies

Token budgeting allocates limited context window space across different content types:

```
Total context window: 128,000 tokens

Reserved:
- System prompt:        ~2,000 tokens
- Conversation history: ~20,000 tokens (last 10 turns)
- Retrieved context:    ~50,000 tokens (up to 20 chunks)
- Current user query:   ~500 tokens
- Response buffer:      ~4,000 tokens
- Safety margin:        ~1,000 tokens

Available for retrieved content: ~50,000 tokens
```

Effective budgeting ensures that the most important information (system instructions, recent conversation, relevant retrieval) gets priority, while less critical content is summarized or omitted.

#### Long-Context Models and Their Tradeoffs

Modern models support very large context windows (128K–1M tokens), which might seem to eliminate the need for careful context engineering. However, long context comes with tradeoffs:
- **Cost:** More tokens = higher API costs. Processing 128K tokens costs significantly more than 8K.
- **Latency:** Larger contexts take longer to process, both in prefill and generation.
- **Quality degradation:** Models can struggle to maintain coherence across very long contexts, even with large context windows.
- **Diminishing returns:** More context doesn't always mean better performance — the model still needs to find the relevant information within a larger haystack.

#### The "Lost in the Middle" Problem

Research has shown that LLMs struggle to attend to information placed in the middle of a long context. Performance is highest for information at the beginning and end of the context, with a notable dip for content in the middle. This has significant implications for RAG system design:

- **Front-load critical information:** Place the most important retrieved content at the beginning of the context.
- **Avoid burying key facts:** Don't place essential information in the middle of a long block of retrieved text.
- **Use recency to your advantage:** Recent conversation turns and the most relevant documents should appear near the end.
- **Test empirically:** The severity of this effect varies by model — test with your specific model and context patterns.

### Prompt vs. Context Engineering

| Aspect | Prompt Engineering | Context Engineering |
|:-------|:-------------------|:--------------------|
| Scope | Single prompt design | Full context pipeline |
| Focus | How you ask | What information is provided |
| Challenge | Clever wording | Information architecture |
| Scale | Per-interaction | System-wide |

In practice, production AI systems require both. A well-engineered prompt is wasted if the context around it is poorly assembled. Conversely, perfect context is ineffective if the prompt doesn't guide the model on how to use it. The most effective systems treat prompt engineering and context engineering as complementary disciplines — prompts define the *task*, and context engineering ensures the model has the *information* it needs to succeed.

## Discussion Questions

- How does the "Lost in the Middle" problem affect RAG system design?
- When is Chain of Thought prompting most effective?
- How would you design a token budgeting strategy for a customer support bot?

## Previous

[← Module 2: The LLM Training Lifecycle]({% link modules/02-llm-training-lifecycle.md %})

## Next

[Module 4: LLMs and the AI Ecosystem →]({% link modules/04-llm-ecosystem.md %})
