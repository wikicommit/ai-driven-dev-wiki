---
source:
  type: url
  url: 'https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/how-tool-use-works'
  hash: sha256:72962bc6dbde244cd4d2ed36591f00bceb8f38f4883c0f7c11aaaafd13504b19
  license:
  lang: en

schema:
status: generated
last_generated_at: "2026-09-30"
extracted_tokens: 4788
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/client-and-server-tools.md
  - .wikicommit/entity/en/DefinedTerm/function-calling.md
failed_pages: []
---

## Summary

This page of Anthropic's Claude API documentation explains the concepts behind tool use: a contract in which the application specifies which operations exist and what shape their inputs and outputs take, while Claude decides when and how to call them and never executes anything itself. It sorts tools by where their code runs — user-defined and Anthropic-schema tools executed by the client, and server-executed tools run by Anthropic — and describes the client-driven agentic loop keyed on `stop_reason`, the server-side loop with its `pause_turn` iteration limit, and when tool use is and is not the right approach.
