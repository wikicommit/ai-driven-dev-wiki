---
title: "Agent Skills"
type: "schema:BlogPosting"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agent-skills/'
    hash: sha256:b9423cb1290bb467c3a66aa51884a5717037c14bd668eeca8b09ca3fba6fa781
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "An explanation of the design choices behind the author's Agent Skills project: a library of workflow-based skills meant to make AI coding agents perform the senior-engineering steps (specs, tests, review, scope discipline) they otherwise skip by default."
  author: "Addy Osmani"
  datePublished: "2026-05-03"
---

This post explains the design rationale behind the author's [[SoftwareApplication/agent-skills]] project, arguing that AI coding agents default to the shortest path to "done" and skip the senior-engineer work that doesn't show up in a diff — writing specs, writing tests first, sizing changes for review, and refusing to ship what can't be verified. It frames Agent Skills as scaffolding meant to bolt that discipline back onto an agent, and walks through five design principles the project is built on, mapping several of them onto documented practices from *Software Engineering at Google*.

The post distinguishes a "skill" from reference documentation: a skill is a workflow with checkpoints and a defined exit criterion that an agent can actually follow, not an essay a model reads and then produces plausible-sounding text about without doing the underlying work.

## Key Points

- A skill is defined as a workflow with checkpoints and an exit criterion, not reference documentation — the post argues this "process over prose" distinction is what separates a useful skill from a markdown file that changes nothing in practice.
- The project organizes twenty skills around six SDLC phases (define, plan, build, verify, review, ship) with seven slash commands, and a router skill decides which apply to a given task so a small fix activates fewer skills than a complex feature.
- Anti-rationalization tables — a table of excuses an agent might use to skip a workflow step, paired with a written rebuttal — are presented as the project's most distinctive design choice, aimed at LLMs' tendency to produce plausible justifications for skipping work.
- Every skill is said to terminate in concrete evidence (passing tests, clean build output, a runtime trace, a reviewer sign-off) rather than accepting "seems right" as sufficient.
- Skills are loaded via progressive disclosure — activated by task phase through a router skill rather than all loaded into context at session start — to avoid degrading performance with unused instructions.
- A non-negotiable scope-discipline rule ("touch only what you're asked to touch") is presented as the practice with the largest effect on whether an agent's PR is mergeable without being unwound.
- The post maps specific skills to specific published Google engineering practices: Hyrum's Law in `api-and-interface-design`, the test pyramid and the Beyoncé Rule in `test-driven-development`, ~100-line PR sizing with severity labels in `code-review-and-quality`, and Chesterton's Fence in `code-simplification`, among others.
- The project is reported to have crossed 27,000 GitHub stars at the time of writing and is described as MIT-licensed.

## Context

The post frames itself as the explanation the project's own README doesn't fully cover — why each design choice exists rather than how to install it — and positions Agent Skills as one layer within the author's broader [[DefinedTerm/harness-engineering]] framing, sitting alongside `AGENTS.md`, hooks, and tools as components with their own specific job.
