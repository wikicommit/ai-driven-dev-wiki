---
source:
  type: url
  url: 'https://developers.openai.com/blog/custom-code-review-rules-for-codex'
  hash: sha256:545da2cc607e493ec8565ebfedabe86da5990d39d08e426344d54fa68908973a
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 9752
generated_pages:
  - .wikicommit/entity/en/BlogPosting/custom-code-review-rules-for-codex.md
  - .wikicommit/entity/en/SoftwareApplication/codex-code-review.md
failed_pages: []
---

## Summary

An OpenAI developer blog post announcing that Codex Code Review can apply custom repository rules written in AGENTS.md, so that review guidance a few experienced reviewers carry — preserving an API contract, keeping customer data out of logs — is kept next to the code and cited in findings. It motivates the feature with rising pull-request volume making review the bottleneck, reports an internal eval in which rule-guided variants recovered 98% of required custom findings against 58.3% for a baseline, and advises starting with a consequential non-obvious invariant, scoping rules to the code they govern, stating the safe path, and leaving mechanical checks to CI.

## Generation Notes

- "Hari Srikanth": excluded (privacy) — the named author of the source post; a living individual named by the source without being its subject, per entity-policy.md.
