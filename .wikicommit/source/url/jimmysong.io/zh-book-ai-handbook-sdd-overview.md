---
source:
  type: url
  url: 'https://jimmysong.io/zh/book/ai-handbook/sdd/overview/'
  hash: sha256:946cf421ab8284921cee80b48fc236a89feb6dfd5c4a90f01ae072227495be73
  license:

schema:
status: generated
extracted_tokens: 5266
last_generated_at: "2026-09-21"
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/spec-driven-development.md
  - .wikicommit/entity/en/DefinedTerm/vibe-coding.md
  - .wikicommit/entity/en/SoftwareApplication/kiro.md
  - .wikicommit/entity/en/SoftwareApplication/github-spec-kit.md
  - .wikicommit/entity/en/SoftwareApplication/tessl.md
  - .wikicommit/entity/en/SoftwareApplication/agentscript.md
  - .wikicommit/entity/en/SoftwareApplication/qoder.md
failed_pages: []
---

## Summary

A chapter of Jimmy Song's online handbook 智能体构建指南 (Agent Builder's Guide) introducing spec-driven development as the successor to vibe coding. It argues AI programming is a shift of the whole development paradigm rather than a change in how code is typed, proposes a three-layer protocol stack (MCP between agent and tools, A2A between agents, AG-UI between user and agent), names five core capabilities for AI across the SDLC, and sets accuracy targets — at least 90% of generated code compiling and running, at least 85% passing automated tests, at most 10% needing manual repair — below which rework costs exceed the productivity gain. It then defines SDD as treating a structured specification as the single source of truth that drives design, implementation, testing and deployment, describes a Specify → Plan → Tasks → Implement → Deploy loop with automated verification acting as the oracle, and surveys eight representative tools and projects.

## Generation Notes

- "Jimmy Song" (the handbook's author): excluded, privacy — a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. Not a relevance judgment. No page exists for this entity.
- "OpenHands", "CodePlan", "LangChain Expression Language (LCEL)": not extracted — each is one entry in this chapter's list of representative projects, and the facts it states about them are already held by their existing pages from sources that treat them as their own subject.
- This chapter is a section of a continuously-updated online handbook rather than a dated single-instance work, so it was not treated as a source-as-entity (see `TechArticle.md`'s granularity rule on living resources).
