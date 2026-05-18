---
layout: default
title: Research
permalink: /research/
description: Wentao Zhang's research on LLM Agents, Self-Evolving Agents, and Financial AI.
---

# Research

My research sits at the intersection of **LLM-powered autonomous agents** and **Financial AI (AI4Finance)**. A central theme of my recent work is **agent self-evolution** — building systems that continuously improve themselves through closed-loop experience, resource versioning, and protocol-level self-modification.

---

## Research Themes

- **Self-Evolving Agents** — Designing protocols and architectures that allow agents to evolve their own prompts, tools, memory, and sub-agent configurations autonomously, without human intervention
- **LLM Agents & Multi-Agent Orchestration** — Hierarchical frameworks, tool use, long-horizon planning, and standardized agent communication protocols
- **General Computer Control** — Foundation agents that operate arbitrary software using only pixels and natural language, with no task-specific APIs
- **AI4Finance** — End-to-end financial platforms, algorithmic trading, portfolio management, and high-frequency trading via RL and LLMs
- **Reinforcement Learning** — Deep RL for sequential decision-making in complex, partially observable environments

---

## Featured Projects

### Autogenesis: A Self-Evolving Agent Protocol
<span style="background:#e74c3c; color:white; padding:2px 8px; border-radius:4px; font-size:0.85em;">Featured · Self-Evolution</span>

Autogenesis addresses a fundamental limitation of current LLM agent systems: they are static — their prompts, tools, and behaviors are fixed at design time and cannot improve from experience.

Autogenesis introduces two tightly coupled layers:
- **Resource Substrate Protocol Layer** — models prompts, agents, tools, and memory as *versioned resources* with explicit lifecycles, enabling safe mutation and rollback
- **Self-Evolution Protocol Layer** — a closed-loop system where the agent monitors its own performance, identifies failure modes, and autonomously rewrites its own resources to improve

The result is an agent that gets measurably better at complex planning and tool-use tasks through runtime self-modification — without human intervention.

[[Paper]](https://arxiv.org/abs/2604.15034) &nbsp;|&nbsp; [[GitHub]](https://github.com/DVampire/Autogenesis)

---

### Cradle: Empowering Foundation Agents towards General Computer Control
<span style="background:#2980b9; color:white; padding:2px 8px; border-radius:4px; font-size:0.85em;">Featured · Computer Control</span>

How do you build an agent that can use *any* computer software — without task-specific APIs or hand-coded integrations?

Cradle's answer: treat the screen as the universal interface. Agents receive screenshots as input and produce keyboard and mouse actions as output — exactly how humans interact with computers. This minimal assumption unlocks operation across arbitrary software: games (Red Dead Redemption 2, Stardew Valley, Cities: Skylines), browsers, email clients, and creative tools — all with the same agent, zero per-app engineering.

Cradle also incorporates **self-improvement**: agents curate and refine a skill library from past experience, enabling progressive capability growth on new tasks.

> ⭐ 2.5k GitHub stars

[[Paper]](https://arxiv.org/abs/2403.03186) &nbsp;|&nbsp; [[GitHub]](https://github.com/BAAI-Agents/Cradle) &nbsp;|&nbsp; [[Project Page]](https://baai-agents.github.io/Cradle/)

---

### AgentOrchestra: Hierarchical Multi-Agent Orchestration with the TEA Protocol

The Tool-Environment-Agent (TEA) protocol treats environments, agents, and tools as **first-class resources** with explicit lifecycles and versioned interfaces — solving the fragile, ad-hoc wiring that plagues most multi-agent systems.

AgentOrchestra builds on TEA with a central planner that dynamically spawns and coordinates specialist sub-agents (web navigation, data analysis, file operations). It achieves **89.04% on GAIA**, establishing state-of-the-art performance on general-purpose agent benchmarks.

[[Paper]](https://arxiv.org/abs/2506.12508)

---

### FinAgent: A Multimodal Foundation Agent for Financial Trading: Tool-Augmented, Diversified, and Generalist

A **tool-augmented, diversified, and generalist** multimodal agent for financial trading that integrates heterogeneous data sources (price, news, filings) and diverse trading tools, achieving state-of-the-art results across multiple financial benchmarks.

*KDD 2024*
[[Paper]](https://arxiv.org/abs/2402.18485) &nbsp;|&nbsp; [[GitHub]](https://github.com/DVampire/FinAgent)

---

### FinWorld: End-to-End Financial AI Platform

An **all-in-one open-source platform** for financial AI research and deployment, integrating data pipelines, model training, backtesting, and live deployment. Lowers the barrier for rigorous, reproducible AI4Finance research.

*KDD 2026*
[[Paper]](https://arxiv.org/abs/2508.02292) &nbsp;|&nbsp; [[GitHub]](https://github.com/DVampire/FinWorld) &nbsp;|&nbsp; [[Project Page]](https://dvampire.github.io/FinWorld/)

---

### TradeMaster: Quantitative Trading Platform via RL

A holistic platform covering data processing, environment simulation, RL agent training, and performance evaluation across multiple financial markets and trading tasks.

*NeurIPS 2023*

> ⭐ 2.7k GitHub stars

[[Paper]](https://personal.ntu.edu.sg/boan/papers/NeurIPS_23_TradeMaster.pdf) &nbsp;|&nbsp; [[GitHub]](https://github.com/TradeMaster-NTU/TradeMaster)

---

### True Knowledge Comes from Practice: Aligning LLMs with Embodied Environments via Reinforcement Learning

Aligns LLMs with interactive environments through reinforcement learning, enabling agents to acquire genuine knowledge through embodied practice rather than passive pretraining.

[[Paper]](https://arxiv.org/abs/2401.14151)

---

### EarnHFT: Hierarchical RL for High-Frequency Trading

Decomposes the HFT problem into macro-level strategy selection and micro-level order execution. The hierarchical structure yields significantly improved sample efficiency and live-trading profitability.

*AAAI 2024*
[[Paper]](https://arxiv.org/abs/2309.12891)

---

### EarnMore: Portfolio Management in Customizable Stock Pools

A maskable stock representation framework that enables RL agents to handle arbitrary stock universes with a single trained model — eliminating the need to retrain per pool.

*WWW 2024*
[[Paper]](https://arxiv.org/abs/2311.10801) &nbsp;|&nbsp; [[GitHub]](https://github.com/DVampire/EarnMore)
