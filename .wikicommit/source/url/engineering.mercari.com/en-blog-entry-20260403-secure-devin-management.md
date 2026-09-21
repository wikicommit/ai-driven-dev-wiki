---
source:
  type: url
  url: 'https://engineering.mercari.com/en/blog/entry/20260403-secure-devin-management/'
  hash: sha256:bc915a8ef4d5b712d51f417e33760f31692d9d15436252e3de284e4235644d53
  license:

schema:
status: partial
last_generated_at: "2026-09-21"
extracted_tokens: 5342
generated_pages:
  - .wikicommit/entity/en/BlogPosting/enabling-ai-usage-at-mercari-with-secure-devin-management.md
  - .wikicommit/entity/en/SoftwareApplication/devin.md
  - .wikicommit/entity/en/Organization/mercari.md
failed_pages: []
---

## Summary

A Mercari Engineering post from the AI Security team on operating Devin's Enterprise plan across more than ten Organizations, where member assignment, per-Organization credentials and unexpiring API keys had all been manual. It describes six automations built on Devin's v3 and v2 APIs in Go and GitHub Actions: a custom Terraform provider managing Organizations, members, ACU limits and Devin Knowledge declaratively; bulk secret rotation from Google Cloud Secret Manager; service-account key rotation under an expiry-hours compensating control; audit-log forwarding into an in-house monitoring platform; periodic invalidation of user-issued API keys; and short-interval recreation of the keys internal agents use to reach Devin Wiki through Devin MCP.

## Generation Notes

- "Hiroki Akamatsu" (the post's author): excluded, `privacy` — the entity policy rules out pages about living individuals; named as the author of a source without being its subject.
