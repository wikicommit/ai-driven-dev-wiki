---
title: "Agentic Coding mit Spec-Driven Development: Warum Ihr KI-Agent Struktur braucht, bevor er Code schreibt"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, agentic-coding, test-driven-development, agent-skills]
sources:
  - type: url
    url: 'https://timrutte.de/blog/agentic-coding-spec-driven-development/'
    hash: sha256:6200dda512286daa495cc0bbd8aeaa4059d622b6773b8511017345066b95247a
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A German-language post arguing that AI coding agents need structure before they generate code, and describing how to combine the Superpowers Claude Code plugin with spec-driven development using separate feature, bugfix and chore spec templates."
  author: ["Tim Rutte"]
  datePublished: "2026-03-30"
---

Tim Rutte's post, dated 30 March 2026, argues that most developers optimize the wrong thing when
using AI coding tools: they chase faster generation with longer prompts and more context, when the
problem is not the model but the missing structure around it. His case is a failure mode he says
better prompts do not fix — code that works, passes tests and lint, and is merged, while over the
following weeks the architecture drifts through boundary violations no single commit made obvious.
His answer is not a better prompt but a better workflow.

The workflow he describes combines [[SoftwareApplication/superpowers]], an open-source
[[SoftwareApplication/claude-code]] plugin, with [[DefinedTerm/spec-driven-development]]. In the
post's description, Superpowers gives Claude a set of skills — structured Markdown files, loaded into
the context window when relevant, that Claude must use when one exists for the task at hand — and
enforces a Brainstorm → Plan → Implement sequence; spec-driven development is what, in the author's
view, keeps that sequence stable.

## Key Points

- Different kinds of work carry different risks, so the post keeps a separate spec template for
  each: a feature spec (problem, in scope, out of scope, architecture constraints, success criteria,
  open questions, milestones), a bugfix spec (problem, root cause, affected components, reproduction
  steps, fix approach, regression tests, verification) and a chore spec (motivation, scope, out of
  scope, approach, definition of done).
- The field it calls essential differs by type: the "Out of Scope" section for features, because an
  agent drifts into adjacent functionality unless told what is excluded; the root-cause hypothesis
  for bugfixes, because an agent without one changes things until the symptom disappears; and the
  definition of done for chores, so the agent knows when to stop.
- The spec directory's README documents the workflow and is referenced from
  [[DefinedTerm/claude-md]], so the agent knows the structure at the start of every session.
- Once a spec is complete, the agent creates a branch whose prefix comes from the spec type, the
  planning skill breaks the spec into two-to-five-minute tasks that are committed as a plan, and each
  implementation task gets its own commit; the review skill checks each task against that specific
  spec rather than against general best practice.
- The TDD skill enforces the red/green/refactor cycle as a hard constraint (see
  [[DefinedTerm/red-green-tdd]]): implementation code written before a failing test must be deleted,
  and the agent cannot declare a step green without presenting the test runner's actual output. Tests
  are written against the spec's acceptance criteria rather than the implementation.
- Architecture constraints belong in the spec rather than the prompt, the author argues, because a
  constraint given in a prompt has to be given again in the next session, whereas one documented in
  the spec is loaded with the workflow, respected by the plan and checked by the review.
- The post names the approach's limits: environment and infrastructure debugging falls outside it;
  a poor spec produces an implementation that is correct against the spec but wrong for what was
  needed; and custom architecture rules still have to be written down, in personal skills or in the
  specs' architecture-constraints sections.

## Context

This is the author's own recommended setup, presented from his experience in backend development
rather than as a measured comparison. The post states that Superpowers was developed by Jesse Vincent
and the team at Prime Radiant and has been available in the official Anthropic plugin marketplace
since January 2026. Its closing claim is that the discipline experienced developers apply by habit —
knowing boundaries, writing tests first, committing in coherent steps, reviewing against requirements
— becomes the agent's default behavior because the workflow requires it, not because it was prompted.
