---
source:
  type: url
  url: 'https://simonwillison.net/2023/May/2/prompt-injection-explained/'
  hash: sha256:0d92bc59d6b47bea9a692f7ac853d8e13f2857879ab57db58c2e47b4e30fc1d3
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 5896
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/dual-llm-pattern.md
  - .wikicommit/entity/en/DefinedTerm/prompt-injection.md
failed_pages: []
---

## Summary

Simon Willison's annotated talk from a May 2023 LangChain webinar, introducing prompt injection as an attack on applications built on top of LLMs rather than on the models themselves. It argues that probabilistic, AI-based detection cannot reach the reliability security requires, and proposes the dual LLM pattern -- a privileged LLM that never sees untrusted content alongside a quarantined LLM that does -- as an imperfect mitigation.
