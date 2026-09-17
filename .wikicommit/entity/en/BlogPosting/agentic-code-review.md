---
title: "Agentic Code Review"
type: "schema:BlogPosting"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agentic-code-review/'
    hash: sha256:6012ead92bbbe014c0f7e64ead32c2683f98af21d3fe5b5fa060025c3f58a8e7
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A June 2026 blog post arguing that as coding agents make generating code nearly free, code review has become software engineering's most leveraged bottleneck, and that how much of it a team needs depends on a change's blast radius rather than a one-size-fits-all process."
  author: "Addy Osmani"
  datePublished: "2026-06-15"
---

This post argues that coding agents have shifted the hard part of software engineering from writing code to deciding whether to trust it, making code review the most leveraged skill in software right now. It surveys 2026 industry data showing that while AI adoption sharply raises developer output, it also raises code churn, defect rates, review duration, and the share of PRs merged without any review — and argues the right amount of review effort depends on a change's "blast radius" (what breaks if it's wrong, how long the code lives, and how many people need to understand it) rather than a single standard applied to everyone.

The post also argues that review's core problem changed: when a human writes code, their reasoning is available for a reviewer to check, but an agent's reasoning is usually discarded once a diff is produced, so a reviewer has to reconstruct intent that was never written down. It recommends capturing an agent's stated reasoning as a decision log to make review faster, and closes by arguing that as AI review tools take on more of the reviewing work, a human should shift from reading every diff to owning accountability, judging whether a change is the right one to build, and gating only the highest-risk changes.

## Key Points

- Faros AI's March 2026 telemetry across 22,000 developers and 4,000 teams found that moving from low to high AI adoption raised code churn by 861%, the incidents-to-PR ratio by 242.7%, the per-developer defect rate from 9% to 54%, median review duration by 441.5%, and PRs merged with zero review by 31.3% — with teams that had mature, disciplined engineering practices affected just as much as others.
- CodeRabbit's December 2025 study of 470 open-source PRs (320 AI-coauthored, 150 human-only) found AI-authored changes carried roughly 1.7x more issues than human-only changes, with logic/correctness problems up about 75%, security issues 1.5 to 2x more common, and readability problems more than tripling.
- GitClear's productivity data through 2025 found daily AI users produce around 4x the raw code output of non-users, but the real productivity gain measured against their own prior-year output is only about 12%.
- GitHub reports that Copilot code review has now run over 60 million reviews, a 10x increase in under a year, with more than one in five reviews on the platform involving an agent.
- An independent test running four AI code reviewers (CodeRabbit, Sentry Seer, Greptile, Cursor BugBot) in parallel across 146 real PRs and 679 findings found that of 617 distinct flagged locations, 93.4% were caught by exactly one of the four tools and none were caught by all four — presented as an argument for running multiple, differently-built reviewers rather than picking one "best" tool.
- Anthropic's internal code review tool is reported to have under 1% of its findings marked incorrect by Anthropic's own engineers, and to have raised the share of PRs receiving a substantive review from 16% to 54%.
- The post recommends tiering review effort by a change's blast radius rather than by author, using a "circuit breaker" model to fast-fail PRs predicted to need heavy maintenance before a human looks, requiring evidence (a stated rationale, test output, proof tests were run) before review, keeping agent-authored PRs small since they run larger on average, reading test-file edits especially carefully since an agent may rewrite a failing assertion rather than fix the underlying behavior, and treating CI as a strict gate that cannot be argued out of its verdict.
- It frames the shift as "human in the loop" becoming "human on the loop": rather than reading every diff, a human keeps accountability, judges whether a change is the right one to build, gates the highest-blast-radius changes, and samples and audits the system rather than reviewing everything.
- It profiles an ex-Meta engineer, Kun Chen, who ships around 40 PRs a day largely without per-line review by writing detailed plans upfront and relying on an automated pre-merge gate, while noting this approach fits his specific circumstances (a solo builder with no large team or legacy system) rather than being generally prescribed.

## Context

The post cites a 2026 study analyzing 1,154 posts across 15 Reddit and Hacker News threads about "AI slop" for the observation that reviewing an agent's PR can make a reviewer "the first human being to ever lay eyes on this code," and situates itself alongside the author's other posts on [[DefinedTerm/loop-engineering]], intent debt, and comprehension debt. It also warns that a closed loop of multiple AI reviewers with correlated blind spots can produce a confident-but-wrong verdict with no human left to catch it — a risk the author elsewhere frames as [[DefinedTerm/cognitive-surrender]].
