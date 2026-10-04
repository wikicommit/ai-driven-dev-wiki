---
title: "Review auto-correction loop"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-code-review, code-review, verification]
sources:
  - type: url
    url: 'https://github.com/FlorianBruniaux/claude-code-ultimate-guide/blob/main/guide/workflows/iterative-refinement.md'
    hash: sha256:76f1517fd4fb3d45eeeac738cd655ba37364639f67c145dd11149406e32e52f4
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5"
generated_with: "0.9.0"

properties:
  description: "A bounded form of iterative refinement for code review in which an AI agent reviews a change, fixes the issues found, and re-reviews to verify the fixes, repeating within a fixed iteration budget and accepting the result only on evidence rather than on the loop stopping."
---

A review auto-correction loop is a pattern in which an AI agent reviews a change, applies fixes for the issues it finds, re-reviews to check that the fixes worked and introduced nothing new, and repeats within a fixed budget. The Claude Code Ultimate Guide, which describes it as a specialized form of [[DefinedTerm/iterative-refinement]], stresses that acceptance requires evidence and that the loop stopping does not by itself establish success.

## Usage

The guide's prompt template has the agent run a multi-agent review with three scope-focused reviewers, fix every must-fix issue, re-review, fix the should-fix issues, and re-review once more, with a maximum of three iterations. Each iteration can re-run the same reviewers with distinct scopes — its example names a consistency auditor, a SOLID-principles analyst and a defensive-code auditor — and the guide notes that adding agents does not by itself establish independence or quality.

It separates acceptance from the reason a loop stopped. A result is **accepted** only when the required checks pass on the recorded revision, blocking findings have verified dispositions, and the designated reviewer accepts against the current criteria — which, the guide adds, still does not prove the criteria are complete. A loop that used up its budget is **exhausted**, and one in which two passes resolved no blocking finding and produced no new verification evidence stops for **no progress**; in both cases the unresolved findings and checkpoints are kept and completion is not reported. Failed, timed-out, aborted and unknown outcomes are each recorded as distinct from acceptance, and a small diff is explicitly not acceptance. If review uncovers an incomplete requirement, the criteria are versioned with the reason and the authorized decision and the affected verification re-run, rather than a criterion being silently weakened to reach a passing state.

Its safeguards are a hard iteration limit, quality gates that run type checks, lint and relevant behaviour tests after each fix and record the revision and results, a skip list of protected files such as `package.json`, migrations and `.env` that are never auto-fixed, a progress check on resolved blocking findings, and a checkpoint taken before fixes — with the caveat that rolling back code does not undo mutated data or other external effects.

## When It Applies

The guide recommends the bounded loop for changes that need several correction passes, and a single review pass for simple pull requests, experienced teams or time-sensitive work; changes to sensitive paths still go through their owner and sign-off policy. Against a one-pass review, it credits the loop with each iteration knowing what the previous one found and with re-review catching fixes suggested for code that is already fixed, at the cost of three or more reviews, and it notes that either approach can miss defects and that more passes alone do not prove improvement. The failure modes it lists are an infinite loop with no bounded stop, scope creep as requirements silently change between iterations, fixes that introduce new bugs, changes to protected files, and losing track of the original issues after a few iterations, which it counters with an issue tracker kept across iterations (see also [[DefinedTerm/review-loop-non-convergence]]). The pattern is set out in a practitioner guide, and the example session it gives is marked as illustrative rather than a measured result.

## Related Terms

- [[DefinedTerm/iterative-refinement]]
- [[DefinedTerm/review-loop-non-convergence]]
- [[DefinedTerm/agentic-code-review]]
- [[DefinedTerm/deterministic-quality-gate]]
