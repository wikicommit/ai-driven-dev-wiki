---
source:
  type: url
  url: 'https://blog.langchain.com/improving-deep-agents-with-harness-engineering/'
  hash: sha256:7628e7920b4c219963d45c07cb27a6039a14ef5a60f3939b0ccb424dd7481ddd
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 5056
generated_pages:
  - .wikicommit/entity/en/BlogPosting/improving-deep-agents-with-harness-engineering.md
  - .wikicommit/entity/en/DefinedTerm/agent-middleware.md
  - .wikicommit/entity/en/SoftwareApplication/deep-agents.md
  - .wikicommit/entity/en/Dataset/terminal-bench.md
  - .wikicommit/entity/en/DefinedTerm/reasoning-sandwich.md
  - .wikicommit/entity/en/DefinedTerm/doom-loop.md
  - .wikicommit/entity/en/DefinedTerm/verification-loop.md
  - .wikicommit/entity/en/DefinedTerm/ralph-loop.md
failed_pages: []
---


## Summary

A February 2026 LangChain blog post describing how the company moved its coding agent, deepagents-cli, from just outside the Top 30 to the Top 5 on Terminal Bench 2.0 — from 52.8% to 66.5% — by changing only the harness while keeping the model, gpt-5.2-codex, fixed. It describes an automated trace-analysis loop packaged as an Agent Skill, and the harness changes that helped: system-prompt guidance and a pre-completion checklist middleware that push the agent into a build-and-verify loop, injected context about the environment and time budget, a loop-detection middleware against "doom loops", and a "reasoning sandwich" that spends more reasoning on planning and verification than on implementation. It closes with practical takeaways, including tailoring a harness to each model.

## Generation Notes

- "Vivek Trivedy": excluded (privacy) — the post's author, a living individual named by the source without being its subject, per entity-policy.md; what he reports is attributed to him on the pages for the post, terms and tools instead.
