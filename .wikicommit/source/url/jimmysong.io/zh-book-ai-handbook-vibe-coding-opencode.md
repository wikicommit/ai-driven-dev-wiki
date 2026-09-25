---
source:
  type: url
  url: 'https://jimmysong.io/zh/book/ai-handbook/vibe-coding/opencode/'
  hash: sha256:3cd1ec82817b79f22b6e50da9384b8f2ac1a6884b066eed6a1d9f4ad3e9fba97
  license:

schema:
status: partial
last_generated_at: "2026-09-24"
extracted_tokens: 4228
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/opencode.md
failed_pages: []
---

## Summary

A draft chapter of Jimmy Song's online handbook 智能体构建指南, created 11 January 2026, describing OpenCode, an open-source AI coding agent whose primary interface is the terminal, and Oh My OpenCode, a user-level convention layer built around it. It sets out OpenCode's three-layer architecture (terminal interface, agent runtime, extension tools), its model-agnostic support for cloud and local models, and its division of labour between a Plan agent that only plans and a Build agent that changes code. It closes with engineering advice: define an AGENTS.md context file, route tasks to models by difficulty, require planning before execution, and connect external tools through MCP.

## Generation Notes

- "Jimmy Song" (the handbook's author): excluded, privacy — a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
- This chapter is a section of a continuously-updated online handbook and is marked 草稿 (draft), so it was not treated as a source-as-entity.
- "Oh My OpenCode" was not given a page of its own: the source describes it only as a convention layer around OpenCode, without establishing it as separately installable software, so it is covered in the OpenCode page's body.
