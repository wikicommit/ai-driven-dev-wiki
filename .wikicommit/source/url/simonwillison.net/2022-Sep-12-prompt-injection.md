---
source:
  type: url
  url: 'https://simonwillison.net/2022/Sep/12/prompt-injection/'
  hash: sha256:2d2b741596804f79993a763d44b45e8307bef3e18b62aa98912d397b49a1fa23
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 3432
generated_pages:
  - .wikicommit/entity/en/BlogPosting/prompt-injection-attacks-against-gpt-3.md
  - .wikicommit/entity/en/DefinedTerm/prompt-injection.md
  - .wikicommit/entity/en/DefinedTerm/prompt-leaking.md
failed_pages: []
---

## Summary

A 12 September 2022 blog post proposing the name "prompt injection" for the class of attack in which untrusted input concatenated into an LLM prompt overrides the developer's instructions. It works through a translation-app example, demonstrates that defensive wording in the prompt does not stop the attack, shows the same technique leaking the system prompt, and argues by analogy with SQL injection that the fix would be parameterized prompts — a proposal a later update on the same page describes as extremely difficult if not impossible on current architectures.

## Generation Notes

- "Simon Willison": excluded, privacy — the post's author, a living public figure; entity-policy.md rules out pages about living individuals, and his contribution is recorded in the body text of the pages he is named on instead.
- "Riley Goodside": excluded, privacy — a living individual whose examples the post builds on; same policy.
