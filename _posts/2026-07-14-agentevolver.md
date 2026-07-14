---
layout: post
title: "AgentEvolver: A Self-Evolving Agent Operating System"
date: 2026-07-14
description: We introduce AgentEvolver, a self-evolving multi-agent operating system where a MetaAgent orchestrates specialist sub-agents over an Agent Bus, while generator, evaluator, and optimizer agents continuously improve the tool, skill, and agent ecosystem at runtime.
tags: [LLM Agents, Self-Evolution, Agent Operating System, Multi-Agent]
---

We introduce **AgentEvolver** ([project page](https://dvampire.github.io/AgentEvolver/) · [GitHub](https://github.com/DVampire/AgentEvolver)) — a **self-evolving agent operating system**. A central **MetaAgent** orchestrates specialist sub-agents to complete user tasks, while a set of *meta-level* agents — generators, evaluators, and optimizers — continuously improve the system's tools, skills, and agents themselves. The design keeps an **immutable core** while making everything around it — components registered through 10+ registries — hot-pluggable and evolvable.

## From Static Agents to a Living System

Most agent frameworks ship a fixed set of capabilities: a hand-written prompt, a curated toolbox, a static set of sub-agents. Whatever the developer wired up at design time is exactly what the system can do forever. As tasks diversify, this rigidity becomes the bottleneck — every new capability requires a human to write another tool, another prompt, another agent.

AgentEvolver takes a different stance: **treat the agent stack as an operating system that can rewrite its own userland.** Tools, skills, and agents are not fixed binaries — they are resources the system can observe, evaluate, and regenerate as it runs. The result is an ecosystem that grows more capable through use, not through releases.

## Architecture

AgentEvolver is organized into two cooperating planes.

### 1. The Execution Plane — MetaAgent + Sub-Agents

The **MetaAgent** is the kernel-level orchestrator. Given a user task, it decomposes the goal, selects the right specialists, and coordinates them over an **Agent Bus**. The specialist sub-agents cover complementary capabilities:

- **Deep Researcher** — multi-step web research and evidence gathering
- **Deep Analyzer** — reasoning and analysis over collected material
- **Vibe Coding** — writing, running, and iterating on code in a sandboxed workspace
- **Tool Calling** — general tool use and environment interaction

Every run streams to a live **Trace UI**, so you can watch orchestration, tool calls, and reasoning unfold in real time — and afterwards inspect run state, workspace artifacts, and generated memory reports.

### 2. The Evolution Plane — Optimizer / Evaluator / Generator

This is what makes AgentEvolver an *evolving* OS. Three meta-agents run a closed improvement loop over the system's own ecosystem:

- **Evaluator** — measures outcomes across runs: which tools succeed, where sub-agents fail, which skills are missing.
- **Optimizer** — refines existing resources: rewriting prompts, tuning tool interfaces, and improving how sub-agents are composed.
- **Generator** — synthesizes *new* resources when the current ecosystem falls short: new tools, new reusable skills, and new specialist agents.

The three domains under evolution — **tools, skills, and agents** — form a compounding stack. Better tools raise skill quality; better skills raise agent competence; better agents expose the next gap for the generator to fill.

## Why an "Operating System"?

The OS framing is deliberate. AgentEvolver provides the same primitives a real OS does, but for agents:

- **Process orchestration** — the MetaAgent schedules and coordinates sub-agents like a kernel scheduling processes.
- **A managed resource layer** — tools, skills, and agents are first-class resources registered through 10+ component registries rather than hard-coded functions, so new components hot-plug in around an immutable core.
- **Centralized secret management** — API keys and credentials are handled through **Vault**, keeping secrets out of code and configuration.
- **Observability** — the Trace UI and run artifacts give a system-wide view of everything the agents do.

On top of these primitives sits the distinguishing feature: a **self-evolution loop** that continuously extends the OS's own capabilities.

## Running It

AgentEvolver runs on Python 3.12 with Vault for secrets. The entry point is `examples/run_meta_agent.py`, which supports a default task, an inline task via `--task`, or a task file from `examples/tasks/`. Model selection and other settings are overridable through `--cfg-options` (e.g. `model_name=openai/o3`), with defaults in `configs/meta_agent.py`. The framework ships with a suite of reasoning and agentic benchmarks out of the box — AIME, GPQA, GSM8K, HLE, LeetCode, and DeepWeb, among others.

## Connection to My Prior Work

AgentEvolver is the natural next step from [**Autogenesis**](https://arxiv.org/abs/2604.15034), which established that agents can safely rewrite their own prompts, tools, and memory at runtime through versioned resources, and from [**AgentOrchestra**](https://arxiv.org/abs/2506.12508), whose TEA protocol treats tools, environments, and agents as first-class resources. AgentEvolver unifies these threads into a single operating system: hierarchical orchestration *plus* a dedicated evolution plane that improves the whole ecosystem — tools, skills, and agents — continuously and autonomously.

It is one more step toward agents that genuinely improve through experience rather than through hand-written updates.

## Links

- **Project Page**: [dvampire.github.io/AgentEvolver](https://dvampire.github.io/AgentEvolver/)
- **GitHub**: [DVampire/AgentEvolver](https://github.com/DVampire/AgentEvolver)
