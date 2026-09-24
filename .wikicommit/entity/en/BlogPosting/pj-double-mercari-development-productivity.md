---
title: "pj-double: メルカリの開発生産性向上に向けた挑戦 — AI-Native化が辿り着いたASDDとプロセス変革の全貌"
type: "schema:BlogPosting"
lang: en
tags: [ai-adoption, spec-driven, agentic-coding, software-process]
sources:
  - type: url
    url: 'https://engineering.mercari.com/blog/entry/20251201-pj-double-towards-ai-native-development/'
    hash: sha256:759a8657a3547ccd879fd3b7b260a4e7eda5e4cbc7fbb559a4b86aabecb602c4
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Mercari engineering-blog account of pj-double, a project launched in July 2025 to double product-development productivity by redesigning processes to be AI-Native, which arrived at Agent-Spec Driven Development (ASDD) and then found its limits in the upstream work of reaching agreement on what to build."
  author: ["nnaakkaaii"]
  datePublished: "2025-12-02"
  publisher: "[[Organization/mercari]]"
---

This post, written by a manager in Merpay's VPoE office as part of the Merpay & Mercoin Advent Calendar 2025, tells the story of Project Double (pj-double) at [[Organization/mercari]]. The project's stated mission is to double productivity in product development by redesigning development structures and processes to be AI-Native. The post presents it as a response to a problem with the first wave of AI-assisted coding inside the company: individual developers achieved large gains, but the methods stayed personal and did not add up to an organizational improvement.

The account runs chronologically — from the bottom-up experimentation of early 2025, through a three-month study of how AI was actually being used across projects, to the proposal of [[DefinedTerm/agent-spec-driven-development]] (ASDD) as a standard in September 2025 and the expansion of the effort to the whole company from October. Its second half is reflective: four lessons from the project, and an analysis of where ASDD fell short.

## Key Points

- The post attributes the failure of early efforts to share AI practice to a structural property of [[DefinedTerm/vibe-coding]], which it describes as sending the AI instructions step by step and correcting course while watching its output. Because that process is synchronous and interactive, productivity hinges on each developer's situational judgement, which stays inside their chat logs and is hard to explain afterwards — so it was neither transparent nor reusable.
- pj-double was launched around July 2025 in Merpay's VP of Engineering Office, framed as a move from a "Divergence" phase of individual experimentation to a "Convergence" phase of establishing a company-wide, reproducible development standard.
- Over its first three months the project worked with more than 30 backend projects at Merpay and Mercari Mobile, tracking weekly which AI methods were used in which phases. Productivity was measured by comparing each project's conventional effort estimate at the start with its actual effort, statistics the post describes as subjective and gathered phase by phase to reduce noise.
- By that measure, [[DefinedTerm/spec-driven-development]] was the most effective method: projects that adopted it averaged more than a 150% improvement in development speed relative to their estimates, and more than 80% relative to projects using other AI-assisted methods.
- Qualitatively, the developers who got the most from AI differed from the rest in three respects, according to the post: they gave the AI the relevant primary information up front; they stated the task's purpose, steps and completion criteria explicitly; and they kept the AI's working context lean — for example by splitting implementation across separate conversations or using [[SoftwareApplication/claude-code]]'s subagent feature — so that compaction did not make the AI lose track of its task.
- ASDD was proposed in September 2025 to institutionalise those three practices, as a two-step method in which agents first generate an implementation plan (the Agent Spec) and then implement it.
- On quality and maintainability, the post reports that AI use has not proved to be a trade-off: QA automation and other guardrails build functional checks into the process, and the team monitors revert rate and MTTR with the DX developer-experience tool, which it says has shown no signal of degraded quality. It attributes readability and extensibility problems in AI-written code mostly to missing context rather than to the model.
- On the [[DefinedTerm/review-bottleneck]], the post concludes that review strain came from the size of pull requests — the AI's speed packed huge diffs into one PR — rather than from the code being AI-written. Splitting work at Agent Spec generation into the smallest reasonable working units, with one PR per task, removed that strain, and the post's current conclusion is that AI-written and human-written code show no significant difference in review effort.
- In QA, the team first built a tool with a rich UI to automate the workflow, which the post calls a classic "build trap": the app made the prompts and methods harder to improve, because any change needed application code changes too. Its lesson is to start from a minimal setup focused on refining the method, and to enlist teams on changing the process rather than asking for feedback on a tool.
- The post argues for backcasting — working back from a future in which agents gather context, implement to coding rules and run QA on their own — as the way out of what it calls the dilemma between standardising and becoming obsolete, since tools built around today's limits go stale within months.

## Context

The post is candid about ASDD's limits. Developers reported that the Agent Spec assumes a specification and design that are already agreed, when reaching agreement was what took longest; that auto-generated documents carry no rationale and so cannot serve as a medium for agreement; and that reviewing a long Agent Spec regenerated from scratch each time costs more than writing it by hand, especially when primary information is mixed with generated content of unknown provenance. The team's own diagnosis is that it designed work that should be done by thinking and deciding together with AI as work delegated to AI.

From this it distinguishes synchronous collaboration — "thinking with AI" and "deciding with AI" — from asynchronous collaboration, "leaving it to AI", and argues that upstream work such as requirements and design needs the synchronous kind, because its value lies in the comparison, decision and agreement it records rather than in the documents it produces. The post presents this as the project's current direction, still being explored and validated, rather than as a result.

All figures in the post are the company's own internal measurements, and the productivity figures in particular rest on subjective comparisons of estimated and actual effort.
