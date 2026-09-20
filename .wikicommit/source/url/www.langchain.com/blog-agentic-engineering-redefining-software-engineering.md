---
source:
  type: url
  url: 'https://www.langchain.com/blog/agentic-engineering-redefining-software-engineering'
  hash: sha256:5799c63ef9d6f2d03dd3a460a970c8adca733f9ac55a80be400ce5edb58db2fe
  license:

schema:
status: partial
last_generated_at: "2026-09-20"
extracted_tokens: 5936
generated_pages:
  - .wikicommit/entity/en/BlogPosting/agentic-engineering-swarms-of-ai-agents.md
  - .wikicommit/entity/en/DefinedTerm/agentic-engineering.md
  - .wikicommit/entity/en/SoftwareApplication/langgraph.md
  - .wikicommit/entity/en/DefinedTerm/agent2agent-protocol.md
failed_pages: []
---

## Summary

A guest post by two Cisco engineers on the LangChain blog proposing agentic engineering as a multi-agent coordination model in which AI agents act as digital team members: loosely coupled Worker Agents that plan and execute within defined boundaries, and a Leader Agent that supplies a shared prompt and workflow library, a common tool gateway, long-term memory for the swarm, and global observability. The reference implementation uses LangGraph for orchestration, LangSmith for execution traces and LangMem for long-term state, with worker agents communicating over the A2A protocol and reaching non-A2A agents through an MCP wrapper. A pilot of 20+ debugging workflows reported a 93% reduction in time-to-root-cause and 15+ development workflows a 65% reduction in execution time, with the authors attributing the gains to compressed downstream testing rather than faster code generation.

## Generation Notes

- "Renuka Kumar": excluded, privacy -- one of the post's two named authors, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
- "Prashanth Ramagopal": excluded, privacy -- one of the post's two named authors, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
