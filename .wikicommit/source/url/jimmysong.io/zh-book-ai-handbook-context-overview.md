---
source:
  type: url
  url: 'https://jimmysong.io/zh/book/ai-handbook/context/overview/'
  hash: sha256:f8e2752a1acfb50932f79278c2d01a48144d0a2169965cfa644161eb58799c23
  license:

schema:
status: generated
extracted_tokens: 4738
last_generated_at: "2026-09-21"
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/context-engineering.md
failed_pages: []
---

## Summary

A draft chapter of Jimmy Song's 智能体构建指南 on context engineering, which opens with a conceptual correction it treats as prerequisite to the rest: a Session is the complete, persisted interaction record whose goal is to lose nothing, while a Context is the payload constructed dynamically before each inference whose goal is to carry only what is relevant. It argues that conflating the two produces two engineering consequences — quality degradation, because irrelevant information acts as noise rather than as background, and uncontrolled cost, because a session grows without bound while the context window has a hard limit — and therefore frames the practice not as giving the model more but as building a Context Construction Pipeline that filters, compresses, reorders and validates. The remainder treats agents, query augmentation, retrieval, chunking, memory tiers and tools/MCP as components of that one pipeline.

## Generation Notes

- "Chunking", "Query Augmentation", "Retrieval", "Memory tiers": excluded, theme_mismatch — document-preparation and retrieval techniques for RAG systems in general, not practices of AI-driven software development. The chapter's chunk-size guidance is given for legal, medical and report corpora rather than for code. No pages exist for these entities.
- "Jimmy Song" (the handbook's author): excluded, privacy — a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
- This chapter is a section of a continuously-updated online handbook and is marked 草稿 (draft), so it was not treated as a source-as-entity.
