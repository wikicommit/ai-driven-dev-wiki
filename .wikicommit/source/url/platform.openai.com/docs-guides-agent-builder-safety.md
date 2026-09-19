---
source:
  type: url
  url: 'https://platform.openai.com/docs/guides/agent-builder-safety'
  hash: sha256:86e2fc5f860675a072304196ba8e912392902e82d2ffeb390665f20c928e7016
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 9210
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/prompt-injection.md
  - .wikicommit/entity/en/DefinedTerm/guardrails.md
failed_pages: []
---

## Summary

OpenAI's safety guidance for building agents with Agent Builder, a product it says it is deprecating with shutdown scheduled for 30 November 2026. It names two risks — prompt injection, where untrusted text attempts to override the model's instructions, and private data leakage, where a model sends more to a connected MCP server than the user intended with no attacker involved — and then lists mitigations: keep untrusted input out of developer messages and pass it through user messages instead, define structured outputs between workflow nodes to remove freeform channels, document policies and examples in the prompt, configure the models it names at the agent node, keep tool approvals on for MCP tools, sanitize inputs with guardrails nodes that redact PII and detect jailbreaks, and run evaluations and trace grading. It states throughout that these reduce but do not remove the risk and that an agent can still be tricked.
