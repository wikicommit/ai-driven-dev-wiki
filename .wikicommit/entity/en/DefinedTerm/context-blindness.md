---
title: "context blindness"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, context-engineering, terminology, spec-driven-development]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.05278'
    hash: sha256:a9436d2944579fdac4ded1e91308767999c4eba452e3d149c066ac95095750ba
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A failure mode named in Spec Kit Agents in which a coding agent's intermediate artifacts are internally coherent while being incompatible with the repository as it actually exists — producing references to non-existent APIs, file paths that do not exist, and violations of local conventions."
---

Context blindness is the term [[ScholarlyArticle/spec-kit-agents]] gives to a failure mode it says structured agentic workflows do not eliminate: the agent's intermediate artifacts can be internally coherent while being incompatible with the repository as it exists. The distinction it draws is between an artifact that is *wrong* and one that is merely *unmoored* — a specification or plan may be perfectly self-consistent and still refer to nothing real.

## Usage

The symptoms the paper lists are referencing non-existent APIs, proposing file paths that do not exist, and violating local architectural or stylistic conventions. Its account of why the failure matters is about timing rather than frequency: when these errors surface late, during implementation or test execution, the agent often backtracks, revises earlier artifacts, or introduces further inconsistencies — so errors compound across the planning, task-decomposition and implementation stages, producing wasted iterations and unreliable outcomes.

The paper positions the term against the assumption that staged workflows are sufficient on their own. It grants that externalising intermediate artifacts makes intent explicit and provides an audit trail, and that in principle this "reasoning before coding" structure should improve reliability and debuggability — but argues that in practice structure alone does not supply the repository evidence an artifact needs to be compatible with the codebase it targets.

Its proposed remedy follows from that diagnosis: make grounding an explicit workflow operation rather than an in-trajectory behaviour of the same agent that plans and generates. The authors argue that treating grounding as the generating agent's own responsibility leaves it sensitive to prompt design and context-window noise, whereas phase-scoped read-only probing before each stage and artifact validation after it is more repeatable and inspectable.

## Related Terms

The workflow the term was coined to critique is [[DefinedTerm/spec-driven-development]] as implemented in staged form by [[SoftwareApplication/spec-kit]]. See also [[DefinedTerm/context-rot]].
