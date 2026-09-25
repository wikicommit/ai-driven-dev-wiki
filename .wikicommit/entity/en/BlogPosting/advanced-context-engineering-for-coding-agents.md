---
title: "Advanced Context Engineering for Coding Agents"
type: "schema:BlogPosting"
lang: en
tags: [context-engineering, coding-agents, spec-driven-development]
sources:
  - type: url
    url: 'https://www.humanlayer.dev/blog/advanced-context-engineering'
    hash: sha256:b5755938c78f425250aee7de4d4a3136d208b1d531e6999969cd3e9af536d9a1
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A HumanLayer post arguing that today's coding agents can handle large brownfield codebases if the whole development workflow is designed around context management, which the author calls frequent intentional compaction."
  author: ["Dex"]
  datePublished: "2025-08-29"
  publisher: "HumanLayer"
---

This post starts from the view, which it calls pretty well-accepted, that AI coding tools struggle in
real production codebases: that much of the extra code they ship is rework, and that coding agents help
on new projects and small changes but can make developers less productive in large established
codebases. It reports hearing the same from founders ("too much slop", "tech debt factory"). The
author's counter-claim is that
you can get very far with today's models by embracing core context engineering principles, and that AI
for coding is a deeply technical engineering craft rather than something only for toys and prototypes.
The post is based on a talk the author gave at Y Combinator.

The family of techniques it describes is what the author calls [[DefinedTerm/frequent-intentional-compaction]]:
designing the entire development workflow around context management, keeping context utilization in
roughly the 40-60% range, and splitting work into research, plan and implement steps with human review
at the highest-leverage points. As evidence it reports the team's own results, including getting Claude
Code to work in BAML, a 300k-line Rust codebase the author had never touched, where a bug-fix PR was
approved by the maintainer the next morning, and a 7-hour session in which two people shipped 35k lines
adding cancellation and WASM support — work the post says was estimated at 3-5 days each for a senior
engineer.

## Key Points

- The post argues that at any given point a turn in an agent such as Claude Code is a stateless function
  call — context window in, next step out — so the contents of the context window are the only lever
  on output quality (short of training or tuning models). It says to optimize the window for
  correctness, completeness, size and trajectory, and ranks the worst things that can happen to it as
  incorrect information, then missing information, then too much noise.
- Using a coding agent like a chatbot is presented as the naive approach, and starting over with a new
  session plus a little more steering as a slightly smarter one; "intentional compaction" — pausing and
  writing progress to a file such as progress.md before starting a fresh context — goes a step further
  (see [[DefinedTerm/compaction]]).
- Subagents are described as being about context control rather than anthropomorphized roles: they let
  finding, searching and summarizing happen in a fresh context window so the parent agent is not
  clouded by the calls.
- The research, plan, implement workflow is the team's way of doing frequent intentional compaction:
  research to understand the relevant code, a plan stating the exact steps and verification, and
  phase-by-phase implementation.
- On human leverage, the post argues that a bad line of code is one bad line, a bad line of a plan can
  lead to hundreds of bad lines of code, and a bad line of research can lead to thousands, so human
  review of research and plans gives more leverage than review of the code alone.
- It says the most important part of the workflow for the team is mental alignment: with everyone
  shipping more code, more of the codebase is unfamiliar to any given engineer, and the team now keeps
  aligned through specs, plans and research rather than only pull requests.
- The team adopted something like Sean Grove's "spec-driven development" (see
  [[DefinedTerm/spec-driven-development]]); the author reports the transition took about 8 weeks and
  was uncomfortable, with specs becoming the source of truth while he still reads tests carefully.
- The post stresses that this is "not magic": the approach only works when the human stays deeply
  engaged, and it reports a failed attempt to remove Hadoop dependencies from parquet-java, attributed to
  research that did not go deep enough and to lacking a codebase expert.

## Context

All the reported results are the author's and his team's own, from their own projects and pairing
sessions, and the author notes the team of three averages about $12k per month on Opus. The post
credits two talks from AI Engineer 2025 with shaping its thinking, quotes Geoffrey Huntley's view that
the more of the context window you use the worse the outcomes, and mentions his "Ralph" technique of
running an agent in a loop with a simple prompt (see [[DefinedTerm/ralph-loop]]). It refers back to
HumanLayer's 12-factor agents for the premise that LLMs are stateless functions, and ends by announcing
HumanLayer's CodeLayer in private beta. Related pages include [[DefinedTerm/context-engineering]],
[[DefinedTerm/context-rot]] and [[BlogPosting/12-factor-agents]].
