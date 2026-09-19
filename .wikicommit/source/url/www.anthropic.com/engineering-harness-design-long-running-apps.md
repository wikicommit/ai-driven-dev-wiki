---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/harness-design-long-running-apps'
  hash: sha256:47a08ad7125c953a6a359d169a11e61245c1d5329e47cb7057f496aaaef42b2a
  license:

schema:
status: partial
last_generated_at: "2026-09-19"
extracted_tokens: 10316
generated_pages:
  - .wikicommit/entity/en/BlogPosting/harness-design-for-long-running-application-development.md
  - .wikicommit/entity/en/DefinedTerm/context-anxiety.md
  - .wikicommit/entity/en/DefinedTerm/context-reset.md
  - .wikicommit/entity/en/DefinedTerm/harness-engineering.md
  - .wikicommit/entity/en/DefinedTerm/compaction.md
failed_pages: []
---

## Summary

An Anthropic Labs engineer's account of harness design for two problems he treats as connected: getting Claude to produce high-quality frontend designs, and getting it to build complete applications without human intervention. Taking the generator/discriminator split of GANs as inspiration, he pairs a generator agent with a separately tuned, skeptical evaluator — first for frontend design, graded against four written criteria with the evaluator driving the live page through Playwright, then for full-stack development as a three-agent planner/generator/evaluator architecture with per-sprint contracts. The later half reports taking that architecture apart again as Opus 4.5 and 4.6 landed, dropping context resets and then the sprint construct, and gives duration and cost figures for a retro game maker (6 hours, $200, against a 20-minute $9 solo run) and a browser DAW (3h50, $124.70).

## Generation Notes

- "Prithvi Rajasekaran": excluded (privacy) — the named author of the source post, a living individual named by the source without being its subject, per entity-policy.md. The colleagues listed in the post's acknowledgements are a contributor roster and were not treated as entity candidates.
