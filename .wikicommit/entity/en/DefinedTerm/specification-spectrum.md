---
title: "specification spectrum"
type: "schema:DefinedTerm"
lang: en
tags: [ai-assisted-programming, specification, software-development-process, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2602.00180v1'
    hash: sha256:982804fd917021d4811f4b23fc3ada9dfc07e4c91add2e07b32b2ffa9aad4253
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A three-level taxonomy of specification rigor proposed by Piskala — spec-first, spec-anchored, and spec-as-source — arranged along an axis of increasing specification authority over code, where moving toward higher authority also increases the discipline required to keep spec and code aligned."
---

The specification spectrum is a taxonomy of specification rigor set out in [[ScholarlyArticle/spec-driven-development-from-code-to-contract]], which argues that not all spec-driven approaches are equal and that teams adopt different levels of rigor depending on their needs, tooling, and domain constraints. It runs from traditional code-first development through three named levels — spec-first, spec-anchored, and spec-as-source — with each step to the right increasing the authority of specifications over code, and also increasing the discipline required to maintain alignment.

## Usage

| Level | Source of truth | Characteristic |
| --- | --- | --- |
| Code-first (ad-hoc) | Code | Code first, docs later; drift is common |
| Spec-first | Spec initially, then code | Spec guides the initial build and may then be abandoned |
| Spec-anchored | Spec and code as equal partners | Spec is maintained alongside code; synchronization is enforced by tests |
| Spec-as-source | Spec | Spec is the code; code is generated and never hand-edited |

**Spec-first** is described as the entry point to the practice: a specification is written before coding to guide the initial implementation, typically as a user story with acceptance criteria, a BDD scenario, or a detailed requirements document. Once code exists, the spec may or may not be maintained — the primary value is the initial clarity it provides. The report argues this works particularly well for initial feature development with AI coding assistants, since the upfront spec prevents the AI from guessing at requirements, and for prototypes and one-off features where maintaining a spec indefinitely is not justified. Its stated limitation is that it does not protect against drift over time.

**Spec-anchored** treats the spec as a living document that evolves with the codebase: changes to behavior require updating both, and automated checks derived from the spec ensure the two remain aligned, so that drift causes test failures rather than passing silently. The report names this the sweet spot for most production systems, since it provides clear documentation and verifiable requirements without demanding that code be fully generated from specifications. It cites BDD frameworks such as Cucumber, and OpenAPI specifications paired with contract testing tools, as exemplifying the level.

**Spec-as-source** is presented as the most radical form: the specification is the only artifact humans edit directly, code is entirely generated and should never be manually modified, and any behavior change means changing the spec and regenerating. The report notes that drift is eliminated by design here, because spec and code are always aligned by construction. It observes that this is already standard practice in domains with well-defined code generation — generating API server stubs from OpenAPI specifications, or producing certified embedded code from Simulink models — and that adopting it more broadly requires high trust in generation quality.

The report pairs the spectrum with a decision framework and a stated rule of thumb it calls the Golden Rule: use the minimum level of specification rigor that removes ambiguity for your context — spec-first for AI-assisted initial development, spec-anchored for long-lived production systems, and spec-as-source only when generation tooling is mature and trusted.

## Related Terms

The spectrum is the organizing taxonomy of [[DefinedTerm/spec-driven-development]]. The same report distinguishes SDD-style specs from traditional High-Level Design and Low-Level Design documents on the grounds that the difference lies not in what is written but in how it is used: traditional design documents are advisory, whereas SDD specs are enforced, with tests failing when code diverges.
