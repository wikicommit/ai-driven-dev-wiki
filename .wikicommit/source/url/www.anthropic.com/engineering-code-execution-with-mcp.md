---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/code-execution-with-mcp'
  hash: sha256:100631c97989ce08b85030b756c939a2b9630de43337516938b86c6af9a4f494
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 5058
generated_pages:
  - .wikicommit/entity/en/BlogPosting/code-execution-with-mcp.md
  - .wikicommit/entity/en/DefinedTerm/code-execution-mcp.md
failed_pages: []
---

## Summary

An Anthropic engineering post (Nov 2025) arguing that agents connected to many MCP servers waste context by loading every tool definition upfront and passing intermediate results through the model, and that presenting MCP servers as code APIs the agent calls from a code execution environment addresses both. It describes a filesystem-of-tools implementation, reports a reduction from 150,000 to 2,000 tokens in one example, and lists benefits (progressive disclosure, context-efficient results, control flow, privacy-preserving operations, state persistence and skills) along with the sandboxing overhead code execution adds.

## Generation Notes

"Adam Jones", "Conor Kelly": exclude_reason privacy — the post's authors, living individuals; entity-policy.md rules out pages about living individuals.
