---
source:
  type: url
  url: 'https://zenn.dev/sasadango28/articles/claude-code-harness-engineering-20260415'
  hash: sha256:7cd025ec9144f01f5f085366ebe9b407568f7b2adb0223a1b34b86cd6fb9b7d6
  license:
  lang: ja

schema:
status: generated
last_generated_at: "2026-10-16"
extracted_tokens: 3679
generated_pages:
  - .wikicommit/entity/en/BlogPosting/practicing-harness-engineering-with-claude-code-five-layers.md
failed_pages: []
---

## Summary

A data engineer describes applying harness engineering to Claude Code in a personal information-gathering and knowledge-management repository, arranged as five layers: CLAUDE.md as the project's constitution, `.claude/rules/` for domain rules, Skills for reusable workflows, Agents for context-isolated subagents, and `settings.json` permissions as the safety device. Lessons drawn include stating what the agent should not do, moving deterministic work out of the LLM into scripts, keeping CLAUDE.md small, refining permissions through use, and deferring Hooks until `deny` rules prove insufficient.

## Generation Notes

- "Mitchell Hashimoto": privacy — a living individual named as the originator of the harness-engineering concept; exclude_living_persons is on and entity-policy.md allows no exception for living public figures.
