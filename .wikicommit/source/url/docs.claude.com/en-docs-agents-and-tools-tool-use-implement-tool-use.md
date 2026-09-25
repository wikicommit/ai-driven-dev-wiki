---
source:
  type: url
  url: 'https://docs.claude.com/en/docs/agents-and-tools/tool-use/implement-tool-use'
  hash: sha256:b617f4377dcd4fcab5698ec8b5919a3fec12cf22b96c9f6c69bfb3d73b497ce6
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 6268
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/tool-use-design-pattern.md
failed_pages: []
---

## Summary

Anthropic's Claude Platform documentation page "Define tools" explains how client tools are declared to the Claude API: each user-defined tool has a name, a detailed plaintext description, a JSON Schema `input_schema` and optional `input_examples`, from which the API constructs a tool-use system prompt. It recommends extremely detailed tool descriptions, consolidating related operations into fewer tools, namespacing tool names by service and returning only high-signal information, and it describes the four `tool_choice` options (`auto`, `any`, `tool`, `none`) together with the models and settings on which forced tool use is not supported.
