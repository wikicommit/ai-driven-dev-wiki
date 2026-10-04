---
source:
  type: url
  url: 'https://github.com/alecnielsen/adversarial-review'
  hash: sha256:b6388c19b88afabd80a5fbec468b2934e258bedaf755ba94f82d774704eb71a7
  license:
  lang: en

schema:
status: generated
last_generated_at: "2026-10-04"
extracted_tokens: 4180
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/adversarial-review.md
  - .wikicommit/entity/en/DefinedTerm/cross-model-review.md
failed_pages: []
---

## Summary

Adversarial Review is an experimental open-source shell tool that runs multi-agent code review with Claude and GPT Codex in an adversarial debate loop. The two agents review a target codebase independently, critique each other's findings, respond to those critiques, and Claude then synthesizes the debate and implements the fixes it judges valid, looping until both agents report no issues or a circuit breaker detects stagnation. The README cites multi-agent debate research as the basis for the approach and estimates up to about 21 API calls per review at the default of three iterations.
