---
source:
  type: url
  url: 'https://simonwillison.net/2026/Feb/9/structured-context-engineering-for-file-native-agentic-systems/'
  hash: sha256:3f82de188c24399ccbce66e5e53af94f0076aa296322a4b9d6a662e0554d1406

schema:
status: generated
last_generated_at: "2026-08-21"
extracted_tokens: 1078
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/grep-tax.md
  - .wikicommit/entity/en/DefinedTerm/context-engineering.md
failed_pages: []
---

## Summary

A link-blog post summarising and quoting a paper on context engineering for structured data, covering 9,649 experiments across 11 models, four serialisation formats and schemas from 10 to 10,000 tables, with SQL generation as a proxy for programmatic agent operations. Willison highlights two results: that the model itself dominated, with frontier models benefiting from filesystem-based context retrieval where leading open-source models did not; and the "grep tax," where a format roughly 25% smaller on disk consumed 138% more tokens at 500 tables and 740% more at 10,000, because models unfamiliar with its syntax could not construct effective refinement patterns.
