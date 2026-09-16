---
title: "Trajectory Evaluation"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/new-sdlc-vibe-coding/'
    hash: sha256:2b7eef861936103711a0ad32f7cb0b06602f71701457350ca6e1e37687c85c0e
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "Judging whether the path an AI agent took to reach a result — its tool calls and reasoning — was sound, as distinct from output evaluation, which judges only whether the final result is correct."
---

Trajectory evaluation is one of two mechanisms a cited Google whitepaper uses to verify agent work that isn't fully covered by deterministic tests: it asks whether the path an agent took to reach its result, meaning its tool calls and reasoning, was sound. This is distinguished from output evaluation, which asks only whether the final result itself is correct.

## Usage

The distinction is presented as a reason to want both mechanisms together: an answer that looks right but skipped its checks is described as more dangerous than one that is obviously broken, because output evaluation alone would pass it. The source frames setting evaluation bars at this level, rather than at a one-off demo, as the difference between showing an agent can work once and showing it works reliably.

## Related Terms

[[BlogPosting/new-sdlc-vibe-coding]], [[DefinedTerm/llm-as-a-judge]]
