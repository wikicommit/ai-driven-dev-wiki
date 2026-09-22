---
source:
  type: url
  url: 'https://techblog.zozo.com/entry/loop-engineering-prompt-tuning'
  hash: sha256:880fb71e74e5d9aa9b6c299e1c29e88f42a7f80015910db287c39b2a378226b4
  license:

schema:
status: partial
last_generated_at: "2026-09-22"
extracted_tokens: 10739
generated_pages:
  - .wikicommit/entity/en/BlogPosting/loop-engineering-prompt-tuning.md
  - .wikicommit/entity/en/DefinedTerm/loop-engineering.md
failed_pages: []
---


## Summary

A ZOZO data scientist describes replacing the manual prompt-tuning loop for a vision-language model — look at the failures, work out why, rewrite the prompt, re-evaluate, remember what helped — with a Claude Code skill (`/tune`) whose sub-agents each take one step of that human loop. The design's core idea is to treat the F1 score as a loss and the model's own stated reasoning as a gradient, using the reasoning to decide which direction to move the prompt; an ablation on one task found that withholding the reasoning produced a higher training score but a markedly worse test score, i.e. overfitting. Across three tasks with different schema structures the automated loop improved leaf F1 in every case, matched or slightly exceeded the hand-tuned baseline on the one task where a comparison existed, and cut the full evaluation cycle from about 3.5 weeks to about one week — figures the author flags as a single run rather than a repeated measurement.

## Generation Notes

- "大川" (schema:Person): excluded, `privacy` — the post's named author, a living individual, which `.wikicommit/entity-policy.md` rules out; named in the body text and as a plain-text `author` value instead.
