---
title: "Cognitive Debt"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/own-the-outer-loop/'
    hash: sha256:4945c6720401f08dd3c43a7ec8fd0b79a1c8eb6f08bfa4b0da49f6e4a0c6173a
  - type: url
    url: 'https://addyosmani.com/blog/cognitive-parallel-agents/'
    hash: sha256:11c6c2853c941f4bfa797fda14ef4263bd09268a5d9a6e9cd9457478cf75cc83
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "As framed in Addy Osmani's 'Own the Outer Loop' keynote, the erosion of an engineer's own understanding of a codebase that accumulates when they delegate the thinking behind it to a coding agent instead of reasoning through the problem themselves, worsening as the agent is given a longer planning horizon — described in similar terms, and referred to as 'comprehension debt,' in a separate post about running AI coding agents in parallel, where it also compounds across multiple parallel threads at once."
---

In his "Own the Outer Loop" keynote, Addy Osmani frames cognitive debt as the erosion of an engineer's own understanding and memory of how to solve a problem, which accumulates when the thinking behind a change is offloaded to a coding agent rather than worked through by the engineer. The output an agent produces on a large codebase can be work the delegating engineer would not have been able to produce themselves, on a timescale that leaves no room to climb the learning curve behind it — so the gap between what exists and what the engineer actually understands compounds, and grows faster the longer the agent's planning horizon runs.

## Usage

The source cites a randomized controlled trial from Anthropic comparing engineers who relied on AI to write code against engineers who wrote it themselves, testing both groups afterward with a comprehension quiz: the engineers who worked through AI scored seventeen percentage points lower, 50 percent versus 67 percent. It is presented as one of three hidden costs of agentic delegation, alongside cognitive surrender and the orchestration tax.

A separate post about running multiple AI coding agents in parallel applies the same dynamic to parallel sessions, referring to it there as "comprehension debt": letting agents generate faster than a person can understand accumulates debt that is bounded within a single session but compounds across threads when several agents run at once, since a person cannot always tell which thread is running up the largest tab. That post frames the ceiling on how many agents someone can usefully supervise as a ceiling on throughput of understanding rather than throughput of supervision, and treats that distinction as the reason adding agents does not scale a person's output linearly.

## Related Terms

[[DefinedTerm/outer-loop]], [[DefinedTerm/cognitive-surrender]], [[DefinedTerm/orchestration-tax]], [[DefinedTerm/parallel-agent-limit]]
