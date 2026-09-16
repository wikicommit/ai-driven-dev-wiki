---
title: "From Code to Contract: Spec-Driven Development in the Age of AI Coding Assistants"
type: "schema:ScholarlyArticle"
lang: en
tags: [spec-driven-development, ai-assisted-coding, software-engineering]
sources:
  - type: url
    url: https://arxiv.org/pdf/2602.00180
    hash: sha256:982804fd917021d4811f4b23fc3ada9dfc07e4c91add2e07b32b2ffa9aad4253
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A practitioner's guide to spec-driven development (SDD) for AI coding assistants, defining three levels of specification rigor, a four-phase Specify/Plan/Implement/Validate workflow, and a decision framework for when SDD is worth adopting."
  author: "Deepak Babu Piskala"
  datePublished: "2026-01-30"
  keywords: ["Spec-Driven Development", "AI-Assisted Coding", "Behavior-Driven Development", "Test-Driven Development", "API Design First", "Software Specifications"]
---

This technical report argues that AI coding assistants make spec-driven development (SDD) —
treating specifications, not code, as the primary artifact of software development — newly
relevant, because large language models are good at pattern completion but cannot read a
developer's mind: an unspecified prompt leaves format, permissions, and edge cases to guesswork,
while a specification gives the model enough information to match intent. It defines three levels
of specification rigor along a spectrum — spec-first, spec-anchored, and spec-as-source — and a
four-phase workflow common across the SDD tooling it surveys: Specify (what to build), Plan (how to
build it), Implement (build it), and Validate (verify it), with human review at each checkpoint.

The paper surveys tools across this spectrum, from BDD/TDD frameworks and API specification tools
through contract-testing tools to AI-assisted SDD toolkits — [[SoftwareApplication/github-spec-kit]],
[[SoftwareApplication/kiro]], and [[SoftwareApplication/tessl]] — and model-based design tools for
certified embedded code. Three case studies illustrate the approach: an API-first microservices
adoption, a Cucumber-based BDD adoption for enterprise features, and a Simulink-based spec-as-source
workflow for automotive engine control certified to ISO 26262.

## Key Points
- Proposes three levels of specification rigor — spec-first (a spec guides only the initial
  implementation and may then drift), spec-anchored (the spec is maintained alongside the code
  throughout its lifecycle, kept in sync by automated checks), and spec-as-source (the spec is the
  only artifact humans edit directly; code is entirely generated and regenerated from it) — as a
  spectrum teams can position themselves on rather than a single practice
- Describes a four-phase SDD workflow (Specify, Plan, Implement, Validate) common across the
  surveyed tooling, with human review as a checkpoint between phases
- Reports, citing two studies, that human-refined specifications improve LLM-generated code
  quality, with controlled studies showing error reductions of up to 50%
- Proposes a decision framework for when SDD is worth its overhead: valuable for AI-assisted
  development, complex requirements, systems with multiple maintainers, integration-heavy systems,
  regulated domains, and legacy modernization; likely overkill for throwaway prototypes, solo
  short-lived projects, exploratory coding, and simple CRUD applications
- Argues SDD is an evolution of existing practices (TDD, BDD, API-first design, Design by Contract)
  rather than a new discipline, differing mainly in making specifications executable and enforced
  through tests and CI rather than advisory

## Notes
- This is a self-published technical report (the author is listed as based in Seattle, USA) rather
  than a peer-reviewed publication; its case studies are presented as illustrative examples rather
  than the paper's own original empirical study, and its cited error-reduction figures are drawn
  from other studies it references rather than measured by the author
- Frames itself as extending rather than replacing existing practices, describing Test-Driven
  Development as SDD at the unit level and Behavior-Driven Development as its most direct ancestor
