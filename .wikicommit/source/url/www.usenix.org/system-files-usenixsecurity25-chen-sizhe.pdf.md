---
source:
  type: url
  url: 'https://www.usenix.org/system/files/usenixsecurity25-chen-sizhe.pdf'
  hash: sha256:91f97972f9337ec68915889ea729157686ff67d4a51b175b55127f2e715de659
  license:

schema:
status: generated
last_generated_at: "2026-09-20"
extracted_tokens: 30554
generated_pages:
  - .wikicommit/entity/en/ScholarlyArticle/struq.md
  - .wikicommit/entity/en/DefinedTerm/structured-query.md
  - .wikicommit/entity/en/DefinedTerm/structured-instruction-tuning.md
  - .wikicommit/entity/en/DefinedTerm/completion-attack.md
failed_pages: []
---

## Summary

A USENIX Security 2025 paper from UC Berkeley proposing structured queries -- separating an LLM's prompt from its data into two channels -- as a defense against prompt injection, and StruQ, a system that implements them. StruQ combines a secure front-end that encodes a query using reserved delimiter tokens and recursively filters those tokens out of the user data, with a base LLM converted by structured instruction tuning to follow instructions only in the prompt portion of its input. Evaluated against at least 15 attack techniques on Llama-7B and Mistral-7B, it reduces every tested manual attack to under 2% success with little or no loss of AlpacaEval utility, and cuts Tree-of-Attacks-with-Pruning from 97% to 9% and Greedy Coordinate Gradient from 97% to 58% on Llama; the authors frame prompt injection as the latest instance of the control/data channel-mixing flaw behind SQL injection, XSS and command injection, and state the defense is not yet complete against optimization-based attacks.

## Generation Notes

- "Sizhe Chen": excluded, privacy -- one of the paper's four authors, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
- "Julien Piet": excluded, privacy -- one of the paper's four authors, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
- "Chawin Sitawarin": excluded, privacy -- one of the paper's four authors, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
- "David Wagner": excluded, privacy -- one of the paper's four authors, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
