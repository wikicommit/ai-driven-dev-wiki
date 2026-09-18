---
title: "LoopScript"
type: "schema:DefinedTerm"
lang: en
tags: [sase]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A declarative, version-controlled artifact proposed in Structured Agentic Software Engineering (SASE) that lets a human coach define an agent workflow's task decomposition, level of rigor, and evidence requirements as a Standard Operating Procedure, replacing ad-hoc prompt hacking."
---

A LoopScript is the artifact [[DefinedTerm/structured-agentic-software-engineering]] (SASE) proposes for defining how agents execute a task, introduced in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] as the product of [[DefinedTerm/agentic-loop-engineering]] (ALE). The paper motivates it by noting that agents cannot infer the "stakes" of a task on their own — they may "overthink" a simple request or under-deliver on a critical one — so a coach needs an explicit way to communicate the required level of rigor.

## Usage

A LoopScript can specify task decomposition and parallelization (assigning one [[DefinedTerm/briefingscript]] to multiple agents or a heterogeneous team of specialized agents, enabling N-version programming — e.g. a developer resolving seven tickets triggering 28 parallel pull requests, four per ticket), workflow strategy (granting full autonomy for a simple bug fix while enforcing a strict, multi-stage review process for a critical security patch), and evidence-based acceptance criteria (defining the structure of the final deliverable, a [[DefinedTerm/merge-readiness-pack]]). The paper describes it as a living document a coach can dynamically adjust, for instance allocating more agents to a promising path or adding a review checkpoint if early results look uncertain, and frames it as a direct descendant of DevOps practices — declarative pipelines, infrastructure-as-code, and observability. It notes that some frontier coding agents already show elements of this: Google's [[SoftwareApplication/google-jules]] has included a planning step from its inception, while Anthropic's [[SoftwareApplication/claude-code]] only recently added an on-demand planning mode in which the agent generates a plan and awaits human review before proceeding.

## Related Terms

[[DefinedTerm/agentic-loop-engineering]], [[DefinedTerm/briefingscript]], [[DefinedTerm/merge-readiness-pack]]
