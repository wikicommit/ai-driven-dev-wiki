---
source:
  type: url
  url: 'https://martinfowler.com/articles/function-call-LLM.html'
  hash: sha256:1c1dd75185abb251f131bc42253cf8f85504020b87557cd597a63c250f5362d4
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 8403
generated_pages:
  - .wikicommit/entity/en/TechArticle/function-calling-using-llms.md
failed_pages: []
---


## Summary

In this May 2025 article, Kiran Prakash explains function calling — an LLM analysing a natural-language request and returning a structured description of a function call, with its arguments, for a separate program to execute — by building a Python shopping agent on OpenAI's Chat Completions API. The walkthrough covers unit tests, the system prompt and function schemas, restricting the agent's action space with explicit conditional logic, denylist- and LLM-based guardrails against prompt injection, action classes that translate the LLM's decision into API calls, and using the instructor library with Pydantic to reduce boilerplate. It also discusses whether the pattern could replace rules engines, distinguishes function calling from the broader term tool calling, relates it to the Model Context Protocol's dynamic tool discovery, and recommends starting with low-risk operations.

## Generation Notes

- "Kiran Prakash": excluded (privacy) — the article's author, a living individual named by the source without being its subject, per entity-policy.md.
- "Martin Fowler": excluded (privacy) — quoted once on rules engines and thanked in the acknowledgements, a living individual named in passing, per entity-policy.md.
