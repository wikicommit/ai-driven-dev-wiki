---
source:
  type: url
  url: 'https://www.tbench.ai/'
  hash: sha256:3b3245f22ca4f91bbcd20c983f4ece864010227d87020943e7acafc6e2591bc5
  license:

schema:
status: generated
last_generated_at: "2026-09-22"
extracted_tokens: 254
generated_pages:
  - .wikicommit/entity/en/Dataset/terminal-bench.md
failed_pages: []
---

## Summary

Terminal-Bench is a benchmark, at version 4.0 at the time of this fetch, that its own site describes as measuring and evolving with the frontier of agent work. The landing page publishes a leaderboard ranking model and agent pairings by resolution rate alongside cost and token figures, with whiskers spanning a 95% confidence interval, and points to a task list hosted on the Harbor framework's dataset hub. It names Stanford, Harbor and the Laude Institute as its hosts.

## Generation Notes

- "Terminal-Bench": coverage_gap — the source states the benchmark's version (4.0) and carries a canary GUID marking it as material that should not enter training corpora, but Dataset.md's `properties:` block has no field for either, so both are recorded in the page body only.
