---
title: "Orange Codens"
type: "schema:SoftwareApplication"
lang: en
tags: [agentic-code-review, code-review-agent]
sources:
  - type: url
    url: 'https://dev.to/zoetaka38/when-ai-reviews-ais-code-youve-built-an-infinite-loop-heres-how-we-stopped-it-4g1n'
    hash: sha256:e728a1e5ac20dcc643c605006d08b8675b906bc6c4143d31cd941d98c8d1418e
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "An AI code review product, part of the Codens suite, that reviews pull requests and hands its findings to other Codens agents to produce fix pull requests, with loop guards designed to make that review-and-fix cycle terminate."
  applicationCategory: "AI code review"
---

Orange Codens is an AI code review product in the Codens suite. Its distinguishing feature, as described
in [[BlogPosting/when-ai-reviews-ais-code-youve-built-an-infinite-loop]], is that it does not stop at
review comments: it hands the fix for a finding to another Codens agent — Purple or Red — which opens a
fix pull request, which Orange then reviews in turn. Because that arrangement puts AI on both sides of the
loop, the product's design centres on guaranteeing that the cycle terminates and that its cost is bounded.

## Capabilities

Orange reviews pull requests through GitHub webhooks on open, synchronize and reopen events. Before
a PR is merged it only posts GitHub suggestions; handoff of fix tasks is triggered on the PR's `closed`
event when it was merged, and queued handoffs are discarded if the PR is closed unmerged. Handoff policy
has modes — the post shows a full-automatic mode and a threshold mode that dispatches findings at or
above a configured severity and within configured categories — and a human can queue an individual
finding for fixing, which dispatches even where automatic handoff would not.

Several guards keep the review-and-fix cycle from looping. PRs authored by the Codens bots are reviewed
but never trigger automatic handoff; findings from reviews of the fixing agent's own verify runs are not
handed off; and a finding already handed off is never dispatched again. Findings in the same file bound
for the same target agent are coalesced into one fix task, after per-finding fix PRs were found to block
one another. For bot-authored fix PRs, the review blocks only on unresolved high-severity carry-over
findings or new blockers, recording other new findings while approving; human PRs receive comments only
and are never automatically blocked. The post also mentions a cap on review iterations, reached at five
rounds in one incident.

## Adoption & Ecosystem

The only account of the product here is its builder's own post, which ends by promoting it. It works
alongside the other Codens agents it hands fixes to, and is an instance of the configuration described on
[[DefinedTerm/closed-loop-ai-review]] — AI authoring and AI reviewing the same changes — with the
termination problem discussed on [[DefinedTerm/review-loop-non-convergence]].
