---
source:
  type: url
  url: 'https://zenn.dev/shintaroamaike/articles/df3ecc0ddee047'
  hash: sha256:ed1e00178a0ca382854e79709eae5586c0b71d612ff7e82aac0e1c75dff42146
  license:
  lang: ja

schema:
status: pending
last_generated_at: "2026-10-04"
extracted_tokens: 4557
generated_pages:
  - .wikicommit/entity/en/BlogPosting/implementing-harness-engineering-with-claude-code-skills.md
  - .wikicommit/entity/en/SoftwareApplication/autoharness-skill.md
failed_pages: []
---

## Summary

The author presents AutoHarness, a set of Claude Code skills inspired by Google DeepMind's AutoHarness paper, which analyses a project to generate a natural-language rule file and a verification script and then updates them when rule violations or feedback occur. A small self-reported trial (n=5 per condition) found rules such as using `pathlib.Path` and `Decimal` followed only with the harness, while bug-fix rates were similar, and a June 2026 revision frames CLAUDE.md as the describe layer and hooks as the enforce layer, suggesting the verification script be wired to a PostToolUse hook.

## Generation Notes

- "ShintaroAmaike": privacy — the post's author, a private individual rather than a public figure; entity-policy.md rules out pages about such individuals.
- "Boris Cherny": privacy — a living individual discussed in a column about how he uses CLAUDE.md; exclude_living_persons is on and entity-policy.md allows no exception for living public figures.
- "Cat Wu": privacy — a living individual mentioned alongside Boris Cherny; exclude_living_persons is on.
