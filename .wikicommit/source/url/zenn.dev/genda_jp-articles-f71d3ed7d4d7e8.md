---
source:
  type: url
  url: 'https://zenn.dev/genda_jp/articles/f71d3ed7d4d7e8'
  hash: sha256:3b930434d815794b112529193eb4b0eb5224288334a07ea828aa21c4e620cc28
  license:

schema:
status: partial
last_generated_at: "2026-09-22"
extracted_tokens: 3569
generated_pages:
  - .wikicommit/entity/en/BlogPosting/division-of-labor-in-ai-instruction-files.md
  - .wikicommit/entity/en/DefinedTerm/design-md.md
  - .wikicommit/entity/en/DefinedTerm/agents-md.md
  - .wikicommit/entity/en/DefinedTerm/spec-driven-development.md
failed_pages: []
---

## Summary

This post argues that the instruction files handed to AI coding agents have split into three layers with non-overlapping concerns: AGENTS.md/CLAUDE.md for an agent's overall premises and boundaries, SKILL.md for reusable individual tasks, and DESIGN.md — published by Google Labs in April 2026 with an accompanying lint CLI — for design-system specifications. It reads the split as a question of where each layer places the balance between machine-readable and human-readable content, and offers it as a criterion for deciding how to break up a single overloaded CLAUDE.md. It then sets this against spec-driven development, finding a shared philosophy but a different time axis: SDD specs describe what is about to be built and are archived once done, while the three-layer files describe standing norms that are maintained and grow.

## Generation Notes

- "ikenyal": excluded (privacy) — the post's bylined author, a named living individual; entity-policy.md rules out a page about a living individual, and the switch is on. No existing page.
