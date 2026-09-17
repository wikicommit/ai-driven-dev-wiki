---
title: "Your parallel Agent limit"
type: "schema:BlogPosting"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/cognitive-parallel-agents/'
    hash: sha256:11c6c2853c941f4bfa797fda14ef4263bd09268a5d9a6e9cd9457478cf75cc83
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "Addy Osmani's argument that running multiple AI coding agents in parallel imposes a distinct, non-linearly-scaling cognitive cost on the human overseer — context switching, continuous judgment calls, and trust-calibration overhead — and that each person has a personal, situational 'ceiling' for how many agents they can supervise well, best found by deliberate calibration rather than by pushing until something breaks."
  author: "Addy Osmani"
  datePublished: "2026-04-07"
---

This post argues that the conversation about running AI coding agents in parallel has focused on throughput while ignoring what it costs the person supervising them. Running several agents at once is not several instances of the same task: it means holding several distinct mental models, problem framings, and trust calibrations at the same time, and absorbing the ongoing uncertainty of not knowing what any one agent might quietly be getting wrong — a kind of cognitive labor the post says has no settled vocabulary yet.

It builds on the author's own separate writing on the organizational side of running agents in parallel, treating that as addressing the overhead of managing sessions like an async team, while this post is about the overhead that stays entirely inside the person doing the supervising.

## Key Points

- Running four agents in parallel is qualitatively different from running one: it means managing four distinct mental models, codebases, problem framings, and trust calibrations at once, not four instances of the same task.
- Names the background vigilance of not knowing whether an unwatched agent thread is quietly going wrong the "ambient anxiety tax" ([[DefinedTerm/ambient-anxiety-tax]]) — distinct from the active work of steering and reviewing, but drawing on the same finite mental reservoir.
- Argues that cognitive bandwidth does not parallelize: the agent does the generating, but evaluating, deciding, trusting, and integrating stay single-threaded on the human's side, so a person's throughput of supervision can exceed their throughput of understanding — which is where comprehension debt ([[DefinedTerm/cognitive-debt]]) accumulates.
- Cites the conductor metaphor from [[BlogPosting/code-agent-orchestra]] to explain why the role is tiring even without touching every instrument: holding the whole piece requires whole-system awareness, which cannot be extended by trying harder.
- Describes the author's own changed practice: defining a session's duration and scoping each thread to something resolvable and reviewable within that window before spawning any agent, and settling on roughly three to four parallel threads as a typical, sustainable ceiling rather than pushing for higher throughput.
- Offers a calibration heuristic for finding this personal ceiling ([[DefinedTerm/parallel-agent-limit]]) deliberately: start one thread below what feels comfortable, watch review-quality confidence rather than agent count, treat rising anxiety across more than one thread as an early capacity signal, and prefer reducing a thread's scope before reducing how many threads run.

## Context

The post frames itself as the personal-overhead counterpart to the author's earlier writing on the management model for orchestrating agents ([[BlogPosting/your-ai-coding-agents-need-a-manager]]), which it says addresses mostly organizational overhead, and it links back to the author's own posts on [[DefinedTerm/agentic-engineering]] and on comprehension debt for related ideas. It is presented throughout as a first-person account of the author's own practice and experience rather than as a controlled study.
