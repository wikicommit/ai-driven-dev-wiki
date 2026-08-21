---
source:
  type: url
  url: 'https://sourcegraph.com/blog/agentic-coding'
  hash: sha256:0555e00c666984a838cc1b7db05eafdeedd950e02544b3d77491c6bc5a918d1c

schema:
status: partial
last_generated_at: "2026-08-21"
extracted_tokens: 4974
generated_pages:
  - .wikicommit/entity/en/BlogPosting/agentic-coding-in-2026-a-practical-guide-for-big-code.md
  - .wikicommit/entity/en/DefinedTerm/eighty-percent-problem.md
  - .wikicommit/entity/en/Dataset/codescalebench.md
  - .wikicommit/entity/en/Organization/sourcegraph.md
  - .wikicommit/entity/en/DefinedTerm/agentic-coding.md
failed_pages: []
---


## Summary

A Sourcegraph guide of 21 May 2026 by Matt Tanner for senior engineers running coding agents on large codebases. Its substantive contribution is the 80% problem — its name for agents reliably completing the visible portion of a task and silently missing what lies outside their context window — which became its own page, together with the argument that this is a context-infrastructure rather than a model limitation. The agentic coding page gained the guide's operational definition, its seven-step loop, and its sharpest available statement of the boundary against vibe coding ("who owns correctness").

Excluded as unrelated to the configured theme:
- "Sourcegraph Deep Search", "Sourcegraph Code Insights", "Sourcegraph Agentic Migrations", "Amp" (theme_mismatch): the publisher's own product surfaces, catalogued in the guide's closing sections as the remedy for the problem it describes. The configured theme excludes vendor product marketing; the products are noted in prose on the Sourcegraph organisation page rather than becoming pages of their own.

The methodology content ahead of the product pitch was taken in full. The organisation page and the CodeScaleBench benchmark page are shared with the companion context-engineering post from the same author.

Re-checked on 2026-08-21 (content unchanged, cache hit) as a dedicated coverage comparison. One uncovered item was found and added to the guide's page: its cost model for agentic coding, decomposing spend into model inference, retrieval and indexing infrastructure, and human review time, with inference the most volatile line because agents make many calls per task during the refine loop, and context quality named as the driver of the variance teams report. The status stays `partial` because of the theme exclusions above.
