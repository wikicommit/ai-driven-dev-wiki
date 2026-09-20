---
title: "Agentic Code Review"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, agents]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2607.13196'
    hash: sha256:1635571abac83780f1fe27a5b0def652bdd5addba148b5a72857e7b29a0c3c98
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The third of three code review eras identified in an empirical study of GitHub projects: a review process in which AI agent reviewers participate alongside human reviewers, following human-centric review and LLM-assisted review."
---

Agentic code review is the name given in
[[ScholarlyArticle/from-human-centric-to-agentic-code-review]] to the most recent of three code
review eras a project may pass through. That study distinguishes human-centric review, in which
review is primarily a human process; LLM-assisted review; and agentic code review, in which AI
agent reviewers participate in the review process alongside human reviewers and large language
model reviewers. The eras are identified empirically, from 1.02 million reviewed pull requests in
207 GitHub projects that transition across them.

## Usage

The term is used to mark an era or phase of a project's review practice rather than a particular
tool. In the study that introduces it, projects are characterized by which of three adoption
practices they follow into that era — Gradual AI Adoption, Rapid LLM Adoption, or Rapid AI Agent
Adoption — and review discussions are modelled as sequences of interactions between human, LLM and
agent reviewers.

What the study reports about the era is a split: agent-involved collaboration patterns, especially
reviews initiated by AI agents or involving multiple AI agents, are associated with faster review
decisions under two of those adoption practices, but the authors state that the efficiency gains do
not translate into better review quality.

## Related Terms
- [[DefinedTerm/code-review-agent]]
- [[DefinedTerm/review-bottleneck]]
- [[DefinedTerm/code-review-as-runtime-monitoring]]
- [[DefinedTerm/ai-coding-agent]]
