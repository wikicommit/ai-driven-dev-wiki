---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/april-23-postmortem'
  hash: sha256:269dd6e147333715b02167db5eedbc394fe254ceebed15d9cf7f2a05a25c87f5
  license:

schema:
status: generated
last_generated_at: '2026-09-22'
extracted_tokens: 4135
generated_pages:
  - .wikicommit/entity/en/BlogPosting/update-on-recent-claude-code-quality-reports.md
  - .wikicommit/entity/en/DefinedTerm/reasoning-effort.md
  - .wikicommit/entity/en/SoftwareApplication/claude-code.md
  - .wikicommit/entity/en/DefinedTerm/token-caching.md
failed_pages: []
---

## Summary

Anthropic traces a month of user reports that Claude's responses had worsened to three separate changes rather than one regression: Claude Code's default reasoning effort lowered from high to medium, a caching optimization that a bug made clear prior reasoning on every turn instead of once, and a system prompt instruction limiting verbosity. The three affected Claude Code, the Claude Agent SDK and Claude Cowork, with the API unaffected, and all are stated as resolved as of April 20, 2026 in version 2.1.116. The post also sets out process changes, including a broad per-model evaluation suite and line-by-line ablations for every Claude Code system prompt change, and announces a reset of usage limits for all subscribers.
