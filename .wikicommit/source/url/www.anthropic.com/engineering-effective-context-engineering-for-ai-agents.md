---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
  hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be

schema:
status: generated
last_generated_at: "2026-08-19"
extracted_tokens: 7013
generated_pages:
  - .wikicommit/entity/en/BlogPosting/context-engineering.md
  - .wikicommit/entity/en/DefinedTerm/agentic-memory.md
  - .wikicommit/entity/en/DefinedTerm/coding-agent.md
  - .wikicommit/entity/en/DefinedTerm/compaction.md
  - .wikicommit/entity/en/DefinedTerm/context-engineering.md
  - .wikicommit/entity/en/DefinedTerm/context-files.md
  - .wikicommit/entity/en/DefinedTerm/context-rot.md
  - .wikicommit/entity/en/DefinedTerm/multi-agent-orchestration.md
  - .wikicommit/entity/en/Organization/anthropic.md
  - .wikicommit/entity/en/SoftwareApplication/claude-code.md
  - .wikicommit/entity/en/TechArticle/effective-context-engineering-for-ai-agents.md
failed_pages: []
---
## Summary

Anthropic's engineering post of 29 September 2025 setting out context engineering as the natural progression of prompt engineering, and arguing that context must be treated as a finite attention budget because a model's recall degrades as its context fills. It prescribes system prompts at the "right altitude", tool sets small enough to be unambiguous, curated canonical examples, and just-in-time retrieval, plus three techniques for long-horizon work: compaction, structured note-taking, and sub-agent architectures.
