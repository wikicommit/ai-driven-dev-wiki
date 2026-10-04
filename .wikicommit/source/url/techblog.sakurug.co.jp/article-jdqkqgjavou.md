---
source:
  type: url
  url: 'https://techblog.sakurug.co.jp/article/jdqkqgjavou/'
  hash: sha256:97ebf1fecfb6856f0d67a0b0c6c1466afc4956a0f246c1c7452db796e4a00c3e
  license:
  lang: ja

schema:
status: generated
last_generated_at: "2026-10-04"
extracted_tokens: 6812
generated_pages:
  - .wikicommit/entity/en/BlogPosting/experimental-verification-of-harness-engineering-with-claude-code.md
failed_pages: []
---

## Summary

An engineer at SAKURUG reports a small experiment in which Claude Code built the same customer-management web app under five cumulative harness conditions — prompt only, CLAUDE.md, a PostToolUse hook running lint/typecheck/test, a UI checklist plus a Stop completion gate, and a "Gate TDD" stop gate split into Red/Green/Refactor stages. All five final builds passed lint, typecheck, unit and e2e checks, so the differences showed up instead in how often the hooks and gates blocked the agent mid-run and in what the agent was allowed to count as finished; a rerun of the prompt-only condition produced a markedly different UI language, seed data and file layout. The author concludes that a harness raises the floor and fixes the completion criteria rather than raising the best-case output, and proposes an adoption order for individual developers while noting the small number of runs.

## Generation Notes

- "Akiyoshi" (the post's author): exclude_reason privacy — a named individual engineer who is not a public figure; entity-policy.md rules out pages about living or non-public individuals.
