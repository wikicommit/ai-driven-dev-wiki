---
source:
  type: url
  url: 'https://martinfowler.com/articles/exploring-gen-ai/ccmenu-quality.html'
  hash: sha256:7ea8a1ed00a8a82a1cd5c918dc9ccc8a4e1c4ff443010387ad6a0351210ba291
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 4106
generated_pages:
  - .wikicommit/entity/en/BlogPosting/assessing-internal-quality-while-coding-with-an-agent.md
  - .wikicommit/entity/en/SoftwareApplication/windsurf.md
failed_pages: []
---

## Summary

In this January 2026 "Exploring Gen AI" article, Erik Doernenburg uses coding agents (Windsurf with Sonnet 3.5, later Claude Code with Sonnet 4.5) to add GitLab support to CCMenu, a Swift Mac application, and examines the internal quality of the generated code rather than only whether it works. He describes a series of subtle problems — a wrongly non-optional token parameter patched by an unidiomatic "vibe fix", an unnecessary cache, logic for a non-existent problem, and duplicated URL construction — and concludes that without careful oversight agents tend to introduce technical debt, while finding Claude Code with Sonnet 4.5 good enough to use regularly.

## Generation Notes

- "Erik Doernenburg": excluded (privacy) — the article's author, a living individual named by the source without being its subject, per entity-policy.md.
- "CCMenu": excluded (theme_mismatch) — a Mac application for monitoring CI/CD build status that serves only as the codebase for the experiment; the application itself is not about AI-driven development.
