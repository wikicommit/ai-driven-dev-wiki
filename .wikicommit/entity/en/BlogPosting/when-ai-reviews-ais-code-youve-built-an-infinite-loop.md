---
title: "\"When AI reviews AI's code, you've built an infinite loop. Here's how we stopped it.\""
type: "schema:BlogPosting"
lang: en
tags: [agentic-code-review, agent-failure-modes, agentic-pull-request]
sources:
  - type: url
    url: 'https://dev.to/zoetaka38/when-ai-reviews-ais-code-youve-built-an-infinite-loop-heres-how-we-stopped-it-4g1n'
    hash: sha256:e728a1e5ac20dcc643c605006d08b8675b906bc6c4143d31cd941d98c8d1418e
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A post by the builder of the AI code review product Orange Codens on how a pipeline in which AI both reviews code and fixes it can loop forever, and the architectural cuts — merge-gated handoff, bot-PR exclusion, verify-run exclusion, idempotent dispatch and later fixes for two non-convergence incidents — used to guarantee termination and bound cost."
  author: ["Takayuki Kawazoe"]
  publisher: "DEV Community"
---

The post starts from a design problem its author says dominated building [[SoftwareApplication/orange-codens]]:
when the reviewer is AI and the fixer is AI, a loop forms easily. Orange reviews a pull request, hands
a finding to another agent that opens a fix PR, that fix PR is reviewed in turn, produces new findings,
and so on. Where a human reviewer stops at "good enough", the post argues, an AI reviewer does not, and
every round costs LLM tokens — so termination and bounded cost have to be guaranteed by the architecture,
not by how capable the model is.

The post then walks through the mechanisms built into the product, with excerpts of its code, and two
incidents in which the pipeline, built to that design, still failed to converge — the first of them
observed in an end-to-end run. It
closes by listing the resulting cuts and noting that the product includes all of them; it is written by
the product's builder about their own product.

## Key Points

- There is no single place to cut the loop: when to hand off, whose PRs are eligible, whether a finding
  can be dispatched twice, and when the review itself converges each need their own mechanism.
- Handoff of a fix task fires only when a PR is merged, not when a finding is created; before merge the
  reviewer only posts suggestions, and a PR closed without merging discards its queued handoffs, so an
  unmerged PR has no downstream cost.
- PRs authored by the fixing bots are still reviewed but never trigger an automatic handoff, which the
  author calls the direct break in the loop; findings from reviews of the fixing agent's own verify runs
  are likewise excluded.
- A finding that has been handed off once is never dispatched again, preventing two fix tasks for the
  same problem.
- A finding a human explicitly queued is dispatched even on a bot PR and even with automatic handoff off:
  explicit human intent overrides the loop guard.
- Incident, in an end-to-end run: dispatching one fix task per finding let three findings in the same file deadlock, because
  each fix PR was blocked by the reviewer's carry-over findings on the others. The fix was to coalesce
  findings for the same file and the same target agent into one task.
- Incident: reviews of bot fix PRs kept raising new high-severity findings on the newly written code,
  producing four consecutive request-changes rounds and escalation at the iteration cap. The fix was to
  block bot fix PRs only on unresolved high-severity carry-over findings or new blockers, recording other
  new findings but approving the PR; review of human PRs was left unchanged.
- The general lesson drawn is that "a perfectionist reviewer never converges", so the review bar must be
  designed so the review can stop — presented as the author's conclusion from operating this product,
  not as a measured result.

## Context

The post is a first-person engineering account from a product's builder, and ends by pointing to the
product. Its argument that termination must come from the architecture is one answer to the problem
described on [[DefinedTerm/review-loop-non-convergence]]; other writing on AI reviewing AI-authored
changes is gathered under [[DefinedTerm/closed-loop-ai-review]] and [[DefinedTerm/agentic-code-review]].
