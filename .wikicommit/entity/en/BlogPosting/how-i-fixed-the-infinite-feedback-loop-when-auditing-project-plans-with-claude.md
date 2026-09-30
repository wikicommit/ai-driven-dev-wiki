---
title: "How I Fixed the Infinite Feedback Loop When Auditing Project Plans with Claude"
type: "schema:BlogPosting"
lang: en
tags: [agentic-code-review, planning, claude-code]
sources:
  - type: url
    url: 'https://dev.to/quolu/how-i-fixed-the-infinite-feedback-loop-when-auditing-project-plans-with-claude-4gh'
    hash: sha256:4d822423c523e2709c1a8df03b98bad2af4a22e36ce6e3c9694e2e9de4c07ca3
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A developer's account of an automated plan audit-and-revise loop with Claude that would not converge, and of the fix that made it converge: once a plan is reasonably complete, audit it only for logical contradictions."
  author: ["Quo"]
  publisher: "DEV Community"
---

The post, published on DEV Community and originally on the author's own site, describes a workflow of
writing a plan, having it audited, and then implementing it. The author reports that the audit step had
stopped working well — attributing this, tentatively, to the model gaining a broader perspective since
Opus 4.7 — because the audit kept raising points irrelevant to the plan, and an automated loop of auditing
and revising often failed to converge.

The author's diagnosis is that a broad audit never runs out of things to criticize, so each revision is
met by a criticism from a different angle. The remedy reported is to narrow the audit, for a plan that has
already been through one or two ordinary audits, to logical contradictions only. The post frames this as
a simple idea that nonetheless took the author two months to notice, and its argument is the subject of
[[DefinedTerm/review-loop-non-convergence]].

## Key Points

- In the author's experience, an automated audit-and-revise loop over a plan behaved like
  "Whac-A-Mole" or a seesaw: fixing B from A's perspective drew "B is excessive, and A is thin", adding A
  drew "C is inconsistent", and fixing C alternately drew "redundant" and "insufficiently explained".
- Asking the AI to audit a reasonably complete plan "only for logical contradictions" made the loop
  converge after a few rounds; the author's explanation is that the number of contradictions is finite,
  while points of criticism under a wide scope spring up without end.
- Implementation started from a contradiction-free plan ran through to the end without stopping, with
  only occasional implementation errors needing a retry — reported from the author's own use.
- Prompt wording did not fix the problem: instructions such as "Don't give too many points" or "Be
  consistent with past feedback" did not work, which the author takes as evidence that the problem was
  the scope of the audit rather than how the prompt was written.
- The author looked for prior work and found related ideas — criteria drift in LLM-based evaluation, an
  observation of oscillation under iterative LLM feedback, and fixing the rubric before evaluating — but
  argues that none clearly states narrowing the evaluation axis to a single finite one; the author also
  allows that it may well be written somewhere in academic terms.

## Context

This is a single developer's firsthand account, with no measurement beyond the author's own sessions.
It belongs with other writing on AI reviewing or auditing AI output in a loop, where the practical
question is how such a loop is made to stop; see [[DefinedTerm/review-loop-non-convergence]] and
[[DefinedTerm/llm-as-a-judge]].
