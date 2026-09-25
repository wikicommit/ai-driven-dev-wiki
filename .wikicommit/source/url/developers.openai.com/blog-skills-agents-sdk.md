---
source:
  type: url
  url: 'https://developers.openai.com/blog/skills-agents-sdk'
  hash: sha256:92c2e202346410459520ce7bdf01b1af912f1f79aefe1e1c9bff2e809b5368a4
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 14433
generated_pages:
  - .wikicommit/entity/en/BlogPosting/using-skills-to-accelerate-oss-maintenance.md
  - .wikicommit/entity/en/SoftwareApplication/codex-github-action.md
failed_pages: []
---

## Summary

An OpenAI developer blog post describing how the maintainers of the OpenAI Agents SDK's Python and TypeScript repositories use Codex with repo-local skills, AGENTS.md and the Codex GitHub Action to turn recurring work — verification, docs sync, example runs, release review and PR handoff — into repeatable workflows, alongside a rise in merged PRs over the period described. Its practical lessons are to make skill use mandatory through short if/then rules in AGENTS.md, to treat a skill's description field as routing metadata, to put deterministic shell work in scripts while leaving interpretation to the model, and to keep human review for decisions between several valid options rather than for routine correctness.

## Generation Notes

- "Kazuhiro Sera": excluded (privacy) — the named author of the source post; a living individual named by the source without being its subject, per entity-policy.md.
