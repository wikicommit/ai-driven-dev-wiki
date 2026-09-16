---
title: "AGENTS.md"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agents-md/'
    hash: sha256:ee43d2eb32e588d7c7bbadd7d7913c23bca92a53f6a8f01113bcb23e8b12d029
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A markdown file, conventionally at a repository's root, injected into an AI coding agent's context on every turn to record project conventions and non-obvious facts the agent cannot discover by reading the code itself."
---

AGENTS.md is a markdown file, conventionally placed at the root of a repository, that gets loaded into an AI coding agent's context on every prompt to convey project-specific conventions and constraints. Common coding agents can auto-generate one via an `/init`-style command, which scans a codebase and produces a description of its directory structure, tech stack, and testing conventions.

## Usage

Cited research summarized in the source found that a human-authored `AGENTS.md` recording genuinely non-discoverable, operationally significant facts (e.g. "use `uv` for package management") measurably changed agent behavior and improved task success, while an auto-generated file — typically a codebase overview the agent could otherwise discover by reading the repository directly — was found to add cost without improving, and in some cases while reducing, task success. The source also describes an "anchoring effect": once a technology or pattern is mentioned in the file, it stays in context on every subsequent prompt, which can bias the agent toward it even where it is no longer the current convention.

## When It Applies

The source frames a good `AGENTS.md` as a living record of codebase friction rather than a permanent configuration: a line is added when an agent repeatedly makes the same mistake, and removed once the underlying problem (a confusing directory structure, a build pipeline that should catch something automatically) has been fixed instead. It states the practical filter as: if the agent could discover a fact by reading the code, it doesn't belong in the file. The source also treats a single, static, repository-root file as a structural limitation for any codebase past a certain complexity, since a flat instruction set cannot condition its content on what kind of task is being run, and proposes a hierarchy of directory- or module-scoped files, automatically maintained, as the intended replacement. It further describes a more elaborate three-layer version of this idea (a minimal routing file, task-scoped skill files, and a maintenance subagent), noting that no major coding agent yet exposes the lifecycle hooks needed to build that fuller architecture cleanly.

## Related Terms

[[DefinedTerm/harness-engineering]], [[DefinedTerm/agentic-context-engineering]]
