---
title: "GitHub Spec Kit"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, spec-driven-development]
sources:
  - type: url
    url: https://arxiv.org/pdf/2602.00180
    hash: sha256:982804fd917021d4811f4b23fc3ada9dfc07e4c91add2e07b32b2ffa9aad4253
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An open-source toolkit providing commands for spec-driven AI development, structuring the workflow into four explicit, human-gated phases: Specify, Plan, Tasks, and Implement."
  applicationCategory: "Spec-driven AI development toolkit"
  featureList: "Four-phase workflow (/specify, /plan, /tasks, implement) with human review and refinement required between phases; optional clarification, analysis and checklist commands; integrations across multiple code agents and IDEs"
  author: "GitHub"
---

GitHub Spec Kit is an open-source toolkit for [[DefinedTerm/spec-driven-development]], structuring
the workflow around AI coding assistants into four explicit, gated phases. `/specify` generates a
detailed specification from a prompt, `/plan` creates the technical architecture, `/tasks` breaks
the plan into implementation tasks, and a final implementation step generates code task by task. At
each phase, a human reviews and refines the output before the workflow proceeds to the next one,
which is intended to keep the agent's output aligned with intent throughout the process rather than
only checked at the end.

## Capabilities

[[ScholarlyArticle/from-prompt-to-process]] describes the repository as organising commands such as
constitution, specification, plan, tasks and implementation, plus optional clarification, analysis and
checklist commands. It reports the toolkit's central idea, per Spec Kit's own documentation, as:
describe what to build, refine through structured phases, and let code agents implement from those
artifacts — with the specification acting as a source of truth rather than a disposable document.

## Adoption & Ecosystem

A 2026 practitioner's survey of spec-driven development tools ([[ScholarlyArticle/from-code-to-contract]])
categorizes GitHub Spec Kit, alongside [[SoftwareApplication/kiro]] and [[SoftwareApplication/tessl]],
as one of three representative AI-assisted SDD toolkits that structure coding workflows explicitly
around specifications.

Under the [[DefinedTerm/six-dimension-process-taxonomy]], Spec Kit scores 2 on specification, 1 on
context, 1 on roles, 1 on execution, 1 on validation and 2 on portability — a total of 8 out of 12.
That study reads the profile as high portability bought at the cost of roles and validation: it puts
Spec Kit alongside [[SoftwareApplication/openspec]] as one of two SDD toolkits competing on the same
ground, with Spec Kit the more complete in phases and portability and OpenSpec the lighter. The scores
express that study author's judgement from official documentation rather than an independent empirical
measurement, and the study records that Spec Kit had not been through independent academic evaluation.

The fragility that study names is dependence on interpretation: a clear specification helps, but does
not guarantee that implementation, tests and maintenance stay aligned without additional checks, and
the dominant risk it records for Spec Kit is drift between the artifacts and the implementation where
validation is weak.
