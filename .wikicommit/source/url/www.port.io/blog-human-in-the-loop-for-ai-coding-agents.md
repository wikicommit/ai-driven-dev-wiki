---
source:
  type: url
  url: 'https://www.port.io/blog/human-in-the-loop-for-ai-coding-agents'
  hash: sha256:766abcbeb6946c92580399d54cd8330c0edeb8fda6e8e61aefb36579d744524c
  license:

schema:
status: partial
last_generated_at: "2026-09-20"
extracted_tokens: 9541
generated_pages:
  - .wikicommit/entity/en/BlogPosting/do-you-really-need-a-human-in-every-loop.md
  - .wikicommit/entity/en/DefinedTerm/rule-based-gate.md
  - .wikicommit/entity/en/DefinedTerm/risk-based-gate.md
  - .wikicommit/entity/en/DefinedTerm/human-in-the-loop.md
  - .wikicommit/entity/en/SoftwareApplication/port.md
failed_pages: []
---

## Summary

A post on Port's blog arguing that a human is not needed in every loop, and that gating only code merges and pull requests -- the review teams already ran before agents existed -- breaks as soon as an agent acts in production. It distinguishes two kinds of guardrail that decide when a human is pulled in: rule-based gates, deterministic conditions written in advance that fire the same way every time, and risk-based gates, in which an agent scores the specific action against live context and a human is pulled in only above a set threshold. The test offered for choosing between them is whether the decision is a lookup or a judgment; both kinds are said to depend on the same connected view of an organisation's systems, which is the post's case for running both as native steps of one platform reading from Port's context lake.

## Generation Notes

- "Matar Peles": excluded, privacy -- the post's named author, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
