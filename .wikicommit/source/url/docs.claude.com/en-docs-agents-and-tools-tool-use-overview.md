---
source:
  type: url
  url: 'https://docs.claude.com/en/docs/agents-and-tools/tool-use/overview'
  hash: sha256:b7ea3ad279057166da87ad1e9b7af7e7b420910140fa982f5028a9e7c19e5271
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 5792
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/client-and-server-tools.md
failed_pages: []
---

## Summary

Anthropic's documentation overview of tool use with Claude, covering how tools are defined and called, when Claude decides to call one, and which tool fits which task. Its organizing distinction is where a tool's code executes: client tools run in the calling application, which handles the tool_use block and returns a tool_result, while server tools run on Anthropic's infrastructure and return results directly. It also covers steering tool-calling behaviour through the system prompt and tool_choice, behaviour when required parameters are missing, and how tool use is priced.
