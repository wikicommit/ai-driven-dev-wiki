---
title: "Context Blindness"
type: "schema:DefinedTerm"
lang: en
tags: [agents, spec-driven-development, context-engineering, agent-architecture]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.05278'
    hash: sha256:a9436d2944579fdac4ded1e91308767999c4eba452e3d149c066ac95095750ba
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A failure mode of agentic coding workflows in which the agent's intermediate artifacts are internally coherent but incompatible with the repository as it actually exists — referencing APIs or file paths that are not there, or violating local conventions."
---

Context blindness is the name given in
[[ScholarlyArticle/spec-kit-agents-context-grounded-agentic-workflows]] to a failure mode that
survives the adoption of a structured agentic workflow. An agent's intermediate artifacts — a
specification, an implementation plan, a task checklist — can be internally coherent and still be
incompatible with the repository as it exists. The term names the mismatch between artifact and
codebase specifically, rather than incoherence within the artifact itself, which is what makes it
survive workflow structure: a specification can be reviewed for internal consistency and pass, while
the repository it describes does not match it.

## Usage

The source that introduces the term lists three symptoms: referencing non-existent APIs, proposing
file paths that do not exist, and violating local architectural or stylistic conventions. It
lists, among the reasons multi-step tasks fail in evolving codebases, missing context about the
current architecture, stale assumptions about dependencies, and mismatches with repository
conventions.

What makes the condition costly, on that account, is when it is discovered rather than that it occurs.
The errors surface late, during implementation or test execution, at which point the agent backtracks,
revises earlier artifacts, or introduces further inconsistencies. The failures therefore
compound across stages such as planning, task decomposition and implementation, which that source
describes as producing wasted iterations and unreliable outcomes.

The term is introduced to motivate a remedy, so it carries an implied diagnosis: that grounding
treated as an in-trajectory behavior of the same agent that plans and generates is sensitive to prompt
design and context-window noise. The response proposed alongside it is to make grounding and
validation explicit workflow operations — probing the repository before each phase and checking each
intermediate artifact against the environment after it — so that a plan referencing a path that does
not exist is caught before code is generated from it.

As a term it is new and rests on a single source, which uses it to frame its own contribution rather
than establishing it as a term others already use.

## Related Terms

- [[ScholarlyArticle/spec-kit-agents-context-grounded-agentic-workflows]] — the source that introduces
  the term and proposes context-grounding hooks against it
- [[DefinedTerm/spec-driven-development]] — the practice whose staged workflow this failure mode
  survives
- [[DefinedTerm/context-engineering]] — the broader concern with what an agent is given to work from
