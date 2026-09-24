---
source:
  type: url
  url: 'https://codelabs.developers.google.com/agy-cli-sdk-code-review'
  hash: sha256:283b349fe5d611bf6d0c0d2b5ac36978aaa667fac020078c52e2bf0412ba54ae
  license:

schema:
status: generated
last_generated_at: "2026-09-24"
extracted_tokens: 10043
generated_pages:
  - .wikicommit/entity/en/HowTo/ai-assisted-code-review-with-antigravity-cli-and-sdk.md
  - .wikicommit/entity/en/SoftwareApplication/antigravity-sdk.md
failed_pages: []
---

## Summary

A Google Codelabs tutorial that teaches two ways of using Antigravity as a reviewer of vibe-coded changes: interactively with the Antigravity CLI plus an installed code-review agent skill (review the diff, fix, then open a PR), and automatically with a read-only review agent built on the Antigravity SDK and run as a GitHub Action that posts structured findings as a PR comment. The SDK agent is constrained by deny-by-default policies and a pre-tool-call hook that only lets git commands through.
