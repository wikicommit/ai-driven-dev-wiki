---
source:
  type: url
  url: 'https://martinfowler.com/articles/are-harnesses-worth-the-cost.html'
  hash: sha256:3baedf6f6c5150f062e0a3c5f7a5c6d8a88fe3edce290137be55d057888a85dc
  license:
  lang: en

schema:
status: generated
last_generated_at: "2026-10-16"
extracted_tokens: 8382
generated_pages:
  - .wikicommit/entity/en/BlogPosting/are-harnesses-worth-the-cost.md
  - .wikicommit/entity/en/DefinedTerm/executable-attention.md
failed_pages: []
---

## Summary

This article in the Exploring Gen AI series on martinfowler.com reports an experiment comparing coding agents building the same backend-for-frontend API service with and without a behavioral harness of contract-driven guides and sensors, over 10 runs per model. The frontier GPT-6 Sol passed all 178 external acceptance checks in every run either way, so the harness only added tokens, time and cost, while the cost-optimized GPT-6 Luna succeeded in 3 of 10 unharnessed runs and all 10 harnessed ones at about 33% less cost per run than unharnessed Sol. The author concludes that model capability changes when sensors should run — continuously as "executable attention" for weaker models, or once as a final verification gate for frontier models — not whether independent verification is needed.

## Generation Notes

- "Naresh Jain": privacy — the article's author, a living individual named without being its subject; entity-policy.md rules this out.
