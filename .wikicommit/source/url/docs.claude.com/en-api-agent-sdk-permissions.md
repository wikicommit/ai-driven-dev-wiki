---
source:
  type: url
  url: 'https://docs.claude.com/en/api/agent-sdk/permissions'
  hash: sha256:c4534377b28cb19c1b4d96673f98b2d47028ae3535bb6eda233c73d3933d9f61
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 7044
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/claude-agent-sdk.md
  - .wikicommit/entity/en/DefinedTerm/permission-modes.md
failed_pages: []
---

## Summary

Anthropic's Claude Agent SDK documentation for configuring tool permissions. It specifies a fixed six-step evaluation order — hooks, deny rules, ask rules, permission mode, allow rules, then the canUseTool callback — defines six permission modes, sets out the syntax and anchoring rules for scoped allow/deny entries, and is explicit about two traps: auto-approved tools never reach the runtime callback, and an allow list does not constrain bypassPermissions.

## Generation Notes

- The page itself was not extracted as a source entity: it is living vendor documentation with no fixed publication date.
