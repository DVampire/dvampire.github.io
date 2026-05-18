---
layout: post
title: "AgentOrchestra: Hierarchical Multi-Agent Orchestration with the TEA Protocol"
date: 2025-06-14
description: We propose the Tool-Environment-Agent (TEA) protocol and AgentOrchestra, a hierarchical multi-agent framework that achieves 89.04% on GAIA — state-of-the-art on general-purpose agent benchmarks.
tags: [LLM Agents, Multi-Agent Systems, Benchmarks]
---

We introduce **AgentOrchestra**, a hierarchical multi-agent framework built on the **Tool-Environment-Agent (TEA) protocol**, achieving **89.04% on GAIA** — establishing state-of-the-art performance on general-purpose agent benchmarks.

## The Problem with Existing Multi-Agent Systems

Current LLM-based multi-agent systems suffer from a common structural weakness: environments, agents, and tools are treated as second-class citizens — wired together in ad-hoc, brittle ways with no formal lifecycle management or versioned interfaces. This makes systems fragile, hard to debug, and difficult to scale.

## The TEA Protocol

The **Tool-Environment-Agent (TEA) protocol** addresses this by treating all three components as **first-class resources** with:

- **Explicit lifecycles** — resources are created, activated, suspended, and terminated through well-defined state machines
- **Versioned interfaces** — every resource exposes a typed, versioned contract, enabling safe composition and substitution
- **Unified resource substrate** — a shared layer that manages resource registration, discovery, and communication

This design directly parallels lessons from operating systems and microservice architectures: stable, composable abstractions are the foundation of reliable complex systems.

## AgentOrchestra Architecture

AgentOrchestra builds on TEA with a hierarchical structure:

- **Central Planner** — decomposes complex tasks into sub-goals and dynamically assigns them to specialist sub-agents
- **Specialist Sub-Agents** — independently handle focused domains: web navigation, data analysis, file operations, code execution
- **Resource Manager** — enforces TEA protocol contracts, handles agent spawning/teardown, and monitors resource health

The central planner operates at the task level; sub-agents operate at the action level. This separation of concerns enables parallelism while maintaining coherent task-level reasoning.

## GAIA Benchmark Results

GAIA is a challenging benchmark requiring real-world tool use, multi-step reasoning, and web interaction across hundreds of diverse tasks.

| System | GAIA Score |
|--------|-----------|
| AgentOrchestra | **89.04%** |
| Previous SOTA | < 89% |

AgentOrchestra achieves state-of-the-art performance, demonstrating that principled protocol design — not just model scale — is a key driver of agent capability.

## Links

- **Paper**: [arXiv:2506.12508](https://arxiv.org/abs/2506.12508)
