---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/building-c-compiler'
  hash: sha256:76ec31b147cb595b08d33f9b46ece5a385276d3165f3c8ca4ab62600055ab111

schema:
status: generated
last_generated_at: "2026-08-21"
extracted_tokens: 5256
generated_pages:
  - .wikicommit/entity/en/BlogPosting/building-a-c-compiler-with-parallel-claudes.md
  - .wikicommit/entity/en/Person/nicholas-carlini.md
  - .wikicommit/entity/en/DefinedTerm/agent-harness.md
  - .wikicommit/entity/en/DefinedTerm/multi-agent-orchestration.md
  - .wikicommit/entity/en/DefinedTerm/ralph.md
  - .wikicommit/entity/en/DefinedTerm/verification-bottleneck.md
  - .wikicommit/entity/en/DefinedTerm/agent-teams.md
failed_pages: []
---

## Summary

An Anthropic engineering report on tasking 16 parallel Claude instances with writing a Rust C compiler from scratch. Over nearly 2,000 Claude Code sessions and just under $20,000 in API costs, the agents produced a 100,000-line compiler that builds Linux 6.9 on x86, ARM and RISC-V. Its focus is harness design for long-running autonomous teams: a bash loop spawning fresh sessions, coordination through git lock files with no orchestrator, tests written for the model rather than the author (bounded output, greppable error lines, sampled fast runs against time blindness), and a known-good compiler used as an oracle to manufacture independent subtasks out of one giant one. The evaluation section is candid about the compiler's limits, and the post closes uneasy about deploying software nobody has personally verified.
