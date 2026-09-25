---
source:
  type: url
  url: 'https://www.humanlayer.dev/blog/context-efficient-backpressure'
  hash: sha256:e57c7b4289eae44405b7fa2bcda631a3a903cec96d2347c19da0a422f664cbe9
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 1866
generated_pages:
  - .wikicommit/entity/en/BlogPosting/context-efficient-backpressure-for-coding-agents.md
  - .wikicommit/entity/en/DefinedTerm/backpressure.md
failed_pages: []
---

## Summary

A short HumanLayer blog post from December 9, 2025 recommending that test, build and lint output be swallowed and replaced with a single check mark when a stage passes, with the full output shown only on failure, so coding agents do not waste context on passing results. It gives a run_silent shell wrapper, suggests fail-fast flags, output filtering and framework-specific parsing, and criticizes recent models' own habits of discarding output or piping it to head/tail, which it says end up costing more tokens and human time.

## Generation Notes

- "Dex Horthy" (author, Person): excluded, exclude_reason privacy — a living individual (entity-policy.md).
