---
source:
  type: url
  url: 'https://docs.anthropic.com/en/docs/claude-code/memory'
  hash: sha256:b82b912f1cb5142539e561088fe1795bdeada1ef689b12e535152c8fafc326ee
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 13759
generated_pages: [".wikicommit/entity/en/DefinedTerm/claude-md.md", ".wikicommit/entity/en/DefinedTerm/auto-memory.md"]
failed_pages: []
---

## Summary

Anthropic's Claude Code documentation on how Claude carries knowledge across sessions through two mechanisms: CLAUDE.md files that the user writes (with managed, user, project and local scopes, @path imports, path-scoped rules in .claude/rules/, and optional reading of AGENTS.md) and auto memory, notes Claude writes itself into a per-repository memory directory indexed by MEMORY.md. It also covers loading order, size guidance, the /memory command, and troubleshooting when instructions are not followed or seem lost after compaction.
