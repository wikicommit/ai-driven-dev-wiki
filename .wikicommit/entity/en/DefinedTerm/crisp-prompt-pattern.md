---
title: "CRISP prompt pattern"
type: "schema:DefinedTerm"
lang: en
aliases: ["CRISP"]
tags: [prompting, spec-driven-development]
sources:
  - type: url
    url: 'https://carlosazaustre.es/blog/spec-driven-development-agentes-ia'
    hash: sha256:b17e6ce9fa2310498982db3cbb22fd38907d0a482aa53268416a2149e5083282
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A five-part structure for a coding-agent prompt — Context, Role, Instructions, Specifications, Polish/Criteria — presented as a way to avoid the reasoning-token cost of vague requests."
---

The CRISP pattern is a five-part structure for writing a request to a coding agent, presented in
[[BlogPosting/from-vibe-coding-to-spec-driven-development]] as the alternative to a vague intent such
as "the login doesn't work, fix it". Its letters stand for **Context** (the exact environment the code
runs in), **Role** (the identity the agent should assume), **Instructions** (exactly what it should
do), **Specifications** (protocols, APIs, types and constraints) and **Polish/Criteria** (the
definition of done and the acceptance criteria).

## Usage

That post's worked contrast sets a one-line lazy prompt beside a CRISP one that names the file, the
method, the line where the error is raised and the condition that triggers it, says which existing
error handler to use, and forbids creating new files. It uses the pattern within an account of
[[DefinedTerm/spec-driven-development]], where the precision of what is handed to the agent is treated
as engineering work in its own right, and sums the point up as writing the prompt well being "ingeniería de costes" — cost
engineering.

## When It Applies

The pattern is aimed at the case the post describes as expensive: an imprecise request that forces the
model to explore files blindly and reformulate hypotheses until it lands on something useful. The
post's claim is that the difference is economic as well as a matter of code quality — that a vague
prompt can consume orders of magnitude more reasoning tokens than a precise one to reach the same
result, with more errors.

How established it is: the only account held here is that one post, which presents the pattern
without attributing it to a named originator and offers its cost claim as a general statement rather
than a measurement.

## Related Terms

- [[DefinedTerm/prompt-engineering]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/spec-driven-development]]
