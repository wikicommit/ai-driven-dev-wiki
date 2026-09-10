---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
  hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
  license:

schema:
status: partial
last_generated_at: "2026-09-10"
extracted_tokens: 7033
generated_pages:
  - .wikicommit/entity/en/BlogPosting/effective-context-engineering-for-ai-agents.md
  - .wikicommit/entity/en/DefinedTerm/attention-budget.md
  - .wikicommit/entity/en/DefinedTerm/compaction.md
  - .wikicommit/entity/en/DefinedTerm/context-engineering.md
  - .wikicommit/entity/en/DefinedTerm/context-rot.md
  - .wikicommit/entity/en/DefinedTerm/just-in-time-context-retrieval.md
  - .wikicommit/entity/en/DefinedTerm/prompt-engineering.md
  - .wikicommit/entity/en/DefinedTerm/structured-note-taking.md
  - .wikicommit/entity/en/DefinedTerm/sub-agent-architecture.md
  - .wikicommit/entity/en/Organization/anthropic.md
  - .wikicommit/entity/en/SoftwareApplication/claude-code.md
failed_pages: []
---

## Summary

Anthropic's Applied AI team presents context engineering — curating and maintaining the
optimal set of tokens available to an LLM during inference — as the natural progression of
prompt engineering for agents that operate over many turns. It argues that context must be
treated as a finite resource subject to context rot and a limited attention budget, and sets
out what a well-calibrated system prompt, tool set, and set of examples look like. For
long-horizon work it describes just-in-time context retrieval alongside three techniques for
working around the context window limit: compaction, structured note-taking, and sub-agent
architectures.

The post's four listed authors — the only individuals this source names who were weighed as
entity candidates, as the `author` values of the source-entity page — were excluded under `.wikicommit/entity-policy.md`'s
`exclude_living_persons` rule, so `author` is recorded as plain text rather than as WikiLinks.
