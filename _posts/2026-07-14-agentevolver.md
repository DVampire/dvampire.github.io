---
layout: post
title: "AgentEvolver: From Multi-Agent Execution to Trainable Trajectories"
date: 2026-07-14
description: AgentEvolver connects multi-agent task execution, evidence-driven capability evolution, and reward-annotated SFT/RL trajectories in one inspectable and reversible runtime.
tags: [LLM Agents, Self-Evolution, Multi-Agent Systems, SFT, Reinforcement Learning]
---

We introduce **AgentEvolver** ([project page](https://dvampire.github.io/AgentEvolver/) · [GitHub](https://github.com/DVampire/AgentEvolver)), a self-evolving multi-agent framework for complex engineering and research tasks.

Most multi-agent systems focus on a single question: *how can several agents collaborate on the task in front of them?* AgentEvolver asks a second question: *when that task exposes a real capability gap, how can the missing method become a reusable component for future tasks?*

The current release connects three layers that are often built separately:

1. **Task execution** — a MetaAgent plans, delegates, reviews, and coordinates specialist agents in one project.
2. **Capability evolution** — generators, evaluators, and optimizers create or improve versioned extensions when evidence shows that the existing system is insufficient.
3. **Training data collection** — each run can become a reward-annotated trajectory for SFT or reinforcement-learning pipelines.

> **Mental model:** AgentEvolver is a multi-agent task runtime, a versioned capability extension system, and an SFT/RL data flywheel.

## One System Loop

AgentEvolver organizes work as an explicit loop:

**Execute → Observe → Evaluate → Evolve → Collect**

- **Execute:** specialist agents work on the task in a shared session workspace.
- **Observe:** an append-only event log records meaningful actions, results, failures, resource use, and agent communication.
- **Evaluate:** tests, benchmarks, reviewers, and task-specific judges determine whether the output meets the required standard.
- **Evolve:** a verified, reusable capability gap can trigger the creation or refinement of an extension.
- **Collect:** the effective prompts, native tool calls, observations, token usage, and final reward are persisted as a trajectory.

The final step in the longer-term loop is **train and serve**: use the collected trajectories to train or fine-tune models, evaluate candidate checkpoints, and feed an approved model back into the runtime. AgentEvolver already implements trajectory capture, reward backfilling, persistence, and SFT/RL export. Integrated weight training, checkpoint management, and model feedback remain roadmap items rather than hidden features of the current release.

## Multi-Agent Execution

At runtime, the **MetaAgent** decomposes a goal, delegates work through the **Agent Bus**, reviews returned results, and can send weak work back for another pass. Specialist agents cover areas such as coding, browser interaction, general task execution, research, analysis, and review.

The underlying runtime treats a running agent as a mailbox with its own asynchronous loop. It supports direct requests, fire-and-forget messages, publish/subscribe communication, pausing, cancellation, and suspend/resume. A blocked sub-agent can escalate a question to its parent, park without consuming its step budget, and resume when guidance arrives instead of spinning or failing silently.

This separation between runtime and protocol matters: the runtime controls how messages move, while the protocol defines what those messages mean. New specialists can therefore be introduced without adding another special case to the core execution loop.

## Evidence Before Evolution

Self-evolution does **not** mean unrestricted self-modification. AgentEvolver deliberately makes “fix the task” the default response and reserves evolution for gaps supported by evidence.

An evolution round is appropriate when the system encounters one of three situations:

- **Missing capability:** the task requires an operation that no existing component can perform.
- **Recurring structural failure:** the same failure persists after explicit corrective guidance.
- **Measured quality ceiling:** evaluation shows a systematic limitation and identifies a reusable method that is missing.

A first-time bug, transient tool error, unused existing capability, or tight execution budget should not trigger evolution. In those cases, the system should retry, repair the output, wire in what already exists, or finish the user's task.

When evolution is justified, three roles form a controlled engineering cycle:

- A **generator** creates a new capability.
- An **optimizer** improves an existing evolvable capability.
- An **evaluator** compares the candidate against tests, benchmarks, replayed tasks, or a baseline.

Generated components live outside the hand-written core in an `extension/` tree. They are staged, versioned, evaluated, promoted, and—if they regress—rolled back or unloaded. This keeps the mutation surface explicit and preserves a clean boundary between trusted built-ins and evolved extensions.

The extension layer covers reusable **tools, skills, agents, connectors, environments, workflows, memory systems, and plugins**. Each component exposes a common schema through registry-driven managers, making capabilities discoverable and replaceable without coupling them to the runtime.

## Every Run Can Become Training Data

Capability evolution improves the runtime immediately; trajectory collection creates a path toward improving the model itself.

The `TrajectoryHook` records what actually happened during inference:

- the effective messages sent to the model after hooks and context compaction;
- model reasoning and native tool calls;
- observations, errors, and results returned by actions;
- token usage and cost when available;
- the task outcome and a reward that may arrive after evaluation.

Failures remain in the record. If a model fails twice and succeeds on the third attempt, the trajectory preserves all three attempts instead of presenting a fictional first-try success. Late evaluation rewards are backfilled into the steps that produced the outcome.

Finished runs can be exported as OpenAI-style chat records for SFT or through a pluggable RL format, including a text-level VERL episode representation. This makes the execution trace more than telemetry: it becomes a faithful training example with state, action, observation, and reward.

Exportability is not the same as readiness for training. Real trajectories may contain user text, file contents, tool arguments, external responses, and model reasoning, so production datasets still require consent and retention rules, redaction, deduplication, quality filtering, and train/evaluation leakage checks.

## Inspectable by Design

AgentEvolver makes the runtime understandable from both the browser and the filesystem.

Prompts, workflows, task documents, memory reports, and per-step snapshots are complete HTML documents. The same bytes used by the runtime can be opened, reviewed, diffed, and styled in a browser—there is no separate export representation that can drift from what the agent executed.

The Web workbench provides several views over the same project:

- **Overview** keeps the plan, runtime activity, capabilities, candidates, and files together.
- **Chat** submits tasks and renders the live event log.
- **Canvas** composes reusable visual workflows.
- **Code** opens a browser-based VS Code environment over the session workspace.
- **Science** provides a live Jupyter kernel over the same project files.

Because these surfaces share a project and backend, switching views does not create competing copies of state. A file written by an agent can be inspected in Code, analyzed in Science, and referenced from Chat in the same session.

## Safety and Operational Boundaries

An agent that can execute commands or propose new components needs enforcement mechanisms, not prompt-only advice. AgentEvolver separates several controls:

- **Permission modes** determine whether a capability is allowed to perform a mutating operation.
- **Plan mode** permits reading and reasoning while refusing mutation until a person approves the plan.
- **Sandboxes** constrain where commands run, which paths are mounted, and which network destinations are reachable.
- **Budgets** enforce step, token, and wall-time ceilings while exposing the remaining budget to the model.
- **Versioning and rollback** limit the impact of a bad extension, although reversibility is not proof that a component is safe or correct.

These boundaries make AgentEvolver a better fit for long-running engineering, data, and scientific workflows—where reusable methods, coordination, and auditability justify the additional machinery—than for simple Q&A or latency-sensitive one-step automation.

## Getting Started

AgentEvolver supports Python 3.11 or newer. The shortest local path is:

```bash
git clone https://github.com/DVampire/AgentEvolver.git
cd AgentEvolver
bash scripts/install.sh
conda activate agentos
```

If Conda is unavailable, the installer also supports `bash scripts/install.sh --uv`. After configuring a model provider in `.env`, run a small task first:

```bash
python examples/run_meta_agent.py \
  --task "Reverse a string and add unit tests"
```

Task documents can also be loaded from HTML files:

```bash
python examples/run_meta_agent.py \
  --task-file examples/tasks/qsar_egfr_experiment.html
```

For an interactive terminal use `agentevolver tui --config configs/meta_agent.py`; for the full workbench use `bash scripts/serve-ui.sh`. Optional browser, sandbox, desktop, and remote-machine capabilities can be added when the task requires them.

## Connection to My Prior Work

AgentEvolver brings together ideas from [**AgentOrchestra**](https://arxiv.org/abs/2506.12508) and [**Autogenesis**](https://arxiv.org/abs/2604.15034). AgentOrchestra explored hierarchical orchestration and first-class agent resources; Autogenesis studied controlled self-evolution through versioned resources. AgentEvolver turns those ideas into a working runtime where execution, evaluation, reversible component evolution, and training-data collection share one system boundary.

The immediate goal is practical: finish today's task and preserve the reusable improvement. The longer-term goal is a closed loop in which successful behavior becomes training data, approved model updates return to serving, and the next generation of tasks produces better experience again.

## Links

- **Project overview:** [dvampire.github.io/AgentEvolver](https://dvampire.github.io/AgentEvolver/)
- **Tutorial:** [From nothing to a trajectory](https://dvampire.github.io/AgentEvolver/tutorial.html)
- **Architecture:** [One log, two readings](https://dvampire.github.io/AgentEvolver/architecture.html)
- **Web workbench:** [Feature tour](https://dvampire.github.io/AgentEvolver/ui.html)
- **Source code:** [DVampire/AgentEvolver](https://github.com/DVampire/AgentEvolver)
