---
source:
  type: url
  url: 'https://habr.com/ru/articles/1086832/'
  hash: sha256:9c76f0c74d68bede0b7f7ea5e41acfac5237a0fe31876a274fcd47109094c0b6
  license:
  lang: ru

schema:
status: generated
last_generated_at: "2026-10-04"
extracted_tokens: 10621
generated_pages:
  - .wikicommit/entity/en/BlogPosting/a-team-of-agents-in-claude-code-from-task-to-release.md
  - .wikicommit/entity/en/DefinedTerm/agent-teams.md
failed_pages: []
---

## Summary

A Russian-language Habr case study by a developer who spent six months building a service alone with Claude Code agents organised, through the Agent Teams feature, as a team of twelve roles. Each role is a markdown slash-command file whose prohibitions matter more than its duties; a weekly analyst cycle and a per-task tech-lead pipeline (architect, backend and frontend, DevOps, QA, documentation) leave the human two decision points, and a separate code-review stage is replaced by up-front architecture decisions, automated checks and knowledge kept in repository files such as ADRs and failure diagnoses.

## Generation Notes

- "Sergey Ladygin": exclude_reason privacy — the article's author, a living individual who is not a public figure; entity-policy.md rules out pages about living individuals.
- "Scruma": exclude_reason theme_mismatch — the team-retrospective service the author was building; the article uses it only as the project the agent team works on, and the product itself is unrelated to the wiki's theme.
