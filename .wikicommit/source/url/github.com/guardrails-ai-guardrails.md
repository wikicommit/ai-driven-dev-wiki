---
source:
  type: url
  url: 'https://github.com/guardrails-ai/guardrails'
  hash: sha256:c84fe48b906a6637f0bbbd8d2a408cc257b2cd2a1db7c25fd3aea2a74e01b319
  license:

schema:
status: generated
last_generated_at: '2026-09-19'
extracted_tokens: 5973
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/guardrails-ai.md
failed_pages: []
---

## Summary

The Guardrails AI repository, describing a Python framework with two stated functions: running Input and Output Guards that detect, quantify and mitigate specific types of risk in an LLM application, and generating structured data from LLMs. Guards are composed from validators drawn from Guardrails Hub, and structured output is obtained from a Pydantic model either by function calling or, where the model does not support it, by appending the expected schema to the prompt. It can also run as a standalone Flask-served REST service; the repository's news entries record a 2025 Guardrails Index benchmark and a July 2026 move of validators to standard PyPI packages alongside the discontinuation of hosted remote inferencing.
