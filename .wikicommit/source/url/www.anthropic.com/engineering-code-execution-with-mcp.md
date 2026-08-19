---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/code-execution-with-mcp'
  hash: sha256:00595274b94dc84401f5d20a982fac4221bd6fef1a8b89c318ac7ad3122afaf8

schema:
status: generated
last_generated_at: "2026-08-19"
extracted_tokens: 5016
generated_pages:
  - .wikicommit/entity/en/TechArticle/code-execution-with-mcp.md
  - .wikicommit/entity/en/DefinedTerm/code-execution-with-mcp.md
  - .wikicommit/entity/en/DefinedTerm/model-context-protocol.md
  - .wikicommit/entity/en/Organization/anthropic.md
  - .wikicommit/entity/en/DefinedTerm/agent-skills.md
failed_pages: []
---

## Summary

Anthropic engineering post of 4 November 2025 by Adam Jones and Conor Kelly, arguing that agents scale better by writing code against MCP servers than by calling their tools directly. It names two token sinks — tool definitions loaded upfront and intermediate results passing through the model — and proposes exposing each server's tools as files in a generated TypeScript tree, reporting one example workflow falling from 150,000 tokens to 2,000. It also concedes the operational cost of running agent-generated code in a sandboxed environment.
