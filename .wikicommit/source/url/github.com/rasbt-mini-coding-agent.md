---
source:
  type: url
  url: 'https://github.com/rasbt/mini-coding-agent'
  hash: sha256:d078822f471591972946c2fadd69b08a042b517b82152ebf0b98c85384710017
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 4149
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/mini-coding-agent.md
failed_pages: []
---

## Summary

The GitHub repository README for Mini-Coding-Agent, a single-file Python coding agent published as a readable reference implementation of what a coding agent harness is made of rather than as a production tool. It organises the harness around six building blocks — live repository context, a stable prompt prefix for cache reuse, structured tools with validation and approval gates, context reduction and output clipping, transcript plus working-memory persistence with session resume, and bounded delegation to subagents — and documents three approval modes, session resume, REPL slash commands and the CLI flags. The model backend is a locally installed Ollama, with `qwen3.5:4b` as the default, and the project depends on nothing beyond the Python standard library.

## Generation Notes

- "Sebastian Raschka" (rasbt): excluded (privacy) — the repository owner and author of the accompanying tutorial, identified only by handle and personal domain in the source; a living individual, which entity-policy.md rules out. His framing of the six components is attributed to the README on the generated page instead.
