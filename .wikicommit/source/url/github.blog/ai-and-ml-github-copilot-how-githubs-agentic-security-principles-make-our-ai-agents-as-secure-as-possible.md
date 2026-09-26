---
source:
  type: url
  url: 'https://github.blog/ai-and-ml/github-copilot/how-githubs-agentic-security-principles-make-our-ai-agents-as-secure-as-possible/'
  hash: sha256:4d060e60394d3bb5b60078b4750eb96bd19bc3ec2961726e242bb6398e575bee
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 8016
generated_pages:
  - .wikicommit/entity/en/BlogPosting/githubs-agentic-security-principles.md
failed_pages: []
---

## Summary

GitHub's account of the security guidelines behind its hosted AI agents, written from the premise that the more agentic a product is the greater the chance and impact of it going off its guardrails, losing alignment or being manipulated. It names three risk classes — data exfiltration, impersonation and action attribution, and prompt injection — and six rules applied across GitHub's hosted agentic products: make all context visible and strip hidden Unicode or HTML directives; firewall the agent's network access; withhold sensitive information such as CI secrets and revoke tokens after a session; prevent irreversible state changes without a human in the loop; attribute actions to both initiator and agent; and gather context only from users with write access.

## Generation Notes

- "Rahul Zhade": excluded (privacy) — the named author of the source post; a non-public-figure individual named by the source without being its subject, per entity-policy.md.
