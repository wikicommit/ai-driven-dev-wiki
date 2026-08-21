---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/managed-agents'
  hash: sha256:0e4e8bf6d9cb724da07f95297d00f7077a224890c85346851d0d455eba93d529

schema:
status: generated
last_generated_at: "2026-08-21"
extracted_tokens: 4919
generated_pages:
  - .wikicommit/entity/en/TechArticle/scaling-managed-agents.md
  - .wikicommit/entity/en/SoftwareApplication/claude-managed-agents.md
  - .wikicommit/entity/en/DefinedTerm/meta-harness.md
  - .wikicommit/entity/en/DefinedTerm/agent-harness.md
  - .wikicommit/entity/en/DefinedTerm/compaction.md
  - .wikicommit/entity/en/DefinedTerm/indirect-prompt-injection.md
failed_pages: []
---

## Summary

Anthropic's account of the architecture behind Managed Agents, built on the premise that harnesses encode assumptions that go stale as models improve — illustrated by context resets added for one model becoming dead weight on the next. It virtualises an agent into three replaceable interfaces (session, harness, sandbox) on an operating-system analogy, making both container and harness disposable, moving credentials out of the sandbox's reach so a prompt injection cannot read them, and treating the durable session log as an interrogable context object rather than relying on irreversible compaction. Lazy container provisioning is reported to have cut p50 time-to-first-token by roughly 60% and p95 by over 90%.
