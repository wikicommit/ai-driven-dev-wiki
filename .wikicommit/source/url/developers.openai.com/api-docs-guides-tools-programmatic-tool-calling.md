---
source:
  type: url
  url: 'https://developers.openai.com/api/docs/guides/tools-programmatic-tool-calling'
  hash: sha256:387e308af93bf5e395e63fc75ef5feab5991b415cfa035a3b416ed10b3b296ac
  license:
  lang: en

schema:
status: generated
last_generated_at: "2026-09-30"
extracted_tokens: 16492
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/programmatic-tool-calling.md
failed_pages: []
---

## Summary

OpenAI's API documentation guide to Programmatic Tool Calling, a hosted tool with which a model writes and runs JavaScript in an isolated OpenAI-hosted V8 runtime to orchestrate its tool calls, with parallel calls, loops and conditions and intermediate results kept out of the model's context. It explains when to prefer it over direct tool calling, how to enable it in the Responses API with the `programmatic_tool_calling` tool and per-tool `allowed_callers`, the `program` / `function_call` / `program_output` response items and the continuation loop for client-owned function calls, how to design and evaluate tools for programs, and that the Agents API enables it by default.
