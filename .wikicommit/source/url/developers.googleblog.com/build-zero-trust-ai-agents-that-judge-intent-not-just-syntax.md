---
source:
  type: url
  url: 'https://developers.googleblog.com/build-zero-trust-ai-agents-that-judge-intent-not-just-syntax/'
  hash: sha256:d0187b744f61bdd8948c7e820262e3fe8ca76ef50a4f6f3fdec012eb9e39c3b8
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 5878
generated_pages:
  - .wikicommit/entity/en/BlogPosting/build-zero-trust-ai-agents-that-judge-intent.md
  - .wikicommit/entity/en/SoftwareApplication/model-armor.md
  - .wikicommit/entity/en/SoftwareApplication/semantic-governance-policies.md
failed_pages: []
---

## Summary

Part 2 of a Google for Developers series on zero-trust agents, which keeps the Part 1 customer-support refund agent built with Agent Development Kit and moves its security checks from build-time code into managed runtime governance on Gemini Enterprise Agent Platform. It describes three controls applied through Agent Gateway — Model Armor screening prompts and responses at the edge, Semantic Governance Policies judging each proposed tool call against user intent and natural-language business rules, and Agent Anomaly Detection flagging multi-turn behaviour such as a refund drained across many turns — and a closed-loop remediation in which a detected anomaly leads to a new policy that takes effect without redeploying the agent.

## Generation Notes

- "Eric Dong": excluded (privacy) — a named author of the source post; a living individual named by the source without being its subject, per entity-policy.md.
- "Shubham Saboo": excluded (privacy) — a named author of the source post; a living individual named by the source without being its subject, per entity-policy.md.
