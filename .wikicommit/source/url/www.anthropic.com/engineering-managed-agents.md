---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/managed-agents'
  hash: sha256:058bb96f68b5ec148e00110cca6d9517e4d5dcba8d1d14b840b8aef1a5da3ed2
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 4928
generated_pages:
  - .wikicommit/entity/en/BlogPosting/scaling-managed-agents-decoupling-the-brain-from-the-hands.md
  - .wikicommit/entity/en/SoftwareApplication/claude-managed-agents.md
  - .wikicommit/entity/en/DefinedTerm/brain-hands-session-split.md
  - .wikicommit/entity/en/DefinedTerm/meta-harness.md
failed_pages: []
---

## Summary

Anthropic describes the design of Managed Agents, its hosted service for long-horizon agent work, which virtualizes an agent into a session (an append-only event log), a harness (the loop that calls Claude and routes its tool calls) and a sandbox, each behind a stable interface. Decoupling the "brain" from the "hands" and the session let containers and harnesses fail and be replaced independently, kept credentials out of the sandbox, and cut p50 time-to-first-token by roughly 60% and p95 by over 90%. The post frames Managed Agents as a meta-harness that stays unopinionated about the specific harness Claude will need in future.

## Generation Notes

"Lance Martin", "Gabe Cemaj", "Michael Cohen": excluded (privacy) — the post's credited authors, living individuals; no existing pages.
