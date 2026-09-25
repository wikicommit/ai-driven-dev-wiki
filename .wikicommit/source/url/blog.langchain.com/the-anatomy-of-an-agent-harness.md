---
source:
  type: url
  url: 'https://blog.langchain.com/the-anatomy-of-an-agent-harness/'
  hash: sha256:71cffd4adc7b81b7dd5f981d26af2bebcee592b2751a882ea95bb833fa2d022e
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 5723
generated_pages:
  - .wikicommit/entity/en/BlogPosting/the-anatomy-of-an-agent-harness.md
  - .wikicommit/entity/en/DefinedTerm/agent-harness.md
  - .wikicommit/entity/en/DefinedTerm/context-rot.md
  - .wikicommit/entity/en/DefinedTerm/ralph-loop.md
  - .wikicommit/entity/en/DefinedTerm/tool-call-offloading.md
failed_pages: []
---


## Summary

A March 2026 LangChain blog post that defines an agent harness as every piece of code, configuration and execution logic that is not the model itself — "Agent = Model + Harness" — and derives a harness's core components by working backwards from what a model cannot do out of the box. It covers filesystems and git for durable state, bash and code execution as a general-purpose tool, sandboxes with default tooling for safe execution and self-verification, memory files and web search for knowledge beyond the weights, compaction, tool-call offloading and Skills against context rot, and Ralph Loops, planning and self-verification for long-horizon work. It closes on the co-evolution of model post-training and harness design, arguing that the best harness for a task is not necessarily the one a model was trained with.

## Generation Notes

- "Vivek Trivedy": excluded (privacy) — the post's author, a living individual named by the source without being its subject, per entity-policy.md; what he argues is attributed to him on the pages for the post and terms instead.
