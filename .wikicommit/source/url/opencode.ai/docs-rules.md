---
source:
  type: url
  url: 'https://opencode.ai/docs/rules/'
  hash: sha256:7cd8c6d50ef202d91e43e65062c29cdda2d416ea578da276ae9ee84503315a7d
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 2504
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/opencode.md
failed_pages: []
---


## Summary

OpenCode's documentation page on rules explains how custom instructions are supplied to the agent through an `AGENTS.md` file, which the `/init` command can create or improve in place, placed either at a project root or globally under `~/.config/opencode/`. It describes Claude Code compatibility fallbacks (`CLAUDE.md`, `~/.claude/CLAUDE.md`, `~/.claude/skills/`), the order in which rule files are looked up, and how additional instruction files, including remote URLs, can be listed in the `instructions` field of `opencode.json`.
