---
layout: post
title: "Autogenesis: A Self-Evolving Agent Protocol"
date: 2026-04-16
description: We introduce Autogenesis, a protocol enabling LLM agents to autonomously rewrite their own prompts, tools, and memory at runtime — getting measurably better at complex tasks without human intervention.
tags: [LLM Agents, Self-Evolution, Agent Protocol]
---

We introduce **Autogenesis**, a protocol that enables LLM-based agents to **autonomously evolve themselves** — rewriting their own prompts, tools, and memory at runtime without human intervention.

## Why Agent Self-Evolution?

Current LLM agent systems are fundamentally static. Their prompts are written once by engineers. Their tools are fixed at deployment. Their behaviors do not improve from experience. This is a severe limitation: real-world tasks are diverse and unpredictable, and static agents plateau quickly as task complexity grows.

**Autogenesis** asks: can an agent monitor its own failures, diagnose what went wrong, and rewrite itself to do better — autonomously?

## Architecture

Autogenesis is built around two tightly coupled layers:

### 1. Resource Substrate Protocol Layer

Everything in an Autogenesis agent — prompts, tools, memory, even sub-agents — is modeled as a **versioned resource** with an explicit lifecycle:

- **Create** → **Activate** → **Suspend** → **Terminate**
- Every mutation produces a new version; prior versions are retained for rollback
- Resources expose typed interfaces, enabling safe composition and substitution

This versioning foundation is what makes self-modification *safe*: the agent can experiment with changes and revert if performance degrades.

### 2. Self-Evolution Protocol Layer

The evolution layer operates as a closed feedback loop:

1. **Monitor** — tracks task outcomes, tool call success rates, and reasoning quality
2. **Diagnose** — identifies failure patterns and root causes across recent episodes
3. **Propose** — generates candidate resource mutations (prompt rewrites, new tools, memory restructuring)
4. **Evaluate** — tests candidates against a held-out task distribution
5. **Commit** — promotes successful mutations; discards or rolls back failures

This loop runs continuously during deployment, not just at training time.

## Results

Autogenesis demonstrates consistent improvement on benchmarks involving complex planning and multi-step tool use. Key findings:

- Agents improve measurably across repeated task episodes without any human-written updates
- The versioned resource model prevents catastrophic self-modification — rollback is triggered automatically when performance regresses
- Self-evolved prompts outperform hand-crafted prompts on out-of-distribution tasks

## Connection to Cradle

Autogenesis shares a philosophical foundation with [Cradle](https://baai-agents.github.io/Cradle/): both systems treat **self-improvement as a first-class capability**, not an afterthought. Where Cradle builds a skill library through interaction, Autogenesis goes further — evolving the agent's core resources at the protocol level.

Together, they represent a research direction toward agents that genuinely improve through experience.

## Links

- **Paper**: [arXiv:2604.15034](https://arxiv.org/abs/2604.15034)
- **GitHub**: [DVampire/Autogenesis](https://github.com/DVampire/Autogenesis)
