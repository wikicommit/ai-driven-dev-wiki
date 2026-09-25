---
title: "Reasoning Sandwich"
type: "schema:DefinedTerm"
lang: en
tags: [reasoning-models, harness-engineering, agentic-coding]
sources:
  - type: url
    url: 'https://blog.langchain.com/improving-deep-agents-with-harness-engineering/'
    hash: sha256:7628e7920b4c219963d45c07cb27a6039a14ef5a60f3939b0ccb424dd7481ddd
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "LangChain's name for a heuristic that allocates a reasoning model's compute unevenly across an agent's work — the highest reasoning setting for planning and for verification, a lower one for implementation in between."
---

A reasoning sandwich is a heuristic, named in LangChain's
[[BlogPosting/improving-deep-agents-with-harness-engineering]], for deciding how much reasoning compute
an agent spends at each stage of a task: more at the start, for planning, and at the end, for
verification, and less for the implementation between them. LangChain's version, for a model offering
`low`, `medium`, `high` and `xhigh` reasoning modes, was `xhigh` for planning, `high` for implementation
and `xhigh` for verification.

## Usage

The term comes from harness design for long-running coding agents, where reasoning models can run for
hours and a harness has to decide how much compute each subtask gets. LangChain's reasoning was that
more reasoning helps an agent fully understand a difficult problem and build a good plan, and helps
late-stage verification catch mistakes before a solution is submitted — but that it can also burn over
twice the tokens and time. Under Terminal Bench's time limits, running the whole task at `xhigh` scored
53.9% because agents timed out, against 63.6% at `high`; the team reports no large differences between
different splits of the reasoning budget in trial runs, and kept the sandwich as its baseline.

## When It Applies

It assumes a model whose reasoning effort can be set per call (see [[DefinedTerm/reasoning-effort]]) and
a task with a binding time or cost budget, which is what made spending maximum reasoning everywhere
counterproductive in LangChain's setting. It is one team's heuristic from its own benchmark runs, not an
established practice. The same post names adaptive reasoning — as in Claude and Gemini models, where the
model itself decides how much to reason — as the natural alternative, and suggests that in a multi-model
harness the same balancing could instead mean planning with a large model and handing implementation off
to a smaller one.

## Related Terms

- [[DefinedTerm/reasoning-effort]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/verification-loop]]
