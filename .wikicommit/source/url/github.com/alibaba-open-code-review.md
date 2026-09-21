---
source:
  type: url
  url: 'https://github.com/alibaba/open-code-review'
  hash: sha256:b9e25b582bd7eea6db72fdab8f395f2c2a3a3d52275e5bb2239736035a7c6c88
  license: Apache-2.0

schema:
status: generated
last_generated_at: "2026-09-21"
extracted_tokens: 7734
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/open-code-review.md
  - .wikicommit/entity/en/Dataset/aacr-bench.md
  - .wikicommit/entity/en/DefinedTerm/agentic-code-review.md
failed_pages: []
---

## Summary
The repository page for Open Code Review, an Apache-2.0 AI code review CLI invoked as `ocr`, which the README says originated as Alibaba Group's internal review assistant and served tens of thousands of developers over two years before being open-sourced. Its stated design is a hybrid: deterministic engineering handles file selection, bundling into isolated sub-agent units, rule matching and comment positioning, while an LLM agent handles dynamic decisions and context retrieval — a response to three problems it attributes to general-purpose agents doing code review, namely incomplete coverage, position drift and unstable quality. It documents diff review, full-file scan and a delegation mode that uses the caller's own agent, plugins for several coding agents, CI integrations, and a benchmark, AACR-Bench, against which it reports higher precision and F1 at roughly a ninth of the tokens.
