---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents'
  hash: sha256:2fa27ef4cd354e98bc9fd4d6cc5bec7f182d3b5a96745c6de6f694f18541f1a6

schema:
status: generated
last_generated_at: "2026-08-21"
extracted_tokens: 4856
generated_pages:
  - .wikicommit/entity/en/TechArticle/effective-harnesses-for-long-running-agents.md
  - .wikicommit/entity/en/DefinedTerm/agent-harness.md
  - .wikicommit/entity/en/DefinedTerm/compaction.md
  - .wikicommit/entity/en/DefinedTerm/agentic-memory.md
failed_pages: []
---


## Summary

Anthropic's engineering post of 26 November 2025 by Justin Young, reporting an internal experiment in getting the Claude Agent SDK to make consistent progress across many context windows. Its two-part harness — an initializer agent that builds the environment on the first run, a coding agent that makes incremental progress every session afterwards — is recorded as its own page, and each of its four components is introduced there as the fix for a specific observed failure. Three existing pages gained material from it: the agent harness page, which previously credited this post only secondhand through the OpenDev report and now has the primary source; the compaction page, for the finding that compaction alone is insufficient across sessions; and the agentic memory page, for progress files and git history as the primary cross-session mechanism and the JSON-over-Markdown durability finding.

No entities were excluded. The post's author is named only as its author with no independent facts stated about him, so no Person page was created.
