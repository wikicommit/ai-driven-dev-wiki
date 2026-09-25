---
source:
  type: url
  url: 'https://cognition.ai/blog/dont-build-multi-agents'
  hash: sha256:c456bd571f488ee46bc4c213e9d4302677f283c444dd4b85a1ad7fa1bd41d480
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 3837
generated_pages:
  - .wikicommit/entity/en/BlogPosting/dont-build-multi-agents.md
  - .wikicommit/entity/en/DefinedTerm/edit-apply-model.md
  - .wikicommit/entity/en/DefinedTerm/context-engineering.md
failed_pages: []
---


## Summary

A June 2025 Cognition blog post arguing that multi-agent architectures, in which subagents work on parts of a task in parallel, are fragile for long-running production agents. It sets out two principles of context engineering — share context, including full agent traces, and recognise that actions carry implicit decisions — and recommends a single-threaded linear agent, optionally with a model that compresses history, using Claude Code's subagents and edit-apply models as examples.

## Generation Notes

- "Walden Yan" (the post's author): excluded, privacy — a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
- "OpenAI Swarm", "AutoGen", "MetaGPT" and "React": not extracted — each is named in passing without facts of its own stated.
