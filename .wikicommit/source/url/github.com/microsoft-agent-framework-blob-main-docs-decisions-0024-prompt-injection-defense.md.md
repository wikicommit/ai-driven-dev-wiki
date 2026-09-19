---
source:
  type: url
  url: 'https://github.com/microsoft/agent-framework/blob/main/docs/decisions/0024-prompt-injection-defense.md'
  hash: sha256:51eb7a8188be72cbaed8c44f9f3fb847df2aaacf057d21f16ab59e9312c5d6d9
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 4121
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/fides.md
  - .wikicommit/entity/en/SoftwareApplication/microsoft-agent-framework.md
failed_pages: []
---

## Summary

An architecture decision record in Microsoft's agent-framework repository proposing FIDES, a deterministic, label-based information-flow-control defence against prompt injection. It records the decision to adopt label-based middleware over prompt engineering, content sanitization, separate agent instances and runtime monitoring, and sets out FIDES's four components, its MCP integration and its trade-offs.
