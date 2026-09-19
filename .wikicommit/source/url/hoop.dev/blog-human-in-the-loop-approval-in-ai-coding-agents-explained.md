---
source:
  type: url
  url: 'https://hoop.dev/blog/human-in-the-loop-approval-in-ai-coding-agents-explained'
  hash: sha256:d47e37ed6d4309cb36f68927dfc4477de6d95bb29a757d4457974ee26a438f58
  license:

schema:
status: partial
last_generated_at: "2026-09-19"
extracted_tokens: 2280
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/hoop-dev.md
  - .wikicommit/entity/en/DefinedTerm/human-in-the-loop.md
failed_pages: []
---

## Summary

A vendor blog post arguing that human-in-the-loop approval for AI coding agents belongs in the data path rather than in a post-hoc pull-request review. It contends that an agent authenticating directly against a Git server, registry or CI/CD orchestrator gives identity verification but no point at which policy can pause, inspect or require a human decision, so hallucinated secrets, CVE-bearing dependency updates and control-bypassing logic reach version control before anyone looks. Its proposed answer is a Layer 7 gateway that inspects each request at the protocol level, routes it to a reviewer where policy demands, forwards it only on consent, and records the session — the design the post's own product, hoop.dev, implements.

## Generation Notes

- "Coleman Nye": excluded (privacy) — the post's bylined author; a living individual and not the subject of the source, which entity-policy.md rules out.
