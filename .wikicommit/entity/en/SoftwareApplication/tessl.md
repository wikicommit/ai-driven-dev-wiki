---
title: "Tessl"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, spec-driven-development]
sources:
  - type: url
    url: https://arxiv.org/pdf/2602.00180
    hash: sha256:982804fd917021d4811f4b23fc3ada9dfc07e4c91add2e07b32b2ffa9aad4253
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/sdd/overview/'
    hash: sha256:946cf421ab8284921cee80b48fc236a89feb6dfd5c4a90f01ae072227495be73
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A spec-as-source development tool where the specification is the only artifact developers edit directly, and code is entirely generated and regenerated from it. A second source describes it as experimental and documents the reverse direction as well: deriving a specification from existing code."
  applicationCategory: "Spec-as-source development tool"
  featureList: "specification as the single edited artifact, with code regenerated from it; a documented command for deriving a specification from existing code; a GENERATED FROM SPEC - DO NOT EDIT marker on generated code; @generate and @test tags controlling generation"
---

Tessl takes the most radical position on the [[DefinedTerm/spec-driven-development]] spectrum:
spec-as-source, where the specification is the only artifact developers edit directly, and code is
entirely generated from it and regenerated whenever the specification changes. The report that places
it there says Tessl represents what that report calls the emerging vision of specs as "the new source
code" — developers work in terms of requirements and behavior, and any change in functionality means
changing the specification and regenerating rather than hand-editing the generated code.

## Capabilities

A chapter of Jimmy Song's online handbook 智能体构建指南 describes it as an experimental framework and
records three concrete mechanisms. It documents a `tessl document --code` command that works in the
reverse direction from the one above, deriving a specification from code that already exists. It
states that generated code carries a `// GENERATED FROM SPEC – DO NOT EDIT` marker, which is how the
spec-as-source boundary is made visible in the tree itself rather than only in the workflow. And it
names `@generate` and `@test` tags used to control what generation does. That account places Tessl as
an early form of the move toward spec-as-source rather than a finished one.

## Adoption & Ecosystem

A 2026 practitioner's survey of spec-driven development tools ([[ScholarlyArticle/from-code-to-contract]])
places Tessl at the spec-as-source end of a three-part toolkit taxonomy that also includes
[[SoftwareApplication/github-spec-kit]] and [[SoftwareApplication/kiro]], noting that this approach
requires mature, trusted code-generation tooling to be practical. The handbook chapter above lists it
among eight representative implementations of the practice, the same three among them.
