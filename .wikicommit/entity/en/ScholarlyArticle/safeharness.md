---
title: "SafeHarness: Lifecycle-Integrated Security Architecture for LLM-based Agent Deployment"
type: "schema:ScholarlyArticle"
lang: en
tags: [agent-security, agent-harness, defense-in-depth]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2604.13630'
    hash: sha256:85e01a32f0a72d98737189a748e8ff6d333a07752cfc5afb766b8cdb3ed2bc9d
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paper proposing SafeHarness, a security architecture that weaves four defense layers into the lifecycle of an LLM agent's execution harness, reporting average reductions of about 38% in unsafe behavior rate and 42% in attack success rate against an unprotected baseline."
  author: ["Xixun Lin", "Yang Liu", "Yancheng Chen", "Yongxuan Wu", "Yucheng Ning", "Yilong Liu", "Nan Sun", "Shun Zhang", "Bin Chong", "Chuan Zhou", "Yanan Cao"]
  datePublished: "2026-04-15"
  keywords: ["LLM agents", "execution harness", "agent security"]
---

The paper starts from the observation that the performance of LLM agents depends critically on the execution harness — the system layer that orchestrates tool use, context management and state persistence (see [[DefinedTerm/agent-harness]]). The authors argue that this same architectural centrality makes the harness a high-value attack surface, since a single compromise at the harness level can cascade through the entire execution pipeline, and that existing security approaches suffer from a structural mismatch: they are blind to harness-internal state and cannot coordinate across the different phases of agent operation.

In response they introduce SafeHarness, a security architecture in which four proposed defense layers are woven directly into the agent lifecycle, one per phase, with cross-layer mechanisms tying the layers together. They evaluate it on benchmark datasets across diverse harness configurations, against four security baselines under five attack scenarios spanning six threat categories.

## Key Points

- The paper frames the execution harness itself, rather than the model alone, as a high-value attack surface whose compromise can cascade through the whole execution pipeline.
- It argues that existing security approaches are structurally mismatched to this setting, being blind to harness-internal state and unable to coordinate across phases of agent operation.
- SafeHarness places one defense layer at each lifecycle phase: adversarial context filtering at input processing, tiered causal verification at decision making, privilege-separated tool control at action execution, and safe rollback with adaptive degradation at state update.
- Cross-layer mechanisms escalate verification rigor, trigger rollbacks and tighten tool privileges whenever sustained anomalies are detected.
- Compared to the unprotected baseline, the authors report an average reduction of approximately 38% in unsafe behavior rate (UBR) and 42% in attack success rate (ASR), while preserving core task utility; these figures come from their evaluation against four baselines under five attack scenarios spanning six threat categories.

## Notes

The paper was first submitted to arXiv on 15 April 2026 and revised on 11 May 2026; it is filed under Cryptography and Security (cs.CR) and Artificial Intelligence (cs.AI) and runs to 26 pages with 6 figures.
