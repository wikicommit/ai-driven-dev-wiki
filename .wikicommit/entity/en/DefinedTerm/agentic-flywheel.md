---
title: "Agentic flywheel"
type: "schema:DefinedTerm"
lang: en
tags: [coding-agents, harness-engineering, human-oversight]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/humans-and-agents.html'
    hash: sha256:767b9a865639b9476811d14704d9d23901875bda1ac1263f9794e9aa70ba663c
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A stage described by Kief Morris beyond humans working on the loop, in which humans direct agents to evaluate the performance of the development loop and to recommend, and eventually apply, improvements to their own harness."
---

The agentic flywheel is, in [[BlogPosting/humans-and-agents-in-software-engineering-loops]], the
level beyond [[DefinedTerm/humans-on-the-loop]]: instead of improving the agent's harness by hand,
humans direct agents to manage and improve it. Agents are given the information they need to evaluate
how the loop performs, review the results of each workflow step, and recommend improvements to any
upstream part of the workflow that could improve those results — so that, in the article's words,
the agent harness "generates recommendations for improving itself."

## Usage

The article's starting point for the signals is the tests and evaluations already in the harness. It
suggests the flywheel becomes more powerful with richer signals: pipeline stages that measure
performance and validate failure scenarios, and operational data from production, user journey logs
and commercial results.

## When It Applies

The article describes adopting it gradually. Humans first consider the recommendations interactively
and prompt agents to implement specific changes, or have agents add recommendations to the product
backlog to be prioritised, scheduled, and then applied and tested by agents in the automated flow. As
confidence grows, agents can score their recommendations for risks, costs and benefits, and
recommendations with certain scores might be approved and applied automatically. The author suspects
that for standard, frequently done work this could end up looking much like humans out of the loop,
once the improvement loops reach diminishing returns, but argues that it yields robust, "maybe even
anti-fragile" systems that continuously improve themselves. This is a forward-looking proposal by
one author, not a reported measured result.

## Related Terms

- [[DefinedTerm/humans-on-the-loop]]
- [[DefinedTerm/harness-engineering]]
