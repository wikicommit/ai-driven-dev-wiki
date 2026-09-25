---
source:
  type: url
  url: 'https://github.com/CrowdStrike/codestrike'
  hash: sha256:a6e1e972e6ab62486a1b31f8e2651c1a50c1c36eaabcae1511455d402f492e59
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 4912
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/codestrike.md
failed_pages: []
---

## Summary

The GitHub repository README for codestrike, an open-source AI-driven pull request review tool written in Go and published by CrowdStrike in public preview. Given a pull request, it runs an LLM-powered, chain-of-thought review over the diff through an OpenAI-compatible API and posts the result back as a single comment, either from a CLI or from a persistent HTTP service. It is configured through a YAML file (system prompt, tone, guardrails, context files, token budget), supports review personas, can read project instruction files such as CLAUDE.md, AGENTS.md and Cursor rules as context, and ships as a Cursor plugin.
