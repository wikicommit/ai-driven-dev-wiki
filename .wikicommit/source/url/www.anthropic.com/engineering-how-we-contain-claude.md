---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/how-we-contain-claude'
  hash: sha256:2f700ae2ec223a60449a0e82f0575d72c600c7a2d945aa408b3384763f2d15c1
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 8967
generated_pages:
  - .wikicommit/entity/en/BlogPosting/how-we-contain-claude-across-products.md
  - .wikicommit/entity/en/SoftwareApplication/claude-cowork.md
failed_pages: []
---

## Summary

An Anthropic engineering post (May 2026) on capping the blast radius of agents through containment rather than per-action human approval. It classifies agent security risks (user misuse, model misbehavior, external attackers) and defensive components (environment, model, external content), then describes three isolation patterns — an ephemeral gVisor container for claude.ai, a human-in-the-loop OS sandbox for Claude Code, and a local VM for Claude Cowork — together with incidents the authors missed, and closes with principles: contain at the environment layer first, match isolation to the user's capacity for oversight, and be wary of custom components.

## Generation Notes

"Max McGuinness", "Mikaela Grace", "Jiri De Jonghe", "Jake Eaton", "Abel Ribbink": exclude_reason privacy — the post's authors, living individuals; entity-policy.md rules out pages about living individuals.
