---
source:
  type: url
  url: 'https://developers.openai.com/blog/eval-skills/'
  hash: sha256:51ec56a57b97282cac1e2ff8d92b29b354928a62291f581e9daa7e0697a3597d
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 12307
generated_pages:
  - .wikicommit/entity/en/BlogPosting/testing-agent-skills-systematically-with-evals.md
  - .wikicommit/entity/en/DefinedTerm/behavioral-evaluation.md
failed_pages: []
---


## Summary

A January 2026 post on OpenAI's developer blog sets out a pattern for testing Codex agent skills with evals rather than judging changes by feel. It recommends defining measurable success first (outcome, process, style and efficiency goals), then running a small set of 10–20 prompts — including negative controls that should not trigger the skill — through `codex exec --json`, scoring the recorded event trace with deterministic checks, and adding a model-assisted, rubric-based style check constrained by an output schema, growing the prompt set from real failures over time.

## Generation Notes

- "Dominik Kundel": excluded (privacy) — a named author of the source post; a living individual named by the source without being its subject, per entity-policy.md.
- "Gabriel Chua": excluded (privacy) — a named author of the source post; a living individual named by the source without being its subject, per entity-policy.md.
