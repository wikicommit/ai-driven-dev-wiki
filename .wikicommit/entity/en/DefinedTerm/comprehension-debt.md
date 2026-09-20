---
title: "Comprehension Debt"
type: "schema:DefinedTerm"
lang: en
tags: [technical-debt, software-engineering, cognition]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2604.13277'
    hash: sha256:941128b107d96f25f94ea6be7d597cefea10e55de8abf1cfeaaad7845fa60ee4
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The growing gap between what a development team knows about its codebase and what it actually needs to understand in order to maintain and modify it effectively — proposed as a socio-cognitive risk of generative AI tool adoption."
---

Comprehension Debt (CD) is the growing gap between what a development team knows about its codebase
and what it actually needs to understand in order to maintain and modify that codebase effectively.
The term is proposed in [[ScholarlyArticle/comprehension-debt-in-genai-assisted-software-engineering-projects]],
which frames it as a socio-cognitive risk introduced by the adoption of generative AI tools in
software development: such tools reduce cognitive load, and the understanding that would otherwise
have been built in the course of doing the work is not built. That paper argues the concept is
distinct from traditional technical debt, because it resides in the collective cognition of a
development team rather than in the codebase itself.

## Usage

The proposing study describes four patterns by which Comprehension Debt accumulates, observed in an
undergraduate software engineering project: AI-as-black-box code acceptance, in which generated code
is taken without being understood; context-mismatch debt; dependency-induced atrophy; and
verification-bypass. It also names one mitigating pattern, in which the same tools are used as a
comprehension scaffold and the developer builds a deeper understanding of the code through the
interaction rather than around it.

Because the debt sits in what a team collectively knows rather than in what it has written, the
study's proposed responses are practices rather than code changes: verification practices,
structured retrospectives, and active learning assessments.

## Related Terms
- [[DefinedTerm/cognitive-debt]]
- [[DefinedTerm/verification-debt]]
- [[DefinedTerm/skill-atrophy]]
- [[DefinedTerm/automation-bias]]
