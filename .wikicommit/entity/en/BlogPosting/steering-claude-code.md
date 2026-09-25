---
title: "Steering Claude Code: when to use CLAUDE.md, skills, hooks, and subagents"
type: "schema:BlogPosting"
lang: en
tags: [context-engineering, agent-tooling, agent-safety]
sources:
  - type: url
    url: 'https://claude.com/blog/steering-claude-code-skills-hooks-rules-subagents-and-more'
    hash: sha256:bb67b24e7e743610aadc45e492a9035d66952bb3cadff52ef8301bc773391708
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Anthropic's guide to the seven ways of instructing Claude Code — CLAUDE.md files, rules, skills, subagents, hooks, output styles and appending the system prompt — compared by when each loads into context, how it survives compaction, what it costs in context and how much authority it carries."
  author: ["Michael Segner"]
  datePublished: "2026-06-18"
  publisher: "[[Organization/anthropic]]"
---

This post from [[Organization/anthropic]] sets out where an instruction to
[[SoftwareApplication/claude-code]] should live. It counts seven methods for instructing Claude's
behaviour — [[DefinedTerm/claude-md]] files, rules, skills, subagents, hooks, output styles and
appending the system prompt — and compares them on three axes: when an instruction loads into
context, whether it persists through long sessions (its behaviour under
[[DefinedTerm/compaction]]), and how much authority it carries. Its framing is that each method trades
context cost against authority, while the choice of model and effort level is a separate dial that
controls how capable Claude is and how hard it works.

Most of the post is a per-method account followed by a decision framework, phrased as a list of
anti-patterns that signal an instruction is in the wrong place. Its sharpest argument is about
enforcement: behaviour that must happen every time, or must never happen, should not be written as a
prompted instruction at all, because the model can fail to follow one.

## Key Points

- **CLAUDE.md** loads at session start and stays for the whole session; a root file is re-read after
  compaction, while a CLAUDE.md in a subdirectory loads only when Claude reads a file under that
  directory and is lost after compaction until the directory is touched again. The post recommends
  keeping it under 200 lines, giving it an owner and reviewing changes to it like code.
- In a shared repository CLAUDE.md grows like any unowned configuration file, and every line costs
  tokens in every session for every engineer; the post says this also dilutes adherence to the
  instructions that matter.
- **Rules** are markdown files in `.claude/rules/`. Unscoped rules behave like CLAUDE.md: always loaded
  at session start and re-injected on compaction. Path-scoped rules, declared with a `paths` field, load
  only when Claude reads matching files; the post describes them, like subdirectory CLAUDE.md files, as
  gone after compaction until a matching path is touched again.
- **Skills** live in `.claude/skills/`; only each skill's name and description load at session start,
  and the full body loads when the skill is invoked by slash command or by matching the task. On
  compaction, invoked skills are re-injected up to a shared budget, oldest dropped first (see
  [[DefinedTerm/agent-skills]]).
- **Subagents** are markdown files in `.claude/agents/`; the body becomes the subagent's system prompt
  and never enters the parent conversation, the subagent runs in a fresh context window, and only its
  final message plus metadata returns. The post states that subagents can nest up to five levels deep
  (see [[DefinedTerm/sub-agent-architecture]]).
- The post's rule of thumb between the two: use a subagent when a side task would clutter the main
  conversation with intermediate results, and a skill when you want the procedure to play out in the
  main thread where you can see and steer it.
- **Hooks** are commands, HTTP endpoints or LLM prompts that fire on lifecycle events; they bypass
  compaction and cost little context because they are code the harness runs rather than instructions
  loaded into context (see [[DefinedTerm/agent-hooks]]).
- **Output styles** are injected into the system prompt and carry the highest instruction-following
  weight of the methods covered. A custom style replaces the default one — which the post warns removes
  Claude Code's default software-engineering instructions — unless `keep-coding-instructions: true` is
  set in the style's frontmatter.
- **Appending the system prompt** via a flag is additive and applies only to that invocation; the
  post notes that it has diminishing returns for adherence as more instructions are added.
- "Every time X, always do Y" belongs in a hook, because the model choosing to run a formatter is
  different from the formatter running automatically.
- "Never do this" is the wrong job for an instruction: under pressure, in a long session, in an
  ambiguous situation, or through a prompt injection in a file it reads, the model can fail to follow a
  prompted rule. The post names hooks and permissions as the deterministic enforcement methods, and
  managed settings as the only way to enforce a deterministic organisation-wide guardrail.
- Procedures belong in skills and facts in CLAUDE.md; a rule that applies only to one path should be
  scoped with `paths:`; personal preferences belong in user-level files rather than a project's
  CLAUDE.md.

## Context

The post is Anthropic's guidance about its own product; the 200-line guideline is offered as a tip and
the five-level nesting limit as a product fact, with no measurements given for either. It closes by pointing to plugins as a way to bundle skills, subagents,
hooks and output styles into a setup shared across teammates or projects.
