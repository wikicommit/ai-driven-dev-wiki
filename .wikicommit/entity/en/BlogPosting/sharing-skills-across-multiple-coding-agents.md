---
title: "複数のコーディングエージェントでSkillsを共有する（Claude Code / Codex対応）"
type: "schema:BlogPosting"
lang: en
tags: [agent-skills, coding-tools, context-management]
sources:
  - type: url
    url: 'https://zenn.dev/atamaplus/articles/6d8c3615ff3f33'
    hash: sha256:ca7b63ec337b963433b4413e2e2821307e56ce9248f4a9ff5d3f2cc95316d76a
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A post on the atama plus tech blog describing how a team using both Claude Code and OpenAI Codex keeps one shared set of Agent Skills, by storing the skills in a common directory and pointing each agent's skills directory at it with a symbolic link."
  author: "yutake27"
  datePublished: "2026-01-09"
  publisher: "atama plus techblog"
---

This post addresses a practical problem for teams whose members do not all use the same coding agent: [[DefinedTerm/agent-skills]] are read from a different directory by each agent, so adopting them naively means keeping duplicate copies. The author's team had members on [[SoftwareApplication/claude-code]] and members on [[SoftwareApplication/openai-codex]], and had held off adopting skills for that reason.

The solution described is to keep the real skill files in one shared directory, `.agent/skills/`, and make `.claude/skills` and `.codex/skills` symbolic links to it, so that maintenance happens in one place. It extends a convention the team already followed for project instructions, where `AGENTS.md` is the real file and `CLAUDE.md` is a symlink to it (see [[DefinedTerm/agents-md]] and [[DefinedTerm/claude-md]]). The post is dated as reflecting the state of the tools on 9 January 2026, and a note added on 12 March 2026 says Codex's skills location had since moved from `.codex/skills` to `.agents/skills`.

## Key Points

- The shared layout keeps skill content in `.agent/skills/`, with `.claude/skills` and `.codex/skills` as symbolic links to it; edits are made only in the shared directory.
- The approach reuses the team's existing practice of making `CLAUDE.md` a symlink to `AGENTS.md`, so either agent reads the same guidelines.
- The author explains the motivation for skills in terms of context: instructions in `AGENTS.md` are all loaded at the start of a conversation, whereas a skill has only its name and description loaded at startup and its full content loaded when it is used.
- The team's `AGENTS.md` had grown past 600 lines, so that frontend work also loaded database-design guidelines. The author had the coding agent itself split it into skills, then adjusted the result by hand.
- After the split, `AGENTS.md` kept basic information plus a table listing the available skills, intended to help the agents recognise them.
- The author reports, from the team's own migration, that `AGENTS.md` went from about 600 lines to about 100, unrelated guidelines stopped being loaded during frontend work, and each skill could be edited independently.
- Both agents were checked to recognise the symlinked skills: Claude Code lists them via `/skills`, and Codex shows them when `$` is typed.
- The author reports that VS Code can load Claude Code skills from `.claude/skills/` when its `chat.useClaudeSkills` setting is enabled, and that Cursor's skills support was then available only in its Nightly channel, with a setting that imports skills from `.claude/skills/` and `.codex/skills/`; another symlink can be added for `.cursor/skills/`.

## Context

The author presents symbolic links as a stopgap: the post anticipates that coding agents may one day agree on a common location for configuration files, and until then regards symlinks as the safe way to cope. The adoption itself is tied to timing: the author writes that the team only moved once Anthropic had published Agent Skills as an open standard and OpenAI had implemented skills in Codex. The post also cautions that agent specifications change often and that the method described may become unnecessary; the March 2026 note about Codex's changed directory is an example of exactly that.
