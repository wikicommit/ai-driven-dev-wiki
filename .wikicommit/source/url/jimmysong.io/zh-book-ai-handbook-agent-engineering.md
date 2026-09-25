---
source:
  type: url
  url: 'https://jimmysong.io/zh/book/ai-handbook/agent/engineering/'
  hash: sha256:ba3ef8f424b5b76f1af59a9b3a243e05ffacad7327edcda8e2f9e42bc81e3099
  license:

schema:
status: partial
last_generated_at: "2026-09-25"
extracted_tokens: 4315
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/agent-systems-engineering.md
  - .wikicommit/entity/en/DefinedTerm/compositional-reliability.md
failed_pages: []
---

## Summary

A draft chapter of Jimmy Song's online handbook 智能体构建指南 arguing that LLM-based agents must move from merely running to being reproducible, extensible, observable and maintainable through systems engineering rather than prompt tweaking. It describes three layers of complexity (runnability, reproducibility, evolvability), shows how per-call uncertainty compounds across many LLM calls (90% per call gives about 35% over 10 calls and 12% over 20), and prescribes replay, version tracking, monitoring metrics and checkpoint-based error recovery. It closes with a five-stage growth model, a table of agent design patterns and a layered engineering roadmap, concluding that an agent's future lies in being more reliable rather than smarter.

## Generation Notes

- "Jimmy Song" (the handbook's author): excluded, privacy — a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
- This chapter is a section of a continuously-updated online handbook and is marked 草稿 (draft), so it was not treated as a source-as-entity.
- "LangChain", "LangGraph", "LangSmith", "Flowise", "ReAct", "CodeAct": not extracted — each is named only in the chapter's lists and tables, with no independent facts stated; they are linked from the Agent Systems Engineering page where existing pages exist.
