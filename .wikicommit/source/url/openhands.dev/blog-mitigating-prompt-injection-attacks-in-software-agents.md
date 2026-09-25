---
source:
  type: url
  url: 'https://openhands.dev/blog/mitigating-prompt-injection-attacks-in-software-agents'
  hash: sha256:c531528526e6141ec71ff79c2e5e157b6f4eed38552de696dcc4c7135b39d6ff
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 3112
generated_pages:
  - .wikicommit/entity/en/BlogPosting/mitigating-prompt-injection-attacks-in-software-agents.md
  - .wikicommit/entity/en/SoftwareApplication/openhands.md
failed_pages: []
---


## Summary

An OpenHands blog post (August 14, 2025) examines the prompt-injection risk faced by highly autonomous coding agents such as OpenHands, showing that strong models often refuse obviously malicious instructions but that this is only a soft, non-deterministic block. It compares the risk to existing developer habits such as `curl | bash` and `npm install`, and walks through mitigation strategies — confirmation mode, security analyzers, Docker sandboxing, and hard policies such as Kubernetes network policy and eBPF — concluding that the main advice is to stick to trusted sources.

## Generation Notes

"Robert Brennan": excluded (privacy) — named only as the post's author; entity-policy.md rules out pages about individuals a source names without making them its subject, and about living individuals.
