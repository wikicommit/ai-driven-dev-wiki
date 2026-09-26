---
source:
  type: url
  url: 'https://engineering.mercari.com/en/blog/entry/20260427-mercari-pm-agent-design-automating-the-pm-workflow-with-claude-code-skills-and-mcp/'
  hash: sha256:f446b9545db9ce2a51b98a91bfe525a706f8f22bd2381f38543f927626b9b58a
  license:

schema:
status: generated
last_generated_at: "2026-09-21"
extracted_tokens: 3882
generated_pages:
  - .wikicommit/entity/en/BlogPosting/mercari-pm-agent-design.md
  - .wikicommit/entity/en/DefinedTerm/agent-skills.md
failed_pages: []
---

## Summary

A Mercari Engineering post describing `mercari-pm-agent`, a Claude Code Skill built during an internship that carries a product manager's workflow — problem discovery, data gathering, PRD drafting and UI mockups — through a single session, pulling from Notion, Slack, an in-house Looker/BigQuery platform and Figma over MCP. Its design findings are that splitting a long `SKILL.md` into a thin behaviour definition plus a `references/` directory measurably improved output scores, that MCP sources should be queried in parallel with silent fallback when one is unavailable, and that constraints against fabricating data matter more than instructions to perform it. The author defines evaluation criteria before implementation — an approach the post calls Prompt TDD — and built a second skill whose job is to score the first one's output.

## Generation Notes

- "Shogo Kikuchi" (the post's author): excluded, `privacy` — the entity policy rules out pages about living individuals; named as the author of a source without being its subject.
