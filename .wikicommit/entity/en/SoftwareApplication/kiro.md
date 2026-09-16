---
title: "Kiro"
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
  description: "Amazon's agentic AI development tool, which guides users through requirements, design, and task-creation stages before any code generation begins."
  applicationCategory: "Spec-driven AI development tool"
  author: "Amazon Web Services"
---

Kiro is Amazon Web Services' agentic AI development tool, which stages a coding session through
requirements capture, design, and task creation before any code generation begins. It emphasizes
structured requirements capture and iterative refinement, ensuring the AI has clear context before
attempting implementation; the explicit staging is intended to prevent the AI from guessing at
requirements that were never specified, the same problem [[DefinedTerm/spec-driven-development]]
addresses more generally.

## Adoption & Ecosystem
A 2026 practitioner's survey of spec-driven development tools ([[ScholarlyArticle/from-code-to-contract]])
categorizes Kiro, alongside [[SoftwareApplication/github-spec-kit]] and [[SoftwareApplication/tessl]],
as one of three representative AI-assisted SDD toolkits.
