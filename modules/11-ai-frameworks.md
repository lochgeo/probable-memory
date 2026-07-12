---
layout: default
title: AI Frameworks & Development Ecosystem
parent: Day 2 – Building AI Applications
nav_order: 7
---

# Module 11: AI Frameworks and Development Ecosystem
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Overview

Gain an understanding of the major frameworks used for building AI applications and agentic systems, and learn where each fits.

## Learning Objectives

- Compare major AI frameworks and their philosophies
- Understand when to use each framework
- Evaluate tradeoffs between simplicity and flexibility

## Key Topics

### Framework Comparison

| Framework | Focus | Best For |
|:----------|:------|:---------|
| LangChain | Chain-based composition | General-purpose LLM apps |
| LangGraph | Stateful, cyclic workflows | Complex agent architectures |
| Google ADK | Google ecosystem integration | Gemini-based applications |
| CrewAI | Role-based multi-agent | Team-based agent workflows |
| AutoGen | Microsoft's multi-agent | Research and enterprise agents |
| PydanticAI | Type-safe, Pydantic-based | Structured AI applications |
| Semantic Kernel | Microsoft enterprise | Enterprise .NET/Python apps |
| OpenAI Agents SDK | OpenAI ecosystem | OpenAI model-based agents |

### Selection Criteria

{: .note }
> No single framework fits all use cases. Consider your team's expertise, ecosystem preferences, and application requirements.

- **Simplicity vs. Flexibility**: Some frameworks are batteries-included, others are more modular
- **Community and Support**: Maturity, documentation, and community size
- **Ecosystem Integration**: Compatibility with your existing tools and services
- **Production Readiness**: Monitoring, testing, and deployment support
- **Model Agnosticism**: Support for multiple LLM providers

### Emerging Trends
- Model Context Protocol (MCP) adoption
- Agent-to-Agent (A2A) communication
- Framework convergence and interoperability
- Shift toward simpler, more composable tools

## Discussion Questions

- If you were building a customer support agent today, which framework would you choose and why?
- How do you evaluate framework maturity for production use?
- What role do protocols like MCP play in framework evolution?

## Previous

[← Module 13: Tool Calling, Agent Communication, and Multi-Agent Systems]({% link modules/10-tool-calling-multi-agent.md %})

## Next

[Module 15: Advanced Retrieval and Modern RAG →]({% link modules/12-advanced-retrieval.md %})
