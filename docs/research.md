---
layout: default
title: Research
permalink: /research/
description: Wentao Zhang's research on LLM Agents, Self-Evolving Agents, and Financial AI.
---

# Research

<div class="reveal reveal-delay-1">
My research sits at the intersection of <strong>LLM-powered autonomous agents</strong> and <strong>Financial AI (AI4Finance)</strong>. A central theme is <strong>agent self-evolution</strong> — building systems that continuously improve themselves through closed-loop experience, resource versioning, and protocol-level self-modification.
</div>

---

## Research Themes

<div class="reveal reveal-delay-2">
<ul>
  <li><strong>Self-Evolving Agents</strong> — Protocols and architectures enabling agents to evolve their own prompts, tools, memory, and sub-agents autonomously</li>
  <li><strong>LLM Agents &amp; Multi-Agent Orchestration</strong> — Hierarchical frameworks, tool use, long-horizon planning, and standardized agent communication protocols</li>
  <li><strong>General Computer Control</strong> — Foundation agents that operate arbitrary software using only pixels and natural language</li>
  <li><strong>AI4Finance</strong> — End-to-end financial platforms, algorithmic trading, portfolio management, and HFT via RL and LLMs</li>
  <li><strong>Reinforcement Learning</strong> — Deep RL for sequential decision-making in complex, partially observable environments</li>
</ul>
</div>

---

## Featured Projects

<div class="project-card featured reveal reveal-delay-3">
  <span class="feature-badge badge-red">Featured · Self-Evolution</span>
  <h3>Autogenesis: A Self-Evolving Agent Protocol</h3>
  <p>Autogenesis addresses a fundamental limitation of current LLM agent systems: they are static — prompts, tools, and behaviors fixed at design time cannot improve from experience.</p>
  <p>Two tightly coupled layers power the system:</p>
  <ul>
    <li><strong>Resource Substrate Protocol Layer</strong> — models prompts, agents, tools, and memory as <em>versioned resources</em> with explicit lifecycles, enabling safe mutation and rollback</li>
    <li><strong>Self-Evolution Protocol Layer</strong> — a closed-loop system where the agent monitors its own performance, identifies failure modes, and autonomously rewrites its own resources to improve</li>
  </ul>
  <p>The result is an agent that gets measurably better at complex planning and tool-use tasks through runtime self-modification — without human intervention.</p>
  <div class="project-links">
    <a href="https://arxiv.org/abs/2604.15034" target="_blank">Paper</a>
    <a href="https://github.com/DVampire/Autogenesis" target="_blank">GitHub</a>
  </div>
</div>

<div class="project-card featured reveal reveal-delay-3">
  <span class="feature-badge badge-blue">Featured · ICML 2025</span>
  <h3>Cradle: Empowering Foundation Agents towards General Computer Control</h3>
  <p>How do you build an agent that can use <em>any</em> computer software — without task-specific APIs or hand-coded integrations?</p>
  <p>Cradle's answer: treat the screen as the universal interface. Agents receive screenshots as input and produce keyboard and mouse actions as output — exactly how humans interact with computers. This unlocks operation across arbitrary software: games (Red Dead Redemption 2, Stardew Valley, Cities: Skylines), browsers, email clients, and creative tools — all with the same agent.</p>
  <p>Cradle also incorporates <strong>self-improvement</strong>: agents curate and refine a skill library from past experience, enabling progressive capability growth on new tasks.</p>
  <p>⭐ 2.5k GitHub stars</p>
  <div class="project-links">
    <a href="https://arxiv.org/abs/2403.03186" target="_blank">Paper</a>
    <a href="https://github.com/BAAI-Agents/Cradle" target="_blank">GitHub</a>
    <a href="https://baai-agents.github.io/Cradle/" target="_blank">Project Page</a>
  </div>
</div>

<div class="project-card reveal reveal-delay-4">
  <span class="feature-badge badge-teal">Multi-Agent · GAIA SOTA</span>
  <h3>AgentOrchestra: Hierarchical Multi-Agent Orchestration with the TEA Protocol</h3>
  <p>The Tool-Environment-Agent (TEA) protocol treats environments, agents, and tools as <strong>first-class resources</strong> with explicit lifecycles and versioned interfaces — solving the fragile, ad-hoc wiring that plagues most multi-agent systems.</p>
  <p>AgentOrchestra builds on TEA with a central planner that dynamically spawns and coordinates specialist sub-agents (web navigation, data analysis, file operations). It achieves <strong>89.04% on GAIA</strong>, establishing state-of-the-art performance on general-purpose agent benchmarks.</p>
  <div class="project-links">
    <a href="https://arxiv.org/abs/2506.12508" target="_blank">Paper</a>
  </div>
</div>

<div class="project-card reveal reveal-delay-4">
  <span class="feature-badge badge-teal">KDD 2024</span>
  <h3>FinAgent: A Multimodal Foundation Agent for Financial Trading: Tool-Augmented, Diversified, and Generalist</h3>
  <p>A <strong>tool-augmented, diversified, and generalist</strong> multimodal agent for financial trading that integrates heterogeneous data sources (price, news, filings) and diverse trading tools, achieving state-of-the-art results across multiple financial benchmarks.</p>
  <div class="project-links">
    <a href="https://arxiv.org/abs/2402.18485" target="_blank">Paper</a>
    <a href="https://github.com/DVampire/FinAgent" target="_blank">GitHub</a>
  </div>
</div>

<div class="project-card reveal reveal-delay-4">
  <span class="feature-badge badge-teal">KDD 2026</span>
  <h3>AlphaForgeBench: Benchmarking LLMs as Quantitative Researchers</h3>
  <p>Rather than asking LLMs to emit trading actions directly — which suffers from extreme run-to-run variance and irrational reversals — AlphaForgeBench repositions LLMs as <strong>quantitative researchers</strong> that generate executable alpha factors and strategy code, evaluated via standardized backtesting across 7 assets and 6 frontier models.</p>
  <p>A 3×3 level-grade taxonomy of 903 queries (633 real-world + 270 augmented) reveals three persistent model archetypes and systematic difficulty scaling — providing a stable, reproducible foundation for LLM financial capability evaluation.</p>
  <div class="project-links">
    <a href="https://arxiv.org/abs/2602.18481" target="_blank">Paper</a>
    <a href="https://github.com/finbrain-lab-hkustgz/AlphaForgeBench" target="_blank">GitHub</a>
    <a href="https://finbrain-lab-hkustgz.github.io/AlphaForgeBench/" target="_blank">Project Page</a>
  </div>
</div>

<div class="project-card reveal reveal-delay-4">
  <span class="feature-badge badge-teal">AI4Finance · Prediction Markets</span>
  <h3>PolyMonitor: Prediction Market Intelligence Workspace</h3>
  <p>An open-source live intelligence workspace for Polymarket — consolidating market prices, on-chain flow, oracle activity, order-book depth, and macro context into a unified dashboard. Paired with the <strong>Polymarket Agent</strong>, a 10-node multi-agent forecasting pipeline combining deterministic evidence construction, LLM specialist agents, adversarial critique, and calibration.</p>
  <p>The platform serves as the operational infrastructure for our <em>Unlocking the Forecasting Economy</em> dataset suite, covering the full prediction market lifecycle from listing through oracle resolution and settlement.</p>
  <div class="project-links">
    <a href="https://arxiv.org/abs/2604.20421" target="_blank">Paper</a>
    <a href="https://github.com/virusLuke3/polymonitor" target="_blank">GitHub</a>
    <a href="https://www.polymonitor.club/" target="_blank">Project Page</a>
  </div>
</div>

<div class="project-card reveal reveal-delay-5">
  <span class="feature-badge badge-teal">KDD 2026</span>
  <h3>FinWorld: End-to-End Financial AI Platform</h3>
  <p>An <strong>all-in-one open-source platform</strong> for financial AI research and deployment, integrating data pipelines, model training, backtesting, and live deployment over 800M+ multimodal data samples from 1995–2025. Lowers the barrier for rigorous, reproducible AI4Finance research.</p>
  <div class="project-links">
    <a href="https://arxiv.org/abs/2508.02292" target="_blank">Paper</a>
    <a href="https://github.com/DVampire/FinWorld" target="_blank">GitHub</a>
    <a href="https://dvampire.github.io/FinWorld/" target="_blank">Project Page</a>
  </div>
</div>

<div class="project-card reveal reveal-delay-5">
  <span class="feature-badge badge-teal">NeurIPS 2023</span>
  <h3>TradeMaster: A Holistic Quantitative Trading Platform Empowered by Reinforcement Learning</h3>
  <p>A holistic platform covering data processing, environment simulation, RL agent training, and performance evaluation across multiple financial markets and trading tasks.</p>
  <p>⭐ 2.7k GitHub stars</p>
  <div class="project-links">
    <a href="https://personal.ntu.edu.sg/boan/papers/NeurIPS_23_TradeMaster.pdf" target="_blank">Paper</a>
    <a href="https://github.com/TradeMaster-NTU/TradeMaster" target="_blank">GitHub</a>
  </div>
</div>

<div class="project-card reveal reveal-delay-5">
  <span class="feature-badge badge-teal">AAAI 2024</span>
  <h3>EarnHFT: Efficient Hierarchical Reinforcement Learning for High-Frequency Trading</h3>
  <p>Decomposes the HFT problem into macro-level strategy selection and micro-level order execution. The hierarchical structure yields significantly improved sample efficiency and live-trading profitability.</p>
  <div class="project-links">
    <a href="https://arxiv.org/abs/2309.12891" target="_blank">Paper</a>
  </div>
</div>

<div class="project-card reveal reveal-delay-5">
  <span class="feature-badge badge-teal">WWW 2024</span>
  <h3>EarnMore: Portfolio Management in Customizable Stock Pools</h3>
  <p>A maskable stock representation framework that enables RL agents to handle arbitrary stock universes with a single trained model — eliminating the need to retrain per pool.</p>
  <div class="project-links">
    <a href="https://arxiv.org/abs/2311.10801" target="_blank">Paper</a>
    <a href="https://github.com/DVampire/EarnMore" target="_blank">GitHub</a>
  </div>
</div>

<div class="project-card reveal reveal-delay-5">
  <h3>TWOSOME: True Knowledge Comes from Practice: Aligning LLMs with Embodied Environments via Reinforcement Learning</h3>
  <p>Aligns LLMs with interactive environments through reinforcement learning, enabling agents to acquire genuine knowledge through embodied practice rather than passive pretraining.</p>
  <div class="project-links">
    <a href="https://arxiv.org/abs/2401.14151" target="_blank">Paper</a>
  </div>
</div>
