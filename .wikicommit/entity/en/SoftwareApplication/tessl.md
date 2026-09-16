---
title: "Tessl"
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
  description: "A spec-as-source development tool where the specification is the only artifact developers edit directly, and code is entirely generated and regenerated from it."
  applicationCategory: "Spec-as-source development tool"
---

Tessl takes the most radical position on the [[DefinedTerm/spec-driven-development]] spectrum:
spec-as-source, where the specification is the only artifact developers edit directly, and code is
entirely generated from it and regenerated whenever the specification changes. It represents what
its own framing calls specs becoming "the new source code" — developers work in terms of
requirements and behavior, and any change in functionality means changing the specification and
regenerating rather than hand-editing the generated code.

## Adoption & Ecosystem
A 2026 practitioner's survey of spec-driven development tools ([[ScholarlyArticle/from-code-to-contract]])
places Tessl at the spec-as-source end of a three-part toolkit taxonomy that also includes
[[SoftwareApplication/github-spec-kit]] and [[SoftwareApplication/kiro]], noting that this approach
requires mature, trusted code-generation tooling to be practical.
