---
source:
  type: url
  url: 'https://www.anthropic.com/research/trustworthy-agents'
  hash: sha256:7b2800e6840e79dc817c3f2b89dba0aad5a79482b920ffc7c6ff72b1b9f967c9
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 4917
generated_pages:
  - .wikicommit/entity/en/BlogPosting/trustworthy-agents-in-practice.md
  - .wikicommit/entity/en/DefinedTerm/harness-engineering.md
failed_pages: []
---

## Summary

Anthropic's account of how its five trustworthy-agent principles become product decisions, organised around a decomposition of an agent into four components — the model, a harness of instructions and guardrails, the tools it can call, and the environment it runs in — each presented as both a source of capability and a point of oversight. Its corrective is that policy attention concentrates on the model while a well-trained model can still be exploited through a poorly configured harness, an overly permissive tool, or an exposed environment. It works through per-action permissions and Claude Code's Plan Mode as human-control mechanisms, training the model to pause rather than assume when intent is ambiguous, and layered prompt-injection defences, then names shared benchmarks, evidence sharing and open protocols as infrastructure no single company can supply.
