---
source:
  type: url
  url: 'https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/programmatic-tool-calling'
  hash: sha256:42547562a018e3bd7b2b1f333ad79a9b4e7816bd113c85e722cb90d2062d43ec
  license:
  lang: en

schema:
status: generated
last_generated_at: "2026-09-30"
extracted_tokens: 10929
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/programmatic-tool-calling.md
failed_pages: []
---

## Summary

This page of Anthropic's Claude API documentation describes programmatic tool calling, in which Claude writes Python code that calls developer-defined tools from inside a code execution container instead of making one model round trip per tool call, so that intermediate results are filtered or aggregated in code and only the final output enters Claude's context. It covers the `allowed_callers` and `caller` fields, the container lifecycle and timeouts, the request-and-result workflow, constraints and incompatibilities, Anthropic's reported token-efficiency measurements, guidance on which workloads benefit, and alternative self-hosted implementations of the same pattern.
