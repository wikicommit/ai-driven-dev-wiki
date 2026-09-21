---
title: "miniMaster"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-architecture, agent-tooling, multi-agent]
sources:
  - type: url
    url: 'https://github.com/datawhalechina/self-harness'
    hash: sha256:1cbe56dd3adc95cae9abae32a6356996fc03b56f4bdeb88b44cae256d918dd66
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The minimal harness implementation that accompanies the self-harness tutorial, built to show which parts a continuously running agent system is actually made of."
  applicationCategory: "Agent harness"
  author: "Datawhale"
  featureList: "System tool layer; prompt and action protocol; segmented working memory; three-tier nested agent loop"
---

miniMaster is the minimal harness practice project that accompanies
[[CreativeWorkSeries/self-harness]], the Datawhale tutorial on
[[DefinedTerm/harness-engineering]]. Its code ships in the same repository as the tutorial
text, and its purpose is pedagogical: it separates task modelling, prompt construction, the
action protocol, runtime memory, the validation loop and the tool system into distinct
modules so that a reader can see which parts a continuously running agent system is made of.

The tutorial presents it as the hands-on route to building a minimal system of the kind
[[SoftwareApplication/claude-code]] represents, and states that the practice section shows how
harness theory is applied in actual development.

## Capabilities

miniMaster's tool layer offers a set of basic system tools — shell execution, and reading,
writing and editing files — alongside search and retrieval tools for globbing and grepping,
all managed uniformly through a shared tool-context, tool-specification and tool-service core
rather than wired in ad hoc.

Prompt construction, the per-role action policies, and the native function-call protocol are
kept in separate modules, which the project describes as the way it keeps a prompt's
description of what an agent may do consistent with the action boundary actually enforced.

Working memory is segmented rather than kept as one transcript: the planning, generation and
validation roles each hold their own memory, and retried tasks are archived separately. The
stated reason is that this retains the context each role needs while allowing older
trajectories to be compressed.

Its control flow is a three-tier nested loop — a Planner agent doing global scheduling, an
Executor agent carrying out the work, and a Validator agent assessing it — the structure this wiki records as
[[DefinedTerm/planner-executor-reviewer]], though the project does not use that name. The project pairs that structure with a
completion checklist, a guard against repeating the same action, and the retry archive, which
together are what it describes as closing the loop stably.

## Adoption & Ecosystem

miniMaster ships as the tutorial's practice project, and shares the Alpha status and the Creative
Commons Attribution–NonCommercial–ShareAlike 4.0 International
licence of the tutorial it belongs to. The repository includes worked runs with their full
logs, showing the three agent roles working through a question about the project's own
codebase.
