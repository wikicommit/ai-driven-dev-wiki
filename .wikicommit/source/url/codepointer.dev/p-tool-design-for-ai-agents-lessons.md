---
source:
  type: url
  url: 'https://codepointer.dev/p/tool-design-for-ai-agents-lessons'
  hash: sha256:798960d4831740d5de8d2d8de9ef9533000b374e32d6edc5fdbe5fa1c6862502
  license:
  lang: en

schema:
status: generated
last_generated_at: "2026-09-30"
extracted_tokens: 7520
generated_pages:
  - .wikicommit/entity/en/BlogPosting/tool-design-for-ai-agents-lessons-from-50-claude-code-tools.md
  - .wikicommit/entity/en/DefinedTerm/tool-search.md
failed_pages: []
---

## Summary

A Code Pointer post that walks through how Claude Code's source assembles tool instructions: each of its 50+ tools ships its own `prompt.ts`, and a four-stage pipeline (registry, filtering, schema rendering, per-session caching) turns them into the tool descriptions the model receives, some of them rewritten from live context such as sandbox settings or which peer tools are loaded. It then examines individual tool prompts — Bash, Read, Edit, Write, Grep, WebFetch, WebSearch, Agent, ToolSearch and others — and draws design lessons, including keeping volatile content out of tool definitions to protect the prompt cache and making tool defaults fail safe.

## Generation Notes

"Yongkyun" (the post's author): excluded, exclude_reason privacy — a living individual; entity-policy.md rules out pages about living individuals.
