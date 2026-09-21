---
source:
  type: url
  url: 'https://engineering.mercari.com/en/blog/entry/20251030-taming-agents-in-the-mercari-web-monorepo/'
  hash: sha256:2be25eae3259d1a99d5bcb659f731c2564ffe64e94c6bf0ad803148e7fb2a464
  license:

schema:
status: partial
last_generated_at: "2026-09-21"
extracted_tokens: 3884
generated_pages:
  - .wikicommit/entity/en/BlogPosting/taming-agents-in-the-mercari-web-monorepo.md
  - .wikicommit/entity/en/Organization/mercari.md
  - .wikicommit/entity/en/DefinedTerm/agents-md.md
failed_pages: []
---

## Summary

A Mercari Engineering post describing how the Web team replaced its diverging per-tool rule files — written separately for Cursor and Claude Code, with no process keeping them in sync — with a single `AGENTS.md` at the root of its monorepo. It records the format's history as the team encountered it: a singular `AGENT.md` RFC proposed by Sourcegraph through AmpCode, which became plural once OpenAI secured the agents.md domain, after which the team adopted it as its single source of truth and made `CLAUDE.md` and other rule files symlinks to it. The file works as an entrypoint linking to smaller topical documents on architecture, code style, authentication and testing, and the team runs an agent over a pull request's changeset to have the model itself propose edits to those rules.

## Generation Notes

- "Maximilien Mellen" (the post's author): excluded, `privacy` — the entity policy rules out pages about living individuals; named as the author of a source without being its subject.
