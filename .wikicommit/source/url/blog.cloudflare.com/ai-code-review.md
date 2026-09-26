---
source:
  type: url
  url: 'https://blog.cloudflare.com/ai-code-review/'
  hash: sha256:3713b9e52fb6d7bc6997a3eb6390c9e942880583682e40e2101d03533bc6657b
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 18034
generated_pages:
  - .wikicommit/entity/en/BlogPosting/orchestrating-ai-code-review-at-scale.md
failed_pages: []
---

## Summary

An April 2026 Cloudflare blog post describing the company's internal CI-native AI code review system, built as an orchestration layer around the open-source OpenCode agent. Up to seven specialised reviewer agents (security, performance, code quality, documentation, release, AGENTS.md and internal-compliance) run as concurrent OpenCode sessions under a coordinator agent that deduplicates and judges their findings and posts one structured review; the post covers the plugin architecture, risk tiers, circuit breakers and model failback, a Workers-based control plane, and reports figures from its first 30 days across 5,169 repositories.

## Generation Notes

- "Ryan Skidmore" (the post's author): exclude_reason privacy — a living individual; entity-policy.md rules out pages about living individuals.
