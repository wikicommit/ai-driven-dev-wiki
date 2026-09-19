---
source:
  type: url
  url: 'https://github.com/invariantlabs-ai/invariant'
  hash: sha256:5a9042b22e273383ebfb67b3e9731ccdf632b5d879e9d72c7088f76568e7f7b1
  license:

schema:
status: generated
last_generated_at: '2026-09-19'
extracted_tokens: 3926
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/invariant-guardrails.md
failed_pages: []
---

## Summary

The Invariant Guardrails repository, describing a rule-based guardrailing layer for LLM- and MCP-powered agent applications that is deployed as a proxy between the application and its model or tool servers, so that it can steer and monitor continuously without invasive code changes. Rules are Python-inspired matching rules that can match flows between tool calls rather than single messages -- its worked examples raise on a `get_inbox` call followed by `send_email` to an address outside the company domain, and on a prompt injection detected in a `get_website` output followed by `send_email`. It runs either through the Gateway proxy, which evaluates rules on each LLM and MCP request, or programmatically through the `invariant-ai` package.
