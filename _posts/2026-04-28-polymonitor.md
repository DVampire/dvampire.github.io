---
layout: post
title: "PolyMonitor: Open-Source Intelligence Infrastructure for Prediction Markets"
date: 2026-04-28
description: We introduce PolyMonitor, an open-source live intelligence workspace for Polymarket — aggregating market data, on-chain flow, oracle activity, and AI-generated forecasts into a unified dashboard, paired with a 10-node multi-agent forecasting pipeline.
tags: [AI4Finance, LLM Agents, Prediction Markets, Multi-Agent]
---

We introduce **PolyMonitor** ([polymonitor.club](https://www.polymonitor.club/)), an open-source intelligence workspace for Polymarket participants — the companion platform to our paper [*Unlocking the Forecasting Economy: A Suite of Datasets for the Full Lifecycle of Prediction Market*](https://arxiv.org/abs/2604.20421).

## What PolyMonitor Does

Prediction market research today is fragmented: prices, on-chain trade flow, oracle activity, order-book depth, and macro context live in separate tools. PolyMonitor unifies them into a single live workspace, covering the full lifecycle of a prediction market from listing through settlement and archive.

The platform is organized around five core modules:

| Module | What it tracks |
|--------|---------------|
| **Market & Lifecycle** | Active markets, outcome probabilities, price movement, trade history |
| **Flow & Liquidity** | OrderFilled tape, whale tracking, order-book depth, bid/ask snapshots |
| **Oracle Watch** | UMA oracle events, resolution timelines, settlement risk signals |
| **Intelligence & News** | AI-generated market briefs, macro panels (CPI, Fed), sports odds, weather markets |
| **Distribution** | Telegram publishing layer for topic-based channel updates |

Unlike wrappers around public Polymarket APIs, PolyMonitor maintains independent infrastructure — a custom market catalog, token catalog, chain indexing system, runtime snapshots, and panel registry — enabling comprehensive inspection across the full market lifecycle.

## Polymarket Agent

The intelligence layer is powered by the **Polymarket Agent**, a structured multi-agent forecasting pipeline built on the *Forecast Intelligence Graph*. Rather than free-form conversation, the agent produces auditable, market-level claims grounded in prices, fills, related markets, oracle state, and external catalysts.

The pipeline executes as a directed state machine with 10 sequential nodes:

![Polymarket Agent Architecture](https://www.polymonitor.club/docs-assets/images/polymarket-agent-architecture.png)

The nodes divide into deterministic stages and LLM specialist stages:

**Deterministic stages** (rule-based, fast):
1. **Evidence Builder** — constructs structured evidence from market prices, fills, and external context
2. **Related Markets** — links sibling markets and cross-market correlations
3. **Quant Forecaster** — computes price drift and microstructure indicators
4. **Reflexion Memory** — loads prior forecast episodes to detect drift and anchoring

**LLM specialist stages** (model-backed):
5. **Microstructure Agent** — analyzes trading mechanics, liquidity depth, and order flow patterns
6. **Catalyst Agent** — identifies external event triggers and timing signals
7. **Resolution Agent** — examines settlement criteria and oracle signals

**Synthesis stages**:
8. **Calibration Agent** — aggregates confidence scores across all data sources
9. **Skeptic Agent** — adversarially critiques weak evidence and overconfidence
10. **Panel Writer** — generates the final dashboard output

Each run returns a dashboard payload, a quant snapshot, and a replayable event trace with per-node outputs, latency metrics, and token usage — making every forecast fully auditable.

## Connection to the Forecasting Economy Dataset

PolyMonitor is the operational platform behind our *Unlocking the Forecasting Economy* dataset suite, which provides structured data covering every stage of the prediction market lifecycle: market creation, trading dynamics, oracle resolution, and settlement. The dataset spans thousands of Polymarket markets with linked on-chain and off-chain signals, enabling end-to-end forecasting research across the full arc from listing to close.

## Links

- **Website**: [polymonitor.club](https://www.polymonitor.club/)
- **Agent Docs**: [polymonitor.club/docs/polymarket-agent](https://www.polymonitor.club/docs/polymarket-agent/)
- **GitHub**: [virusLuke3/polymonitor](https://github.com/virusLuke3/polymonitor)
- **Paper**: [arXiv:2604.20421](https://arxiv.org/abs/2604.20421)
