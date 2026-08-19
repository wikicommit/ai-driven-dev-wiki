---
source:
  type: url
  url: 'https://ghuntley.com/ralph/'
  hash: sha256:9836ee3ee0773613f370a27796b1e456199be38681f73a47b974e210dd356317

schema:
status: generated
last_generated_at: "2026-08-19"
extracted_tokens: 10543
generated_pages:
  - .wikicommit/entity/en/BlogPosting/ralph-wiggum-as-a-software-engineer.md
  - .wikicommit/entity/en/DefinedTerm/backpressure.md
  - .wikicommit/entity/en/DefinedTerm/multi-agent-orchestration.md
  - .wikicommit/entity/en/DefinedTerm/ralph.md
  - .wikicommit/entity/en/DefinedTerm/subagents.md
  - .wikicommit/entity/en/Person/geoffrey-huntley.md
failed_pages: []
---
## Summary

Geoffrey Huntley's post of 14 July 2025 setting out Ralph, a technique for running a coding agent in an unattended shell loop that feeds it the same prompt file every iteration, doing one task per loop. It gives the operating rules he derived while building a programming language and compiler with it — deterministic stack allocation each loop, subagents dispatched by the primary context window acting as a scheduler, backpressure as the verification phase, and tuning by adding instructions to the prompt rather than changing tools.
