---
source:
  type: url
  url: 'https://docs.anthropic.com/en/docs/test-and-evaluate/strengthen-guardrails/mitigate-jailbreaks'
  hash: sha256:cccb2171881ac7e3fdad07195764b42fff863153b2b262af3fd66a5ff5c7779c
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 4348
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/jailbreaking.md
  - .wikicommit/entity/en/DefinedTerm/indirect-prompt-injection.md
failed_pages: []
---

## Summary

Anthropic's platform documentation on defending Claude-based applications against jailbreaks and prompt injection. It separates two threat models -- jailbreaks and direct prompt injection, where the application's own user is the adversary, and indirect prompt injection, where untrusted third-party content reaches the model through tool results -- and gives concrete mitigations for each, including harmlessness screens, JSON-encoded untrusted content, and injection screening of tool output.
