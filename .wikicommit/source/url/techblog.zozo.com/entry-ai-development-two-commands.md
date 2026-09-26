---
source:
  type: url
  url: 'https://techblog.zozo.com/entry/ai-development-two-commands'
  hash: sha256:58353a3fded13879de422c6b7cc6aff4012808394657a717d42726f5f81140df
  license:

schema:
status: generated
last_generated_at: "2026-09-22"
extracted_tokens: 12299
generated_pages:
  - .wikicommit/entity/en/BlogPosting/ai-driven-development-two-commands.md
  - .wikicommit/entity/en/Organization/zozo.md
  - .wikicommit/entity/en/DefinedTerm/critical-dialogue-review.md
failed_pages: []
---


## Summary

ZOZO's core-systems division standardized AI-driven development across the organization into two Claude Code commands, `/dev-init` and `/dev-resume`: the first builds a Confluence design document and a local progress table from a Jira ticket after parallel sub-agent investigation of the codebase, and the second reads that table against `git status`/`git diff` to re-establish where work stands. The post argues that what to delegate should be decided by the direction of information transformation — same-level and concrete-to-abstract conversions go to AI, while abstract-to-concrete judgment such as planning, requirement shaping and prioritization stays with humans. For quality-critical work it pairs Claude Code with Codex in a three-round critical dialogue in which Codex independently investigates the repository and criticizes, Claude Code adjudicates each finding as accepted, rejected or deferred, and Codex re-criticizes the rejections.

## Generation Notes

- "田中秀明" (schema:Person): excluded, `privacy` — the post's named author, a living individual, which `.wikicommit/entity-policy.md` rules out; named in the body text and as a plain-text `author` value instead.
