---
source:
  type: url
  url: 'https://ghuntley.com/ralph/'
  hash: sha256:9836ee3ee0773613f370a27796b1e456199be38681f73a47b974e210dd356317
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 10516
generated_pages:
  - .wikicommit/entity/en/BlogPosting/ralph-wiggum-as-a-software-engineer.md
  - .wikicommit/entity/en/DefinedTerm/ralph-loop.md
  - .wikicommit/entity/en/DefinedTerm/backpressure.md
failed_pages: []
---

## Summary

Geoffrey Huntley's July 2025 post introduces "Ralph", a technique for autonomous AI coding that in its purest form is a Bash loop repeatedly feeding the same prompt file to a coding agent, and describes how he used it to build a new esoteric programming language. It sets out the technique's principles — one item per loop, loading the same plan and specifications into context every loop, using subagents to keep the primary context window small, wiring in tests, type checkers and static analysers as backpressure, and tuning the prompt whenever the agent misbehaves — and argues that it suits greenfield projects but still needs senior engineering judgment.

## Generation Notes

- "Geoffrey Huntley": exclude_reason privacy — the post's author, a living individual; entity-policy.md rules out pages about living individuals.
