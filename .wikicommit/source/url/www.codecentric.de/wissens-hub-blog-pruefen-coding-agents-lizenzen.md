---
source:
  type: url
  url: 'https://www.codecentric.de/wissens-hub/blog/pruefen-coding-agents-lizenzen'
  hash: sha256:c38afd754438229f1c0570cd206b7ef55a531a9abaac3e23485f1b8426b6e0ba
  license:
  lang: de

schema:
status: generated
last_generated_at: "2026-10-04"
extracted_tokens: 7206
generated_pages:
  - .wikicommit/entity/en/BlogPosting/do-coding-agents-check-licenses.md
failed_pages: []
---

## Summary

A German-language codecentric blog post by Johannes Barop (July 2026) asking whether coding agents check a library's license before using it. It reports experiments showing that agents usually reproduce library usage from training data without inspecting the library, so license additions, machine-readable markers and code markers placed in the library never reach them, and only a runtime notice written to stderr does — which is effectively the same technique as prompt injection. It concludes that license compliance remains the consumer's responsibility and that a license check should be anchored in the harness, for example as an automatic step before every merge.
