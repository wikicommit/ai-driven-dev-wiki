---
source:
  type: url
  url: 'https://simonwillison.net/2024/Mar/5/prompt-injection-jailbreaking/'
  hash: sha256:03253e283263bfa4feaf0bb8e37840fdfebd27239d9b8c6a1b186cf5bc19d34a
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 2674
generated_pages:
  - .wikicommit/entity/en/BlogPosting/prompt-injection-and-jailbreaking-are-not-the-same-thing.md
  - .wikicommit/entity/en/DefinedTerm/jailbreaking.md
failed_pages: []
---

## Summary

Simon Willison's March 2024 argument that prompt injection and jailbreaking are distinct attack classes that are routinely conflated. Prompt injection depends on concatenating untrusted input with a trusted developer prompt and targets applications, while jailbreaking targets the safety filters built into the models themselves; he warns that a detection system trained on jailbreaks will not stop an application-specific injection, and reflects that a coined term needs ongoing maintenance.
