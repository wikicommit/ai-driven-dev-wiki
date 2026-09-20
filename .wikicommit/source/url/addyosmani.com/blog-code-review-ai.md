---
source:
  type: url
  url: 'https://addyosmani.com/blog/code-review-ai/'
  hash: sha256:e678c0f13766adc73b4d03c644a747b3d135be132242e1875d32cfbf38e936be
  license:

schema:
status: generated
last_generated_at: "2026-09-20"
extracted_tokens: 3935
generated_pages:
  - .wikicommit/entity/en/BlogPosting/ai-writes-code-faster-your-job-is-still-to-prove-it-works.md
  - .wikicommit/entity/en/DefinedTerm/pr-contract.md
failed_pages: []
---

## Summary

A January 2026 post by Addy Osmani arguing that AI did not kill code review but made the burden of proof explicit: a pull request without evidence that it works moves work downstream rather than shipping faster, so changes should ship with proof (tests, manual verification) and review should be spent on risk, intent and accountability. It contrasts solo developers shipping at "inference speed" behind strong automated test suites with teams that use AI review bots for a first pass but keep human sign-off, and argues the practical team problem is volume outrunning verification capacity rather than missed style issues. It sets out a four-item PR Contract (what/why, proof it works, risk and AI role, review focus) plus principles for dividing first-pass AI review from human review of security, duplication and maintainability.
