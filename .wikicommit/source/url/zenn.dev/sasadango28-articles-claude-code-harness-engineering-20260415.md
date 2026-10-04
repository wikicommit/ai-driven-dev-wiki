---
source:
  type: url
  url: 'https://zenn.dev/sasadango28/articles/claude-code-harness-engineering-20260415'
  hash: sha256:79cb7abe556ce0e76b248f159ac27efc7053962370948d78172ea53f09fa7494
  license:
  lang: ja

schema:
status: pending
last_generated_at: "2026-10-04"
extracted_tokens: 3671
generated_pages:
  - .wikicommit/entity/en/BlogPosting/practicing-harness-engineering-with-claude-code-five-layers.md
failed_pages: []
---

## Summary

A data engineer describes applying harness engineering to Claude Code in a personal information-gathering and knowledge-management repository, arranged as five layers: CLAUDE.md as the project's constitution, `.claude/rules/` for domain rules, Skills for reusable workflows, Agents for context-isolated subagents, and `settings.json` permissions as the safety device. Lessons drawn include stating what the agent should not do, moving deterministic work out of the LLM into scripts, keeping CLAUDE.md small, refining permissions through use, and deferring Hooks until `deny` rules prove insufficient.

## Generation Notes

- "Mitchell Hashimoto": privacy — a living individual named as the originator of the harness-engineering concept; exclude_living_persons is on and entity-policy.md allows no exception for living public figures.
