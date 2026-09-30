---
source:
  type: url
  url: 'https://dev.to/zoetaka38/when-ai-reviews-ais-code-youve-built-an-infinite-loop-heres-how-we-stopped-it-4g1n'
  hash: sha256:e728a1e5ac20dcc643c605006d08b8675b906bc6c4143d31cd941d98c8d1418e
  license:
  lang: en

schema:
status: generated
last_generated_at: "2026-09-30"
extracted_tokens: 4073
generated_pages:
  - .wikicommit/entity/en/BlogPosting/when-ai-reviews-ais-code-youve-built-an-infinite-loop.md
  - .wikicommit/entity/en/SoftwareApplication/orange-codens.md
  - .wikicommit/entity/en/DefinedTerm/review-loop-non-convergence.md
failed_pages: []
---

## Summary

The builder of Orange Codens, an AI code review product that hands the fixes for its findings to other AI agents which open fix pull requests, explains how a loop in which AI both reviews and fixes code can run forever and how the product's architecture stops it: handoff only when a PR is merged, no automatic handoff from bot-authored PRs or from verify runs, no finding dispatched twice, and an escape hatch for findings a human queued. It also describes two non-convergence incidents found in end-to-end runs — fix PRs for findings in the same file blocking one another, and repeated new findings on fix PRs — and the fixes adopted, arguing that termination and bounded cost must be guaranteed by the architecture rather than by the model.

## Generation Notes

"Takayuki Kawazoe" (the post's author): excluded, exclude_reason privacy — a living individual; entity-policy.md rules out pages about living individuals.
