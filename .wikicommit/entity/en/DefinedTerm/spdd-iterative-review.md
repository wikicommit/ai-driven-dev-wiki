---
title: "Iterative Review (Structured-Prompt-Driven Development)"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, spec-driven-development, ai-assisted-programming]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/structured-prompt-driven/iterative-review.html'
    hash: sha256:cb389fcf642701a177954fd2765262d1a96e71b350b21a0bcbd9cdac3cdc1f75
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A practice in Wei Zhang and Jessie Jie Xia's Structured-Prompt-Driven Development (SPDD) that turns AI-generated output into a controlled review-and-iterate loop, keeping the structured prompt and the code in sync and validating behaviour before reviewing the code in depth."
---

Iterative Review is a practice described in Structured-Prompt-Driven Development (SPDD), by Wei Zhang
and Jessie Jie Xia, for making AI assistance behave like an engineering process rather than a one-shot
draft: AI output is put through a disciplined loop of review and iteration in which fixes are made by
updating the structured prompt and regenerating, not by patching the code by hand. The authors frame it
against two failure modes of working without such a loop — forcing the model to keep patching until the
solution drifts, or restarting repeatedly and losing control of cost and time.

## Usage

The practice names four areas to focus on during review: consistency between prompt and code (the
specification stays ahead of the implementation, so a logic change updates the structured prompt
first); architecture and responsibility boundaries (layering discipline and clean contracts between
interfaces and implementations); cross-cutting engineering standards (exception handling, encapsulation
of object construction inside domain objects, obvious code smells such as magic numbers and long
methods, and team-specific conventions); and hallucination and correctness checks (whether the code
implements what the prompt describes, whether imports and dependencies are correct and minimal, and
whether invented APIs or wrong assumptions cause syntax or compilation errors).

It calls for four capabilities: prompt debugging, functional validation by running the system locally
against business expectations, deep code review once functionality is correct, and asset integrity —
committed code mapping cleanly to the exact prompt version, so future changes stay traceable.

## When It Applies

- **Conditions**: work in which code is generated from a structured prompt that acts as the
  specification, as in SPDD.
- **Assumptions**: the structured prompt is treated as a first-class source artifact ("prompt as
  code"), so every requirement change or bug fix updates the prompt and the code together; and the
  system can be run locally for hands-on validation.
- **Ordering**: "run first, review second" — correct behaviour is the first quality gate, the prompt is
  iterated on until the system behaves as expected, and only then is effort put into deeper code-level
  review.
- **Failure modes**: the ones it is meant to prevent — patching generated code until it drifts from the
  intended solution, or regenerating from scratch repeatedly without converging.
- **Establishment**: one part of a single methodology proposed by its two authors; the material states
  the practice as guidance and does not report evidence of its effect.

## Related Terms

- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/prompt-debt]]
