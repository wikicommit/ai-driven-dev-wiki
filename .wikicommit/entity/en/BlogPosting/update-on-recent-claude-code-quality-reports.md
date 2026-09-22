---
title: "An update on recent Claude Code quality reports"
type: "schema:BlogPosting"
lang: en
tags: [claude-code, anthropic, coding-tools, evaluation]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/april-23-postmortem'
    hash: sha256:269dd6e147333715b02167db5eedbc394fe254ceebed15d9cf7f2a05a25c87f5
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Anthropic's postmortem tracing a month of user reports that Claude Code had got worse to three unrelated changes — a lowered default reasoning effort, a caching optimization that kept discarding prior reasoning, and a system prompt instruction limiting verbosity — and setting out the process changes it is making in response."
  author: "Anthropic"
  datePublished: "2026-04-23"
  publisher: "[[Organization/anthropic]]"
---

This post is Anthropic's account of why users had been reporting for about a month that Claude's
responses had got worse, and of what it found. Its central claim is that there was no single
regression: three separate changes landed on different slices of traffic on different schedules,
and because their effects overlapped, the aggregate looked like broad and inconsistent degradation.
All three are stated as resolved as of April 20 in version 2.1.116.

The post is explicit about scope and about intent. The changes affected
[[SoftwareApplication/claude-code]], the Claude Agent SDK and Claude Cowork; the API is stated as
not impacted, and Anthropic says it confirmed immediately that its API and inference layer were
unaffected and that it never intentionally degrades its models. The final section describes
tightened controls on how system prompts change, and the post closes by crediting both the users who
reported issues through the `/feedback` command and those who posted specific, reproducible
examples online, and by announcing a reset of usage limits for all subscribers as of April 23.

## Key Points

- The post presents three separate causes rather than one, and attributes the appearance of a
  single broad regression to their overlapping on different traffic slices and schedules.
- On March 4 the default [[DefinedTerm/reasoning-effort]] in Claude Code was lowered from `high` to
  `medium`, to address very long latencies that could make the UI appear frozen. Anthropic calls
  this the wrong tradeoff and reverted it on April 7 after users said they would rather default to
  higher intelligence and opt down for simple tasks.
- Design iterations meant to make the current effort setting clearer — startup notices, an inline
  effort selector, and bringing back ultrathink — did not move most users off the medium default.
  Anthropic states that it reversed the decision on April 7 after hearing feedback from more
  customers.
- On March 26 an optimization meant to clear old reasoning once from sessions idle for over an hour
  instead cleared it on every turn for the rest of the session, so the agent kept acting without
  memory of why it had chosen what it was doing. The post reports this surfaced as forgetfulness,
  repetition and odd tool choices, and that it was fixed on April 10 in version 2.1.101.
- That same bug is given as the likely cause of separate reports that usage limits were draining
  faster than expected, because continually dropping reasoning blocks also caused cache misses.
- The post states the bug passed multiple human and automated code reviews, unit and end-to-end
  tests, automated verification and dogfooding, and that it took over a week to confirm the root
  cause. Two unrelated changes are given as having made it hard to reproduce at first: an
  internal-only server-side experiment on message queuing, and an orthogonal change in how thinking
  is displayed, which the post says suppressed the bug in most CLI sessions.
- Anthropic reports back-testing its own Code Review tool against the offending pull requests:
  given the repositories needed for full context, Opus 4.7 found the bug where Opus 4.6 did not,
  and it is adding support for additional repositories as code-review context in response.
- On April 16 a system prompt instruction was shipped alongside Opus 4.7 to curb that model's
  verbosity: it held text between tool calls to 25 words and final responses to 100, the latter
  qualified as applying unless the task required more detail. It had passed weeks of internal
  testing with no regressions in the set of evaluations then being run; wider ablations run during the
  investigation showed a 3% drop on one evaluation for both Opus 4.6 and 4.7, and it was reverted
  on April 20.
- The stated process changes are: more internal staff running the exact public build rather than a
  feature-testing version; improvements to the internal Code Review tool, to be shipped to
  customers; a broad per-model evaluation suite run for every Claude Code system prompt change,
  with continued line-by-line ablations and new tooling to review and audit prompt changes; a
  CLAUDE.md addition gating model-specific changes to the model they target; and soak periods,
  broader evals and gradual rollouts for any change that could trade against intelligence.

## Context

The post is a vendor's account of its own product, and its evidence is internal — evaluation
results, ablations and its own reading of the code. Its most transferable observation is an
admission about the limits of evaluation rather than a claim about the product: the verbosity
instruction cleared weeks of internal testing on the evaluation set then in use, and the regression
only appeared once a broader set was run line by line, which is the reasoning behind committing to
per-line ablations for every future system prompt change.

The reasoning-effort episode reads as a product-defaults problem rather than a model one — the
capability was reachable throughout and the post's own account is that most users simply stayed on
whatever was default. The caching bug bears on [[DefinedTerm/token-caching]] from the other
direction than the usual cost argument: here dropped reasoning caused the cache misses rather than
the reverse, and the user-visible symptom was consumption rather than latency.
