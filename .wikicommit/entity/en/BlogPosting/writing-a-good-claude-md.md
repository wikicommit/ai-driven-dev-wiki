---
title: "Writing a good CLAUDE.md"
type: "schema:BlogPosting"
lang: en
tags: [context-engineering, agent-instructions, coding-agents]
sources:
  - type: url
    url: 'https://www.humanlayer.dev/blog/writing-a-good-claude-md'
    hash: sha256:fa23502d53bddbb8cccdecb704426d3137dbffcf62a88ed2965780a516d208fb
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A HumanLayer post on how to write a CLAUDE.md (or AGENTS.md) file: treat it as onboarding for the agent, keep it short and universally applicable, and use progressive disclosure for everything else."
  author: ["Kyle"]
  datePublished: "2025-11-25"
  publisher: "HumanLayer"
---

This post, which it says applies equally to AGENTS.md, starts from the premise that LLMs are (mostly)
stateless: their weights are frozen at inference time, so the only thing a model knows about a codebase
is the tokens put in front of it. Since [[DefinedTerm/claude-md]] is, in the post's words, the only file
that by default goes into every conversation with the agent, it treats the file as the way to onboard
Claude to a codebase — covering **what** (the stack and a map of the project), **why** (the purpose of
the project and its parts) and **how** (how to work on it, and how to verify changes).

Much of the post is about keeping the file small. It reports that Claude Code injects CLAUDE.md
alongside a system reminder saying the context "may or may not be relevant", so Claude ignores content it
judges irrelevant to the current task — and the more non-universal instructions a file holds, the more
likely it is ignored. The authors speculate that Anthropic added this because many CLAUDE.md files are
full of narrowly applicable "hotfix" instructions. Its six concluding recommendations follow from that.

## Key Points

- CLAUDE.md is for onboarding Claude into the codebase and should define the project's why, what and how.
- Less is more: include as few instructions as reasonably possible. The post argues that models can
  follow only a limited number of instructions consistently, that smaller models degrade much faster,
  and that as the count rises instruction-following worsens across all instructions rather than only the
  later ones; the authors' own analysis puts Claude Code's system prompt at about 50 instructions before
  anything is added.
- Keep the contents concise and universally applicable. The post reports general consensus that under
  300 lines is best, notes Anthropic has no official length recommendation, and says HumanLayer's root
  CLAUDE.md is under sixty lines.
- Use progressive disclosure: keep task-specific instructions in separate, descriptively named markdown
  files (for example under an `agent_docs/` folder), list them in CLAUDE.md, and let Claude decide which
  to read; prefer `file:line` pointers to copied code snippets, which go stale (see
  [[DefinedTerm/progressive-disclosure]]).
- Claude is not a linter: never send an LLM to do a linter's job. Use deterministic formatters and linters,
  for example from a Claude Code `Stop` hook, and rely on LLMs being in-context learners that tend to follow
  existing code patterns (see [[DefinedTerm/agent-hooks]]).
- Do not use `/init` or otherwise auto-generate the file: because it affects every phase of the workflow
  and every artifact produced, the post calls it the highest-leverage point of the harness and says every
  line deserves careful thought.

## Context

The post frames its rules as HumanLayer's recommendations following context engineering best practices,
with the caveat "your mileage may vary" — rules to break once you understand when and why. Its evidence is
the authors' own experience and analysis of Claude Code, plus research it acknowledges has not been
investigated in an incredibly rigorous manner. Anthropic's own guidance on the file is summarized on the
[[DefinedTerm/claude-md]] page. Related pages include [[DefinedTerm/agents-md]],
[[DefinedTerm/context-engineering]] and [[BlogPosting/skill-issue-harness-engineering-for-coding-agents]].
