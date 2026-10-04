---
title: "Claude Codeでハーネスエンジニアリングを実践する — 5層の設計パターン"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, claude-code-configuration, agent-skills]
sources:
  - type: url
    url: 'https://zenn.dev/sasadango28/articles/claude-code-harness-engineering-20260415'
    hash: sha256:79cb7abe556ce0e76b248f159ac27efc7053962370948d78172ea53f09fa7494
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A data engineer's account of applying harness engineering to Claude Code in a personal knowledge-management repository, organised as five layers: CLAUDE.md, rules, skills, agents and permission settings."
  author: "28"
  datePublished: "2026-04-15"
---

This post applies [[DefinedTerm/harness-engineering]] to [[SoftwareApplication/claude-code]] in one concrete setting: the author's own repository for gathering information and managing knowledge. Its premise is that writing good prompts has limits, and that Claude Code offers several mechanisms for designing and managing the agent's behaviour the way code is managed. Combining them to steer the agent in the intended direction is what the author means by harness engineering.

The author grounds the need for a harness in the statelessness of LLMs: a model keeps no memory between calls, a conversation only appears continuous because the application resends its history, and so project rules, past mistakes and directory structure exist for the model only if they are injected from outside. Designing that injection is, in the author's framing, the harness. The author places this beside prompt engineering (optimising what is asked) and [[DefinedTerm/context-engineering]] (optimising what is shown), describing context engineering as part of the harness and harness engineering as the broader idea, covering tools, permissions and guardrails.

## Key Points

- The author lists six Claude Code mechanisms as harness components — `CLAUDE.md`, rules in `.claude/rules/`, skills, agents, `settings.json`, and hooks — and describes them as stacking in layers rather than working independently. The post implements five of them, all except hooks.
- Layer 1, [[DefinedTerm/claude-md]], is treated as the project's "constitution": its purpose, directory structure, technical and security rules, and explicitly what the agent should not do. The author describes listing what not to do as defining the scope of action rather than suppressing reasoning.
- For team repositories, personal preferences can be kept out of the shared `CLAUDE.md` by adding an `@my-preferences.md` import line and ignoring that file in Git; the author notes that a missing import target is simply ignored.
- Layer 2 puts domain rules in Markdown files under `.claude/rules/`. A rule file without a `globs` setting is loaded at session start; one with `globs` is loaded only when Claude reads a matching file, which saves context. The author uses the undocumented `globs` key rather than the documented `paths`, citing reported bugs in parsing `paths`.
- Layer 3 uses [[DefinedTerm/agent-skills]] for reusable workflows; the author runs thirteen. The key design principle stated is separating work the LLM should do from work a script should do.
- The author's example: an early news-gathering skill had the LLM fetch and parse RSS feeds; a revised version moved fetching and parsing into a Python script and left the LLM only translation and classification, which the author reports cut token use to a sixth and processing time to a third.
- Layer 4 uses agents, subagents called by name that run in a separate context, so that a search across hundreds of notes returns only a summary to the main conversation. The author identifies context isolation as their benefit.
- Layer 5 uses `settings.json` permissions as the safety device: allow broadly what the work needs so confirmations do not break the rhythm, deny destructive operations explicitly, and keep machine-specific permissions in `settings.local.json`.
- Lessons the author draws from the setup: stating what the agent should not do was the most cost-effective decision; moving deterministic processing to scripts improved token use and stability; `CLAUDE.md` should stay small — "a constitution, not an encyclopedia" — with detail delegated to rules and skills; and permissions converge only through use.
- The author has not adopted hooks. The post contrasts `CLAUDE.md` and rules as advisory with hooks as deterministic, and argues that for blocking alone `deny` rules often suffice; hooks become necessary for dynamic judgments that pattern matching cannot express, and handlers that call an LLM add token overhead on every tool call. See [[DefinedTerm/agent-hooks]].

## Context

The post opens with a short history of the term, attributing the concept to a blog post by Mitchell Hashimoto and pointing to later articles from OpenAI, Anthropic and Martin Fowler; those accounts are covered on their own pages, such as [[BlogPosting/harness-engineering-for-coding-agent-users]] and [[BlogPosting/harness-design-for-long-running-application-development]]. What this post adds is a single practitioner's layered configuration, and its recommendations rest on the author's own repository rather than on measurement across projects. The author's stated approach is to start minimal and add mechanisms only after observing real failures — staying with `deny` while it is enough and introducing hooks when conditional judgments are needed.
