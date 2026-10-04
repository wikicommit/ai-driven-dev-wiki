---
title: "Verification Budget"
type: "schema:DefinedTerm"
lang: en
tags: [verification, software-factory, quality-gates]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/human-judgment-doesnt-leave-the-software/'
    hash: sha256:c4cc398bbcb3b786b12103edd73235c1799a0c14110e69dfb8a172809051a0b4
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A framing Addy Osmani uses for deciding, the way one sets a performance budget, which verification checks an agentic workflow runs and at what point — fast, deterministic checks early and continuously, heavier but valuable checks such as the full test suite, mutation, browser and security testing later, around the draft pull request."
---

A verification budget, as Addy Osmani describes it, is the deliberate allocation of verification
checks across the stages of an agentic development loop, thought about "in the same way as I've
historically thought about performance budgets." Some checks are fast enough to run early in the
software development lifecycle — linting and type checking are his examples — while others are heavy
but valuable enough to be worth running later: the full test suite, run closer to or after the point
a draft pull request is put together, which can include mutation testing, browser testing and
security checks. The point of the budget is to keep real checks in the loop without letting them slow the
development loop down.

## Usage

Osmani uses the term in [[BlogPosting/human-judgment-doesnt-leave-the-software-factory]], in
the context of a [[DefinedTerm/software-factory]], where he says verification is where a responsible
factory spends a lot of its time. He observes that tasks can take two to four times as long once
verification, retries, browser checks and human review are included, and reports that in his own
sample factory the verifiers caught real problems, while part of the time went to producing evidence
he wanted and part was factory overhead. The budget is his answer to that tension: separating useful delay from overhead, and asking
of any repeated check whether it is irrelevant, noisy, or actually making the system safer.

## When It Applies

It applies where agent work is gated by automated checks whose cost in time competes with a fast
iteration loop — most clearly in a software factory running many agent tasks in parallel. It assumes there are
real checks to allocate; Osmani is explicit that the budget is not a reason to replace tests with
summaries. The failure he warns against is treating the number of checks as a measure of quality: a
factory running many checks that nobody finds valuable is not thereby a high-quality one, and the
goal he states is the best signal-to-noise ratio rather than a large checklist, with constraints
tightened or relaxed deliberately as risk changes.

How well established it is: this is one practitioner's framing, offered from his own experience and
a sample factory he built, not a measured result or a widely adopted convention.

## Related Terms

[[DefinedTerm/backpressure]], [[DefinedTerm/shift-left]], [[DefinedTerm/deterministic-quality-gate]],
[[DefinedTerm/signal-to-noise-ratio]], [[DefinedTerm/software-factory]]
