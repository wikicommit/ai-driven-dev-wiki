---
source:
  type: url
  url: 'https://github.com/AsyncFuncAI/AsyncReview'
  hash: sha256:fe75d41284e3b16f547100098c199269e82a0d07655fa5e6c55e1989662c322e
  license: MIT

schema:
status: generated
last_generated_at: "2026-09-21"
extracted_tokens: 4233
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/asyncreview.md
  - .wikicommit/entity/en/DefinedTerm/agentic-code-review.md
failed_pages: []
---

## Summary
The repository page for AsyncReview, an open-source agentic code review tool for GitHub pull requests and issues, published under the MIT license. It describes itself as using Recursive Language Models to go beyond diff analysis: the agent reasons and plans, generates Python code, executes it in a sandbox alongside model queries, has its file-fetch and search calls served from the GitHub API, and repeats recursively. Its stated contrast with other review tools is full repository context against the diff alone, executed verification against static guessing, and grounded citations against invented library methods. It runs through `npx asyncreview` with a Gemini API key, and is also packaged as an installable skill for other coding agents.
