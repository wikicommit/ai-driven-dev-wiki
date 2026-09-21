---
source:
  type: url
  url: 'https://jimmysong.io/zh/book/ai-handbook/agent/multi-agent/'
  hash: sha256:644e8c22de6fd778cefa3c3c44647eee3beb025a3fb81617e0411c473018e2c9
  license:

schema:
status: generated
extracted_tokens: 5800
last_generated_at: "2026-09-21"
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/llm-based-multi-agent-system.md
  - .wikicommit/entity/en/DefinedTerm/agent2agent-protocol.md
  - .wikicommit/entity/en/SoftwareApplication/langgraph.md
  - .wikicommit/entity/en/SoftwareApplication/crewai.md
  - .wikicommit/entity/en/SoftwareApplication/autogen.md
  - .wikicommit/entity/en/SoftwareApplication/agno.md
  - .wikicommit/entity/en/SoftwareApplication/mastra.md
  - .wikicommit/entity/en/SoftwareApplication/agent-development-kit.md
  - .wikicommit/entity/en/SoftwareApplication/strands-agents.md
  - .wikicommit/entity/en/SoftwareApplication/microsoft-agent-framework.md
failed_pages: []
---

## Summary

A draft chapter of Jimmy Song's 智能体构建指南 on multi-agent collaboration, written as an operations handbook rather than a concept survey. It covers role separation (Planner, Worker, Reviewer, Orchestrator), consensus and arbitration (majority voting, confidence-weighted voting, trust-value routing), task-plan merging and conflict resolution, cross-agent tracing through shared state machines and trace IDs, and resource containment through call quotas, budget monitoring, retry limits and circuit breaking. It then compares six coordination frameworks — LangGraph, CrewAI, Agno, Mastra, Google ADK and AWS Strands — against centralized, hierarchical, hybrid and decentralized architectures, argues that none of them solves selective semantic context transfer between agents, and records a 2026 consolidation of the ecosystem in which MCP connects tools and A2A connects agents.

## Generation Notes

- "Supervisor Pattern", "Majority Voting", "Confidence-weighted Voting", "Trace ID", "Execution Budget": not extracted as separate entities — the chapter lists them under 关联术语 and explains each only as part of its account of multi-agent collaboration, so they are recorded on that page rather than given pages of their own.
- "OpenAI Agents SDK", "OpenHands": not extracted — each appears only as one row of the chapter's 2026 framework summary table, with no facts of its own stated.
- "Jimmy Song" (the handbook's author): excluded, privacy — a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
- This chapter is a section of a continuously-updated online handbook and is marked 草稿 (draft), so it was not treated as a source-as-entity.
