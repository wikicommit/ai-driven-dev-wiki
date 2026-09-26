---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents'
  hash: sha256:26ce4c203cbb030f31253f1eb174b46b2c0203c9b44576aa4654b89b4d7be777
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 4878
generated_pages:
  - .wikicommit/entity/en/BlogPosting/effective-harnesses-for-long-running-agents.md
  - .wikicommit/entity/en/DefinedTerm/initializer-agent.md
  - .wikicommit/entity/en/DefinedTerm/long-running-agent.md
  - .wikicommit/entity/en/DefinedTerm/compaction.md
  - .wikicommit/entity/en/DefinedTerm/harness-engineering.md
  - .wikicommit/entity/en/SoftwareApplication/claude-agent-sdk.md
failed_pages: []
---

## Summary

An engineering post on getting an agent to make consistent progress across many context windows, where each session begins with no memory of the last. It reports two observed failure modes — the agent trying to one-shot the whole app and running out of context mid-feature, and a later session seeing existing progress and declaring the job done — and describes a two-part answer: an initializer agent that sets up the environment once (an `init.sh` script, a progress log, an initial commit, and a JSON feature list of every requirement marked failing), and a coding agent that each session reads that state, advances one feature, verifies it end-to-end with browser automation, and leaves the repository clean and committed.

## Generation Notes

- "Justin Young" and the individuals named in the acknowledgements: excluded, privacy — the post's author and contributors, living individuals, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No pages exist for these entities.
