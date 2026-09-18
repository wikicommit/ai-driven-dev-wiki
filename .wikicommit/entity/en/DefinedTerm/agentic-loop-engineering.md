---
title: "Agentic Loop Engineering (ALE)"
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
  description: "The engineering activity proposed in Structured Agentic Software Engineering (SASE) for governing how agents execute tasks — defining task decomposition, parallelization, required rigor, and evidence-based acceptance criteria as a declarative LoopScript, rooted in DevOps practice."
---

Agentic Loop Engineering (ALE) is one of the structured engineering activities proposed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] as part of [[DefinedTerm/structured-agentic-software-engineering]] (SASE). The paper describes ALE as deeply rooted in the principles pioneered by the DevOps community, transforming an agent's work from an opaque, black-box process into a disciplined, auditable, reproducible workflow that moves beyond simple iterative cycles like the [[DefinedTerm/plan-do-assess-review]] (PDAR) loop.

## Usage

The paper assigns the workflow's definition to the human coach within the [[DefinedTerm/agent-command-environment]] (ACE), while agents execute it within the [[DefinedTerm/agent-execution-environment]] (AEE); its artifact is the [[DefinedTerm/loopscript]]. Its stated purpose is defining how agents work together (or alone), the patterns of their collaboration, and how they engage their toolset — since agents cannot infer the "stakes" of a task on their own. The paper's research roadmap for this activity calls for a declarative LoopScript language capturing task decomposition, parallel execution, review checkpoints, escalation rules, and evidence requirements, building on business-process and DevOps automation but with stronger links to code, tests, risk, and human review; interaction mechanisms letting a coach pause a workflow, redirect a branch, add context, or stop low-value work without restarting the whole loop; and standards for sufficient evidence in a [[DefinedTerm/merge-readiness-pack]], plus more informative tool feedback (structured compiler diagnostics, test failures, or static-analysis findings) to guide agents' search.

## Related Terms

[[DefinedTerm/loopscript]], [[DefinedTerm/plan-do-assess-review]], [[DefinedTerm/structured-agentic-software-engineering]]
