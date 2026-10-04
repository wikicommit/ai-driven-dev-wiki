---
source:
  type: url
  url: 'https://habr.com/ru/articles/1042408/'
  hash: sha256:c60b8325646056c7f0ec17119edf53b1216097738e16003b09c633aff670fd6b
  license:
  lang: ru

schema:
status: generated
last_generated_at: "2026-10-04"
extracted_tokens: 8571
generated_pages:
  - .wikicommit/entity/en/BlogPosting/a-year-with-claude-code-whats-in-the-claude-directory.md
failed_pages: []
---

## Summary

A Russian-language Habr retrospective by a backend Python developer on a year of using Claude Code on every task. It reports where the tool helped (bulk routine edits with plan-first prompting, reading unfamiliar repositories, writing tests, summarising pull requests) and where it fell short (generic architecture answers without context, concurrency bugs, drift in long sessions), and argues that most of the value comes from what sits in the .claude/ directory: a two-level CLAUDE.md, a PostToolUse hook that runs tests, skills such as frontend-design, slash commands, and a cross-check of risky changes with OpenAI's Codex.
