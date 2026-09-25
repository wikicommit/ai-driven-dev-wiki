---
source:
  type: url
  url: 'https://platform.claude.com/cookbook/tool-use-context-engineering-context-engineering-tools'
  hash: sha256:ff18c6ce4f289fc1d0603542473d89de2170efe173360a83c70d460ec9204888
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 30526
generated_pages:
  - .wikicommit/entity/en/TechArticle/context-engineering-memory-compaction-and-tool-clearing.md
  - .wikicommit/entity/en/DefinedTerm/tool-result-clearing.md
  - .wikicommit/entity/en/DefinedTerm/compaction.md
  - .wikicommit/entity/en/DefinedTerm/structured-note-taking.md
failed_pages: []
---

## Summary

A Claude Cookbook notebook published in March 2026 that compares three context-engineering primitives for long-running agents — compaction, tool-result clearing, and the memory tool — using a research agent that reads a large document corpus across multiple sessions. It explains what each primitive operates on, what it trades away and which problem it solves, maps them to Anthropic's first-party API features and their configuration knobs, and shows how they can be layered or deliberately left out depending on the workload.

## Generation Notes

"Isabella He": privacy — the notebook's named author, a real individual named by the source without being its subject, whom entity-policy.md rules out.
