---
source:
  type: url
  url: 'https://developers.googleblog.com/a-guide-to-fine-tuning-functiongemma/'
  hash: sha256:04fc7d0d05af957da0b49f748286546b544a53c9541dea52a2541b70e8f5dda3
  license:

schema:
status: generated
last_generated_at: "2026-09-24"
extracted_tokens: 3260
generated_pages:
  - .wikicommit/entity/en/BlogPosting/a-guide-to-fine-tuning-functiongemma.md
failed_pages: []
---
## Summary

A Google DeepMind tutorial post on fine-tuning FunctionGemma, a function-calling variant of Gemma 3 270M, so that it resolves tool-selection ambiguity according to an organization's own policy — in its case study, routing internal-policy questions to a knowledge-base search tool rather than to Google search. It walks through supervised fine-tuning with Hugging Face TRL, warns that an unshuffled train-test split of category-sorted data can leave the model trained on only one tool, and introduces the FunctionGemma Tuning Lab, a no-code Hugging Face Spaces demo for the same process.
