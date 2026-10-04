---
source:
  type: url
  url: 'https://github.com/FlorianBruniaux/claude-code-ultimate-guide/blob/main/guide/workflows/iterative-refinement.md'
  hash: sha256:76f1517fd4fb3d45eeeac738cd655ba37364639f67c145dd11149406e32e52f4
  license:
  lang: en

schema:
status: generated
last_generated_at: "2026-10-04"
extracted_tokens: 7842
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/iterative-refinement.md
  - .wikicommit/entity/en/DefinedTerm/review-auto-correction-loop.md
failed_pages: []
---

## Summary

A workflow chapter of the Claude Code Ultimate Guide repository on GitHub that presents iterative refinement — prompt, evaluate the output, give specific feedback, repeat — as the core loop of AI-assisted development. It covers effective and ineffective feedback patterns, autonomous loops with explicit completion criteria and iteration limits, how to support the loop with Claude Code's task tool, hooks, /compact and checkpoints, a 3–7 iteration pattern for script generation, and anti-patterns such as a moving target, a perfectionism loop and lost context. It also describes a bounded review auto-correction loop (review, fix, re-review within a fixed budget, with acceptance requiring evidence) and community patterns built on the loop, including a test-at-a-time Ralph loop, Stop-hook verification and a structured escalation path.
