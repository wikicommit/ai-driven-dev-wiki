---
title: "Vibe coding and agentic engineering are getting closer than I'd like"
type: "schema:BlogPosting"
lang: en
tags: [vibe-coding, agentic-engineering, code-review]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/May/6/vibe-coding-and-agentic-engineering/'
    hash: sha256:ad2e62c904d9fb829eaaef58183d658acec08216dd6d714f3267f5ddf6f29b9e
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Podcast highlights in which the author reports the line he drew between vibe coding and agentic engineering blurring in his own work: as agents grow reliable he has stopped reviewing every line, even in production, and frames that through depending on another team's service."
  author: ["Simon Willison"]
  datePublished: "2026-05-06"
---

The post collects highlights from a podcast appearance, and its central admission is about the
author's own practice rather than about tooling. He had staked out a clear line between
[[DefinedTerm/vibe-coding]] — not looking at the code at all — and
[[DefinedTerm/agentic-engineering]], where you are a professional software engineer who understands
security, maintainability, operations and performance and is using these tools to the highest of your
own ability. He reports that line blurring: as coding agents have
become more reliable he has stopped reviewing every line they write, including for production work,
and describes the resulting feeling as guilt.

His resolution is an analogy rather than a defence. He compares trusting an agent to depending on
another team's service inside a large organisation — you read the documentation, use the thing, and
only dig into its repository when it appears to misbehave. He is explicit about where the analogy
breaks: a team can build a professional reputation and be accountable, and a coding agent can do
neither, even while repeatedly producing straightforward work correctly. He names the risk in this
as an element of the normalization of deviance.

Two further threads run through the highlights. One is that the surface signals by which a developer
used to judge whether a project had care put into it — commit count, a good readme, comprehensive
tests — can now be produced in half an hour, leaving "has someone actually used this" as the
signal he now values most, at both personal-project and enterprise scale. The other is that raising
code output breaks the software lifecycle at both ends: downstream stages designed around code being
slow to produce, and upstream design processes whose caution was priced against the cost of building
the wrong thing for three months.

## Key Points
- The author reports that the distinction he drew between vibe coding and agentic engineering has
  started to blur in his own work, and describes this as upsetting.
- His original delineation is restated: vibe coding is not looking at the code at all, possibly
  without knowing how to program, and judging the result only by whether it works.
- He maintains that vibe coding is fantastic provided you know when it can be used — a personal tool
  where a bug hurts only you — and grossly irresponsible when building software for other people.
- Agentic engineering is described as a professional engineer using these tools to the highest of
  their ability, still leaning on their own experience, with the goal of higher-quality production
  systems rather than lower-quality ones faster.
- He reports that he no longer reviews every line of code the agents write, even for production-level
  work, because the agents have become reliable enough on routine tasks.
- His stated reconciliation is the analogy of depending on another team's service: read the
  documentation, use it, and investigate the implementation only when problems appear.
- He names the limit of that analogy himself: a human team carries accountability and professional
  reputation, and a coding agent carries neither.
- He identifies an element of the normalization of deviance in this — each time unmonitored code turns
  out correct raises the risk of misplaced trust later.
- A repository with a hundred commits, a good readme and thorough tests no longer signals care,
  because the author reports he can now produce one in half an hour.
- He states he cannot tell the difference even for his own projects, which is why he now values
  evidence that someone has actually *used* a thing over the quality of its tests and documentation.
- The enterprise form of the same preference is stated as wanting a CRM that other large organisations
  have run successfully for six months before taking a risk on it.
- Going from 200 to 2,000 lines of code a day breaks the rest of the lifecycle, which he argues was
  designed around code being slow to produce.
- The same applies upstream: extensive design processes were built around getting the design right
  because handing the wrong thing to engineers used to cost three months of building, so when
  building is cheap the design process can afford to be riskier.
- He reports not fearing for his career, on the grounds that these tools amplify existing experience
  and that producing software remains ferociously difficult regardless of tooling.
- He quotes a commentator preferring that professionally managed software companies use AI assistance
  to sell better products rather than that he vibe code himself, and endorses the sentiment with the
  analogy of preferring to hire a plumber.

## Context
The material is drawn from a podcast conversation, so it is thinking-out-loud rather than a worked
argument, and the post presents it that way — the author says the format pushed him to articulate
something he had not previously put into words. The evidence throughout is his own practice and his
own reactions, not measurement. It also marks a shift within his own writing: his earlier position
fixed vibe coding as a narrow, unreviewed practice clearly separate from responsible use, and this
post reports the boundary eroding from the responsible side rather than the term drifting.
