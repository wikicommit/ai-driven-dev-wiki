---
title: "Code Review as Runtime Monitoring"
type: "schema:DefinedTerm"
lang: en
tags: [agents, code-review, human-oversight]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2602.06310'
    hash: sha256:46f38f583fd26c851dbe000e63a827534bfc88506117ab3f9d5423e0303e5cd8
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A proposal by Aleti, Hoda, Ray, and Chen in [[ScholarlyArticle/trustworthy-ai-software-engineers]] to extend code review in human-AI software engineering teams beyond pre-merge inspection into a continuous, runtime activity, in which deployed code is treated as provisional and AI agents monitor its behaviour in production."
---

Code review as runtime monitoring, proposed in [[ScholarlyArticle/trustworthy-ai-software-engineers]], reframes code review in human-AI software engineering teams so that it no longer ends once code is merged. Under this proposal, deployed code is treated as provisional rather than final: AI agents continuously monitor system behaviour in production, evaluating execution traces, resource usage, security signals, and deviations from expected behaviour, so that trustworthiness is established through sustained behavioural validation rather than a single pre-merge inspection.

## When It Applies

The paper motivates this shift as a response to code review becoming a bottleneck in human-AI teams: the volume of AI-generated artefacts increases substantially, making exhaustive manual pre-merge inspection impractical, while the opacity of AI-generated outputs makes reasoning about their correctness more difficult. It assumes AI agents and monitoring mechanisms are embedded within the system's operational lifecycle, tracking execution behaviour after deployment rather than only static code at merge time. The paper presents this as a proposal in a 2026 vision paper — it states that review becomes "temporally distributed, adaptive, and tightly coupled with system operation," dissolving the boundary between development and deployment — rather than a practice that has been implemented or empirically evaluated.

## Related Terms

[[ScholarlyArticle/trustworthy-ai-software-engineers]], [[DefinedTerm/evidence-centric-inspection]], [[DefinedTerm/agentic-engineer]]
