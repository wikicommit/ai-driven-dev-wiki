---
source:
  type: url
  url: 'https://github.com/liu00222/Open-Prompt-Injection'
  hash: sha256:895ba881a5e3affcbccc872b5e101c586ba2ff92c22fdd66c076d3bdf431138a
  license:

schema:
status: generated
last_generated_at: '2026-09-19'
extracted_tokens: 4497
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/open-prompt-injection.md
failed_pages: []
---

## Summary

The Open-Prompt-Injection repository, an open-source toolkit and benchmark for prompt injection attacks and defenses in LLM-integrated applications and agents. It works by pairing a target task with an injected task and measuring the attack-success value, with models, tasks, attackers, applications and evaluators assembled through factory functions and JSON config files, and a declarative experiment matrix driving the full experiment set from the associated paper. It also ships two defense components distributed as fine-tuned checkpoints -- DataSentinel for detecting injected prompts and PromptLocate for localizing and recovering them -- which the repository presents as composable into a detection-then-localization pipeline.
