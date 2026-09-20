---
layout: post
title: "AgentEvolver: Global Evolution for Complex Tasks"
date: 2026-07-14
description: AgentEvolver is an open agent platform for planning, executing, and inspecting complex work while evolving eight kinds of capability through evidence-backed development.
tags: [LLM Agents, Self-Evolution, Multi-Agent Systems, Agent Runtime, Reinforcement Learning]
---

We introduce **AgentEvolver** ([project page](https://dvampire.github.io/AgentEvolver/index.html) · [GitHub](https://github.com/DVampire/AgentEvolver)), an open platform for building with agents and evolving the whole capability system around them.

Many agent frameworks optimize a single prompt, tool, or workflow. Real tasks expose a broader problem: sometimes the missing piece is an action; sometimes it is a method, a specialist, a workflow, a memory strategy, or a connection to an external system. AgentEvolver treats all of these as evolvable parts of one platform.

> **Build with agents. Evolve the whole system.**

The core loop is simple:

**Plan → Execute → Inspect → Evolve → Evaluate → Use again**

A task enters through a **Living Plan**, runs through a controllable **Runtime**, and carries the right information through **Context & Memory**. When execution reveals a reusable capability gap, AgentEvolver can develop a versioned candidate, evaluate it against real calls, keep or roll it back, and record what happens when it is used again.

<figure>
  <a href="https://dvampire.github.io/AgentEvolver/ui.html">
    <img src="https://dvampire.github.io/AgentEvolver/assets/ui/workbench-overview.png" alt="AgentEvolver project workbench showing the living plan, runtime, workspace, and evolvable capabilities" loading="lazy">
  </a>
  <figcaption>One shared project: inspect the plan, runtime, files, capabilities, and evolution candidates from the AgentEvolver workbench.</figcaption>
</figure>

## Global Evolution Across Eight Entity Types

AgentEvolver does not reduce self-evolution to tool generation. It exposes one development lifecycle across eight kinds of capability:

| Entity | What can evolve |
| --- | --- |
| **Tool** | A callable action with a clear input and output |
| **Skill** | A reusable method, procedure, or set of instructions |
| **Agent** | A specialist's role, behavior, and available capabilities |
| **Workflow** | The order, branching, parallelism, and verification of work |
| **Memory** | How experience is recorded, retrieved, and reused |
| **Environment** | The execution setting and resources available to agents |
| **Connector** | Access to an external API, service, or data source |
| **Plugin** | A packaged combination of capabilities and integration logic |

These entities share a common lifecycle: identify a need, develop a candidate, evaluate it, decide whether to keep it, and observe later use. This gives the system room to change the *right layer* instead of forcing every problem into a new prompt or tool.

## A Foundation for Complex Work

Global evolution only helps if the underlying work can run reliably. AgentEvolver therefore builds on three foundations.

### Runtime

The Runtime coordinates focused workers, resident services, and event subscribers. Agents can exchange messages, share resources, and pause or resume at defined execution boundaries. Budgets, permissions, and cleanup remain visible to the coordinator instead of being hidden inside a monolithic agent loop.

### Living Plan

The plan is active state, not a static checklist produced at the beginning. It preserves the goal, current progress, blockers, evidence, and next decisions while work is underway. After context compaction, the latest plan summary returns to the active context so the agent can continue without losing direction. An approval gate can also separate planning from mutation when human review is required.

### Context & Memory

Long-running tasks need selective continuity rather than an endlessly growing transcript. AgentEvolver separates fixed task instructions, compacted history, recent interactions, the live plan, observations, and remaining budget. This keeps the next decision grounded while controlling context growth.

Together, these layers let both single-agent and multi-agent work continue across failures, handoffs, and long execution horizons.

## Evidence-Backed Evolution

Self-evolution should not mean accepting every generated component. AgentEvolver makes improvement inspectable through five stages:

1. **Observe** — identify a need and record a baseline.
2. **Develop** — create or refine a versioned component.
3. **Evaluate** — compare outcomes using executed calls and task evidence.
4. **Decide** — keep, roll back, or unload the candidate.
5. **Use again** — verify the component in subsequent work.

Evaluation records link a judgment to a specific version and the calls that produced the result. This distinction is important: registering a candidate proves only that it exists, not that it improves the system. Tasks that require verified improvement must also show that the accepted component was actually used and helped later execution.

## Work Alongside the Agents

The Web Workbench provides multiple views over the same project and backend:

- **Overview** brings the Living Plan, runtime activity, workspace, capabilities, and candidates together.
- **Chat** submits tasks and follows live execution events.
- **Canvas** composes visual workflows.
- **Code** opens the project in a browser-based development environment.
- **Science** connects the same files to a live Jupyter kernel.

Because the views share project state, an artifact produced by an agent can be opened in Code, analyzed in Science, and discussed in Chat without copying it between isolated interfaces. The user can inspect the work and take the next step at any point.

## From Websites to Scientific Work

The platform is designed around complete tasks rather than isolated model calls:

- **Website development:** build the site, browse the rendered result, and refine it from visual evidence.
- **Game development:** build in Godot, inspect rendered scenes, and test the experience through engine controls.
- **Research:** investigate sources, run computations, and verify conclusions against evidence.

These examples require different tools and environments, but they use the same planning, runtime, context, evidence, and evolution model.

## System Architecture

<figure>
  <a href="https://dvampire.github.io/AgentEvolver/assets/arch.svg">
    <img src="https://dvampire.github.io/AgentEvolver/assets/arch.svg" alt="AgentEvolver system architecture covering interfaces, orchestration, execution, infrastructure, capabilities, evolution, and training data" loading="lazy">
  </a>
  <figcaption>AgentEvolver connects user interfaces, orchestration, execution infrastructure, evolvable capabilities, and evidence-backed development in one architecture. Open the image for the full-resolution diagram.</figcaption>
</figure>

Several engineering details support the complete loop:

- **Programmatic tool use** expresses batches, loops, and branches in code while returning only selected results.
- **Dynamic workflows** compose parallel work, checkpoints, verification, and recovery paths.
- **Shared budgets and permissions** apply across parent and child agents with inherited ceilings.
- **Trace and recovery** preserve request and action evidence and reconcile uncertain effects before continuing.
- **Capabilities on demand** search the mounted catalog and expose relevant components for the next step.
- **Data for SFT/RL** exports execution records with provenance and reward labels for downstream training.

Training data is therefore one output of the platform rather than its organizing principle. The more immediate objective is to finish the current task, make the result inspectable, and preserve any demonstrated improvement for the next one.

## Getting Started

Clone the repository and run the installer:

```bash
git clone https://github.com/DVampire/AgentEvolver.git
cd AgentEvolver
bash scripts/install.sh
conda activate agentos
```

Set `LLM_HUB_API_BASE` and `LLM_HUB_API_KEY` in a local `.env` file for the provided examples. Other model providers can be selected through configuration. Then start with a small, verifiable task:

```bash
python examples/run_meta_agent.py \
  --task "Build a useful tool and verify it."
```

The same platform can then mount browser, code, scientific-computing, sandbox, or game-development environments as the task demands.

## Why AgentEvolver

AgentEvolver brings together ideas from [**AgentOrchestra**](https://arxiv.org/abs/2506.12508) and [**Autogenesis**](https://arxiv.org/abs/2604.15034), then extends them into a shared platform for execution and capability development.

The long-term goal is not an agent that rewrites itself without constraint. It is a system that can locate the right capability boundary, propose a versioned improvement, test it against real work, preserve the evidence, and safely reuse what proved useful.

## Explore

- **Project overview:** [Global evolution for complex tasks](https://dvampire.github.io/AgentEvolver/index.html)
- **Architecture:** [System architecture guide](https://dvampire.github.io/AgentEvolver/architecture.html)
- **Web Workbench:** [Interactive feature tour](https://dvampire.github.io/AgentEvolver/ui.html)
- **Evolution demos:** [Watch complete evolution workflows](https://dvampire.github.io/AgentEvolver/demos.html)
- **Source code:** [DVampire/AgentEvolver](https://github.com/DVampire/AgentEvolver)
