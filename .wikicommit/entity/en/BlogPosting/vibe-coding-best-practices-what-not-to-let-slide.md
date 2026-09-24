---
title: "Boas práticas de vibe coding: o que não dá pra deixar passar"
type: "schema:BlogPosting"
lang: en
tags: [vibe-coding, code-review, testing, software-quality]
sources:
  - type: url
    url: 'https://blog.douglasmedeiros.dev/artigos/ia/boas-praticas-de-vibe-coding'
    hash: sha256:1879a34aa5b34154a6c6d052e67a713a2bef8fbccecbbeb327adbd2959666f34
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Portuguese-language practitioner essay arguing that AI coding agents have moved the development bottleneck from writing code to validating it, casting the developer as an architect-reviewer and setting out the guardrails — planning, model choice, strict automated tests, mutation testing, static analysis, observability and risk-focused review — that the author treats as the minimum for vibe coding done well."
  author: ["Douglas Medeiros"]
  datePublished: "2026-04-30"
---

This post ("Good vibe-coding practices: what you can't let slide") is a software engineer's continuation
of an earlier reflection on using AI in day-to-day development. Its central argument is that removing
typing as the bottleneck did not make the system flow on its own but moved the bottleneck: when an agent
can deliver hundreds of lines with passing tests in minutes, the constraint becomes validating what it
produced, and no human can review that volume line by line.

From there the author argues that the developer's role has shifted back toward the "ivory tower
architect" — the architect who writes the specification and hands it to implementers — with the
difference that the developer still validates the implementation, making them architect and reviewer at
once. Because the agent does not know when to stop, the judgement of whether something is good enough for
production is described as wholly the human's. The post treats [[DefinedTerm/vibe-coding]], stripped of
its pejorative sense, as essentially this cycle: specifying, mapping trade-offs, handing execution to the
model and validating the result, with quality coming from whoever operates the agent rather than from
the agent itself.

The bulk of the post is a set of practices the author follows to make that workable, drawn from their own
experience rather than from measurement.

## Key Points

- The post argues that AI has moved the development bottleneck from implementation to validation, since
  review bandwidth has stayed the same while output has accelerated.
- It recommends replacing line-by-line reading with automated quality signals (cyclomatic complexity,
  method and class size, dependency counts, coupling) while holding that metrics are not proof: in the
  author's experience, performance bugs such as a hidden N+1 query still passed repeated automated review
  and needed a senior engineer's reading.
- It treats generated code as non-deterministic — the same specification run several times can yield
  different results — and concludes that determinism has to be enforced at the output through strict
  assertions, with strong tests catching drift between runs.
- It says production basics that vibe-coded projects often skip — observability, feature flags, alerts
  and an audit trail — become more important, not less, when an agent is changing code daily.
- It describes project instruction files such as `CLAUDE.md`, Copilot instructions and versioned skills as
  "the floor, not the ceiling": they make the agent follow the project's conventions but do not guarantee
  its output is correct.
- It argues against the practice of planning with a large model and executing with a cheaper one for
  code, recommending paying for the better model for code, planning and architecture, while cheaper models
  remain fine elsewhere.
- It treats the plan as a first-class artifact: the author has the agent propose a plan in Markdown,
  reviews and adjusts it before execution, and applies spec-driven workflows selectively rather than "by
  the book", on the reasoning that a wrong plan is only text while wrong code is already a commit.
- It calls for tighter automated guardrails — coverage above 90% combined with a mutation score above
  90%, stricter static-analysis limits on function and class size, and strong regression tests — noting
  that AI-written tests can look like tests while testing nothing, and that agents often edit files they
  were not asked to touch.
- It argues that manual QA does not scale to AI output volume and that critical flows (money,
  authentication, account creation, data deletion) need automated end-to-end tests, keeping manual QA for
  exploratory testing of new features.
- It recommends reviewing by decision rather than by line: focusing human review on boundaries, contracts,
  authentication, persistence, external calls and unrequested changes, and trusting automated guardrails
  for the rest.
- It warns that an LLM has no stopping criterion and will always find something to improve, so plans and
  code can be over-engineered indefinitely; the human has to decide when scope and acceptance criteria are
  sufficient.
- It lists three bug patterns the author sees AI generate repeatedly — N+1 queries, race conditions in
  asynchronous sequences and memory leaks in caches without expiry — and suggests automated checks for
  each: query-count assertions, property-based and concurrent tests, and load tests with heap profiling.

## Context

The post is one practitioner's account, written from the author's own daily use, and most of its
recommendations rest on that experience rather than on data. It describes its practices as selective
adaptation rather than strict method, comparing strict spec-driven development to Scrum in that teams take
what works and ignore the rest. It also raises an operational-continuity concern: because the AI tool is a
paid, rate-limited third-party service, developers still need to be able to read, debug and write code by
hand when it is unavailable. Its diagnosis of validation as the new constraint is the same pressure
described more formally under [[DefinedTerm/review-bottleneck]].
