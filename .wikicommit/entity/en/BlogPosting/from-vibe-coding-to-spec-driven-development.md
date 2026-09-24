---
title: "Del Vibe Coding al Spec Driven Development: cómo dirigir agentes de IA sin perder el control"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, vibe-coding, context-engineering, agent-config, security]
sources:
  - type: url
    url: 'https://carlosazaustre.es/blog/spec-driven-development-agentes-ia'
    hash: sha256:b17e6ce9fa2310498982db3cbb22fd38907d0a482aa53268416a2149e5083282
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Spanish-language post, written up from the author's notes on a Swift agentic-engineering course, arguing that vibe coding suits prototypes but not production, and presenting spec-driven development — a precise specification, human checkpoints and AI as a controlled tool — as the alternative."
  author: ["Carlos Azaustre"]
  datePublished: "2026-05-11"
---

This post by Carlos Azaustre, published on his personal blog, sets
[[DefinedTerm/vibe-coding]] against [[DefinedTerm/spec-driven-development]] and argues for the
second whenever software is headed for production. The author presents it as his own class notes,
rewritten for the blog, from Apple Coding Academy's Swift Agentic Engineering Program, so what it
records is a course's material as one student took it down rather than an independent study.

Its central claim is a change of role: the engineer writes the specification and the AI produces the
code. In the post's words, in spec-driven development the code is not the source of truth — the
specification is, and the code is a by-product of it. Asking an AI to autocomplete a function saves
typing; writing the complete technical contract an agent will execute autonomously demands, the post
says, more thought rather than less.

Most of the post is a practical account of the environment that makes this work — the files that give
an agent persistent context, the economics of the context window, the controls that keep an agent from
acting destructively, and the security exposure of agentic systems — ending with the four-moment cycle
the post attributes to GitHub Spec Kit.

## Key Points

- Vibe coding, on the post's account, is fine for prototypes and harmful in production. Its stated reason is that AI does not write bad code so much as code consistent with the patterns it sees: a bad practice or misconfiguration in the context gets replicated, because the model completes patterns without evaluating whether they are correct.
- The post's framing is that AI does not create engineering judgement, it only amplifies it — with precise context and a clear specification it produces solid results quickly, and with a vague prompt and full autonomy it produces code that compiles but fails in production.
- The engineer's role is described as an "orchestration architect": write the specification precisely, review the plan the AI proposes before it touches anything, verify the implementation at explicit checkpoints, and catch the agent taking a shortcut it should not.
- Vague prompts are presented as a cost problem as well as a quality one: an imprecise request forces the model to explore files blindly and reformulate hypotheses, and the post's remedy is the [[DefinedTerm/crisp-prompt-pattern]] — Context, Role, Instructions, Specifications, Polish/Criteria.
- The project contract file (`CLAUDE.md` or `Constitution.md`) is called the most important file: stack, code conventions and what is forbidden, with concrete examples of why. The post recommends writing it in English, on the stated grounds that models have better coverage of technical instructions in that language, and using categorical capitals such as `FORBIDDEN`, `ALWAYS` and `NEVER`, because models respond better to constraints with no room for interpretation.
- [[DefinedTerm/agent-skills]] are described as Markdown files the agent loads only when needed, each in its own subfolder of a `/skills` directory with a required `SKILL.md` carrying YAML frontmatter. The author's own convention is to write a skill's description in Spanish for the user and its technical instructions in English.
- A `Memory.md` file holds what the agent learns alongside the user. The post gives 200 lines or 25 KB as the point at which it needs consolidating, usually by a subagent that compresses it periodically, because beyond that the agent stops reading it in full.
- Context is treated as a budget spent on every call. The post says quality starts degrading well before the context window is full — see [[DefinedTerm/context-rot]] — and recommends `/compact` at the end of a block of work and `/clear` after long pauses or radical changes of task.
- On pauses, the post states that the KV cache has a five-minute TTL and that resuming after it costs more than continuing would have; the author reports noticing this most with [[SoftwareApplication/openclaw]].
- Model orchestration: the post assigns reasoning, planning and architecture to Opus, routine implementation and search to Sonnet, and simple tasks and atomic subagents to Haiku, and states Opus to be about 19 times more expensive than Haiku.
- Plan Mode (read-only investigation that produces a plan before any code changes) and [[DefinedTerm/agent-hooks]] (Bash or Python scripts outside the model that the agent cannot ignore — a `PreToolUse` hook blocking destructive commands or reads of `.env`, a `PostToolUse` hook requiring a linter to pass) are presented together as the source of real programmatic guardrails.
- On security, the post names [[DefinedTerm/prompt-injection]], the combination of private data, uncontrolled external content and outbound communication it calls the lethal trifecta (compare [[DefinedTerm/lethal-trifecta]]), and supply-chain risk from third-party MCP servers and plugins, and advises auditing any third-party MCP server's source before installing it. The mitigations it recommends are input sanitization, explicit system-prompt precedence, and typed responses that force the agent to fill fixed schemas rather than free text.
- The closing cycle has four moments — specification, technical plan (produced in Plan Mode and approved by a human), atomic tasks with their own acceptance criteria, and implementation with checkpoints — and the post identifies the plan review as the step most often skipped and the one that avoids the most technical debt.
- The post is explicit that spec-driven development does not let people without technical knowledge build production software; it argues the opposite, that it requires qualified engineers able to recognise a plausible-but-wrong architecture or a shortcut that will complicate maintenance.

## Context

The post frames itself as learning notes rather than an expert's method. Some of its specific figures
— the context-degradation threshold and the security statistics it quotes — are given with links to
other publications, while others, such as the cache TTL and the relative cost of the models, are
stated without a citation.

It keeps a place for vibe coding: the author says it will stay useful for weekend prototypes and for
validating an idea before committing to an architecture, and reserves spec-driven development for
software that will scale and hold real users' data.
