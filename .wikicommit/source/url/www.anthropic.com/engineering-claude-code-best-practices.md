---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/claude-code-best-practices'
  hash: sha256:9aae24f8b850a5f9c8a6f561be1fecf54f29e1ddc4658d00ecded22bccb82b82
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 10503
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/claude-code.md
  - .wikicommit/entity/en/DefinedTerm/permission-modes.md
  - .wikicommit/entity/en/DefinedTerm/sub-agent-architecture.md
  - .wikicommit/entity/en/DefinedTerm/agent-hooks.md
failed_pages: []
---

## Summary

The Claude Code documentation's best-practices page, organising its advice around one constraint: the context window fills quickly and the model's performance degrades as it does. It covers giving the agent a check it can run so the loop closes without a human, separating exploration and planning from implementation via plan mode, writing a short CLAUDE.md and pruning it, configuring permissions and sandboxing, and extending the tool with hooks, skills, subagents and plugins — then turns to managing a session (course-correcting, clearing context, rewinding to checkpoints) and to scaling out through non-interactive mode, parallel sessions, fan-out and an adversarial review step.

## Generation Notes

- The registered URL resolves to the Claude Code documentation, a continuously-updated reference rather than a dated work, so it was not treated as a source-as-entity and no page was created for the document itself.
