---
title: "Creation-to-Verification Shift"
type: "schema:DefinedTerm"
lang: en
tags: [software-engineering, human-oversight, code-review]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.23135'
    hash: sha256:3e017ddd415719f2210ad1a5afb381f4f70a87438df16f7b32b5c7121db023a7
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A reported change in software engineers' perceived task focus under AI coding assistants, in which the relative balance of their effort moves from creation tasks (designing, writing and refactoring code) toward verification tasks (reviewing, testing and debugging)."
---

The creation-to-verification shift is the term Annie Vella and Kelly Blincoe use, in
[[ScholarlyArticle/impact-of-ai-coding-assistants-on-software-engineering]], for a change in where
software engineers using AI coding assistants perceive their effort going: the relative balance
moves away from creation tasks and toward verification tasks. Their conclusion is that development
work is being reorganised rather than simply accelerated.

## Usage

The study groups six core development tasks into two theoretically motivated sets based on the Vee
model: creation tasks (designing, writing and refactoring code) and verification tasks (reviewing,
testing and debugging). Across two questionnaires six months apart, most engineers perceived
spending less time on almost all of these tasks, with writing code falling furthest — 82% reported
spending less time on it. Among the 88 matched participants, neither group changed significantly
in isolation, but the balance between them (verification minus creation) shifted significantly
toward verification, with a moderate effect size; decreased creation combined with increased
verification was the most common individual pattern.

The authors note that the shift is modest in absolute terms: reviewing code was the only task whose
mean sat above neutral, and testing remained below neutral throughout, though it trended upward.
Since the increase in verification did not account for the reduction in creation, they propose that
the remaining effort flows into [[DefinedTerm/supervisory-engineering-work]] — directing, evaluating
and correcting AI output — which engineers may not recognise as traditional testing or code review.

As implications, the authors suggest that engineers prepare for less time writing code and more
time directing and evaluating AI output, and that educators teach judgement, trust calibration and
the components of supervisory work alongside traditional technical skills.

## Related Terms

- [[DefinedTerm/supervisory-engineering-work]]
- [[DefinedTerm/productivity-experience-paradox]]
- [[DefinedTerm/review-bottleneck]]
- [[DefinedTerm/verification-loop]]
