---
title: "GitHub Spec Kit"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, spec-driven-development]
sources:
  - type: url
    url: https://arxiv.org/pdf/2602.00180
    hash: sha256:982804fd917021d4811f4b23fc3ada9dfc07e4c91add2e07b32b2ffa9aad4253
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "An open-source toolkit providing commands for spec-driven AI development, structuring the workflow into four explicit, human-gated phases: Specify, Plan, Tasks, and Implement."
  applicationCategory: "Spec-driven AI development toolkit"
  featureList: "Four-phase workflow (/specify, /plan, /tasks, implement) with human review and refinement required between phases"
  author: "GitHub"
---

GitHub Spec Kit is an open-source toolkit for [[DefinedTerm/spec-driven-development]], structuring
the workflow around AI coding assistants into four explicit, gated phases. `/specify` generates a
detailed specification from a prompt, `/plan` creates the technical architecture, `/tasks` breaks
the plan into implementation tasks, and a final implementation step generates code task by task. At
each phase, a human reviews and refines the output before the workflow proceeds to the next one,
which is intended to keep the agent's output aligned with intent throughout the process rather than
only checked at the end.

## Adoption & Ecosystem
A 2026 practitioner's survey of spec-driven development tools ([[ScholarlyArticle/from-code-to-contract]])
categorizes GitHub Spec Kit, alongside [[SoftwareApplication/kiro]] and [[SoftwareApplication/tessl]],
as one of three representative AI-assisted SDD toolkits that structure coding workflows explicitly
around specifications.
