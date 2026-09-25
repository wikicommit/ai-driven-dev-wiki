---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/infrastructure-noise'
  hash: sha256:9b90b3bbedd0a21cb782473b01e46d26c615e6e342bfbc0dc3d3f8087925a2c6
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 4473
generated_pages:
  - .wikicommit/entity/en/BlogPosting/quantifying-infrastructure-noise-in-agentic-coding-evals.md
  - .wikicommit/entity/en/DefinedTerm/infrastructure-noise.md
  - .wikicommit/entity/en/Dataset/terminal-bench.md
failed_pages: []
---

## Summary

Anthropic reports that infrastructure configuration alone can move scores on agentic coding benchmarks by several percentage points: running Terminal-Bench 2.0 under six resource configurations, the gap between the most- and least-resourced setups was 6 percentage points, and a smaller effect was also seen on SWE-bench. The post explains how container resource enforcement and other factors such as time limits act as confounders, and recommends that evals specify both a guaranteed allocation and a separate hard limit per task, and that leaderboard differences below 3 percentage points be treated with skepticism until configurations are documented and matched.

## Generation Notes

"Gian Segato": excluded (privacy) — the post's credited author, a living individual; no existing page.
