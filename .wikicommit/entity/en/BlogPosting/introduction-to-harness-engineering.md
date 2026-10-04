---
title: "ハーネスエンジニアリング入門 ── CLAUDE.mdの次に来るAIエージェント制御パラダイム"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, agent-config, claude-code]
sources:
  - type: url
    url: 'https://qiita.com/nogataka/items/d1b3fcf355c630cd7fc8'
    hash: sha256:3fd5e6d04c8d269d9f789b575d8917216722eb38a320372721e33c225935ddf3
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A Qiita article presenting harness engineering as the next step after CLAUDE.md for controlling AI coding agents, breaking a harness into five components and recommending that they be added incrementally as problems appear."
  author: ["nogataka"]
  datePublished: "2026-03-24"
---

This article, posted on Qiita on 24 March 2026, presents [[DefinedTerm/harness-engineering]] as the
paradigm for controlling AI coding agents that comes after [[DefinedTerm/claude-md]]. Its premise is
that an agent's output quality depends heavily on structure: a `CLAUDE.md` file is only a request,
with nothing to enforce its rules, detect violations, or notice when a rule has gone stale, so quality
has to be held by mechanisms rather than by human attention.

The author starts from their own experience of running a project on `CLAUDE.md` alone and describing
the problems that appeared as it grew — inconsistent output between sessions, design decisions lost when
a session ended, more than twenty skills whose order and preconditions became unmanageable, and rule
violations only a human reviewer could catch. From there the article lays out a five-part model of a
harness, reads the [[SoftwareApplication/everything-claude-code]] repository as a full implementation
of it, and gives a staged adoption path.

## Key Points

- The word is taken from horse tack: a harness does not reduce the horse's power but lets it run at full
  strength in the intended direction. The author draws the same picture for agents — constrained by a
  harness, an agent can be fully creative within the constraints — and notes that the software "test
  harness" shares the root.
- Agent control is described as having evolved in three stages: `CLAUDE.md` with stack and conventions
  (first half of 2025); [[DefinedTerm/agents-md]] as a cross-tool open standard plus rules split into
  `.claude/rules/` (mid-2025); and the harness, which integrates execution, verification and memory
  (late 2025 onward). Each earlier stage is said to lack enforcement.
- A harness is said to contain context engineering rather than replace it: `CLAUDE.md` and
  `AGENTS.md` are part of it, with skills, hooks, memory and verification loops layered on top. The
  article's comparison table characterizes a harness as spanning multiple sessions, controlled by
  structural constraints, persistent, and detecting violations automatically.
- The article breaks a harness into five components: rules (declarative constraints in `CLAUDE.md` or
  `.claude/rules/`), skills (reusable procedures — it notes Claude Code has moved skill definitions from
  `.claude/commands/*.md` to `.claude/skills/<name>/SKILL.md`), hooks (event-driven triggers that move
  violation detection from after-the-fact review to the moment of editing), memory (progress files and
  decision logs that persist across sessions), and a multi-layer feedback loop (type checking, linting,
  unit tests, structural tests, end-to-end tests, faster layers giving faster correction).
- On memory, the author warns that Markdown is easy for humans to read but makes it easy for an agent to
  mark tasks done on its own or alter the decision log, and suggests JSON where structural integrity
  matters.
- The recommended adoption is incremental rather than all at once: write `CLAUDE.md` on day one, add
  skills when the same explanation keeps being repeated, add hooks when rule violations become a
  concern, build memory when lost context between sessions becomes a problem, and promote rules over
  time. Installing a complete setup from the first day is said to slow the agent with a flood of hooks.
- For promoting rules the article uses an escalation ladder it attributes to a case study published by
  GMO Internet — documentation, AI verification, tool verification, structural tests — with the rule of
  thumb that a violation occurring three times is promoted one level.

## Context

The article frames harness engineering's limits explicitly: initial and maintenance cost (rules drift
from reality if left alone), excessive hooks slowing every edit, and the fact that a harness steers an
agent's output without enabling what the agent cannot do, leaving complex design and domain decisions
to humans. It also rejects the reading of a harness as distrust of AI, comparing it to the git
strategy, CI/CD and code review within which good human engineers do their best work.

Looking ahead, the author expects agent tools to absorb harness functions natively (citing Claude Code
hooks and Kiro CLI steering files), harness templates to be shared and standardized by language and
framework, and self-improving harnesses that extract patterns from sessions to become common. Several
of the figures it gives — rule counts and structural-test counts — come from the GMO Internet case it
cites rather than from the author's own project, and its before/after comparison is an illustrative
example rather than a measurement.
