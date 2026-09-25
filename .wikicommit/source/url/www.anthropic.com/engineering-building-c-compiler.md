---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/building-c-compiler'
  hash: sha256:bb87bd35323bfc4ad526181ebcbea5616b7d93436bb9fcd985cf4d0f8de8a1c5
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 5272
generated_pages:
  - .wikicommit/entity/en/BlogPosting/building-a-c-compiler-with-a-team-of-parallel-claudes.md
  - .wikicommit/entity/en/SoftwareApplication/claudes-c-compiler.md
failed_pages: []
---

## Summary

An Anthropic engineering post (Feb 2026) describing an experiment in which 16 parallel Claude Opus 4.6 instances, run in an infinite loop with minimal human supervision, built a 100,000-line Rust-based C compiler able to build Linux 6.9 on x86, ARM and RISC-V over nearly 2,000 Claude Code sessions and about $20,000 in API costs. It focuses on lessons for designing harnesses for long-running autonomous agent teams: near-perfect tests, keeping output from polluting context, making parallelism easy (including using GCC as a known-good oracle), and specialized agent roles, and it lists the compiler's remaining limitations and the author's unease about deploying unverified software.

## Generation Notes

"Nicholas Carlini": exclude_reason privacy — the post's author, a living individual; entity-policy.md rules out pages about living individuals.
