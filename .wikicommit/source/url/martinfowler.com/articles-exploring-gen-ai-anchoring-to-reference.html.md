---
source:
  type: url
  url: 'https://martinfowler.com/articles/exploring-gen-ai/anchoring-to-reference.html'
  hash: sha256:b601ee397808d7ca15740ec6016dabb27ff69994f59a8f5677d5598aef271cb6
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 2065
generated_pages:
  - .wikicommit/entity/en/BlogPosting/anchoring-ai-to-a-reference-application.md
  - .wikicommit/entity/en/DefinedTerm/code-pattern-drift-detection.md
failed_pages: []
---

## Summary

In this September 2025 "Exploring Gen AI" article, Birgitta Böckeler describes using an MCP server to give a coding agent a compilable reference application, such as a service template, as its source of code samples, and then extending the server to expose the reference's git commits so the agent can detect where an existing codebase has drifted from the reference's patterns. The agent first writes a drift report for human review and then writes code to close the gaps; the author notes that simple changes can be handled deterministically by codemod tools such as OpenRewrite, and that AI adds value where the required changes are too dynamic for regex-based recipes.

## Generation Notes

- "Birgitta Böckeler": excluded (privacy) — the article's author, a living individual named by the source without being its subject, per entity-policy.md.
