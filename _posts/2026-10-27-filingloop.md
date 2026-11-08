---
layout: post
title: "FilingLoop: Evaluating and Evolving LLM Agents for Corporate Disclosure Review and Revision"
date: 2026-10-27
permalink: /blog/filingloop/
description: An interactive benchmark and self-evolving agent framework for corporate disclosure review and revision, grounded in 380 historical SEC review tasks from 96 companies.
tags: [LLM Agents, Self-Evolution, AI4Finance, Benchmark]
---

We introduce **FilingLoop**, an interactive benchmark and self-evolving agent framework for corporate disclosure review and revision. The work brings together two themes in my research: financial AI and agents that improve their procedures through experience.

**Authors:** Wentao Zhang, Yilei Zhao, Guangyan Gan, Shuo Sun, and Lin William Cong.

[Read the paper](https://arxiv.org/abs/2610.37905) · [Download the PDF](https://arxiv.org/pdf/2610.37905)

## From Answering Questions to Revising Disclosures

Reviewing a corporate filing requires an agent to identify what is missing, find the evidence needed to address it, and verify the resulting document changes. A reviewer might challenge an explanation of revenue growth; company counsel must obtain the underlying facts, revise the filing, and respond to the concern.

FilingLoop reconstructs this interaction from historical U.S. Securities and Exchange Commission (SEC) correspondence. It evaluates the entire path from discovering an unstated deficiency to committing an evidence-backed revision.

## A Benchmark Grounded in Historical Reviews

Each task reconstructs one historical review round. Agents receive the filing and permitted earlier records. The current historical comments, replies, and subsequent amendments remain hidden, giving the evaluator a reference against which to assess the agents' work.

| Benchmark component | Coverage |
| --- | --- |
| Companies | 96 |
| Review tasks | 380 |
| Scorable comments | 3,012 |
| Eligible requirement occurrences | 6,099 |
| Registration review tasks | 378 |
| Annual-report review tasks | 2 |

A single comment can request several actions, such as adding a disclosure and explaining an accounting decision. FilingLoop decomposes these requests into individual requirements and checks each in its intended deliverable. **Promising a revision in a response earns no credit for an unchanged filing.**

Company information also has an explicit boundary: the Filer can request facts supported by the historical evidence, while the Reviewer sees those facts only when they appear in formal responses or disclosures.

## Two Roles, One Persistent Filing

<figure>
  <a href="{{ '/assets/img/filingloop-framework.png' | relative_url }}">
    <img src="{{ '/assets/img/filingloop-framework.png' | relative_url }}" alt="FilingLoop framework: historical SEC exchanges become evidence-linked tasks; Reviewer and Filer agents iteratively revise a shared filing; independent grading updates role skills for future batches only." width="1920" height="1090" loading="lazy">
  </a>
  <figcaption>Benchmark construction, review and revision, and online skill evolution. Figure 3 from <a href="https://arxiv.org/abs/2610.37905">FilingLoop</a>, Zhang et al. (2026), <a href="https://creativecommons.org/licenses/by/4.0/">CC BY 4.0</a>. Open the image to inspect the full diagram.</figcaption>
</figure>

The workflow connects three responsibilities:

1. **Reviewer:** inspect the permitted records, raise grounded concerns, and reassess the revised filing and responses.
2. **Filer:** obtain missing company facts, prepare formal responses, and submit concrete document edits.
3. **Independent evaluator:** match concerns to the reference, verify requirements against the final artifacts, and audit unsupported claims and harmful revisions.

Accepted edits persist across exchanges. This makes the final filing an inspectable outcome, with a record of which changes were actually committed.

## Learning Procedures Across Cases

FilingLoop couples the review loop within a case with procedural learning across cases. After a batch is scored, an editor distills requirement-level feedback into separate Reviewer and Filer guidance. The model weights remain unchanged.

The timing matters: **scores are locked before guidance is updated, and new guidance applies only to subsequent cases.** Policies stay frozen within each batch, and scored tasks are never replayed to improve their reported results. All 380 tasks form one evaluation stream, without a separate training or validation split.

This tests whether experience from completed reviews can improve how agents handle later work.

## Results

The fixed-policy and evolving variants share the same backbone and review–revision workflow. Their comparison measures the effect of the cross-case guidance updates on the evaluated stream.

| Metric | FilingLoop–Fixed | FilingLoop–Evolving |
| --- | --- | --- |
| Requirement fulfillment | 24.28% | **27.96%** |
| Full comment resolution | 16.90% | **20.75%** |
| Tasks with every requirement fulfilled | 3.95% | **5.00%** |
| Total system cost | $2,380.15 | $2,519.23 |

Evolution adds **224 fulfilled requirements** and **116 fully resolved comments**, with a **5.8% increase in total cost**. The requirement and comment improvements are 3.68 and 3.85 percentage points, respectively.

Complete resolution remains difficult. Although the evolving system finishes 379 of 380 interactions, only 19 tasks satisfy every requirement. This gap makes checking the final artifacts essential: finishing an interaction does not establish that every disclosure obligation has been met.

The benchmark is predominantly IPO registration review, with only a small annual-report extension. Its scores also depend on model-based evaluation; human–grader agreement and cross-grader sensitivity are not quantified. The results describe the reconstructed tasks and the evaluated stream.

## Read More

- **Paper:** [arXiv:2610.37905](https://arxiv.org/abs/2610.37905)
- **Full text:** [HTML](https://arxiv.org/html/2610.37905v1) · [PDF](https://arxiv.org/pdf/2610.37905)
- **Related work:** [Autogenesis]({% post_url 2026-04-16-autogenesis %}) · [AgentEvolver]({% post_url 2026-07-14-agentevolver %})
