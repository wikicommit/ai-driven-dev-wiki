---
source:
  type: url
  url: 'https://jimmysong.io/zh/book/ai-native-whitepaper/03-development-frameworks/'
  hash: sha256:387bad42083bfa6f2ac79781096a48796e1b0e141792328d9810971e043c1a93
  license:

schema:
status: generated
last_generated_at: "2026-09-24"
extracted_tokens: 4086
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/spring-ai-alibaba.md
  - .wikicommit/entity/en/DefinedTerm/agent2agent-protocol.md
failed_pages: []
---

## Summary

Chapter 3 of the AI 原生应用架构白皮书 (AI-native application architecture whitepaper) hosted on jimmysong.io, which surveys agent development paradigms — a plain LLM application, a single augmented agent, predefined workflows and model-driven multi-agent systems — and illustrates them with the Java framework Spring AI Alibaba and its ReactAgent, SequentialAgent, ParallelAgent, LoopAgent and LlmRoutingAgent types. It then covers moving agents from a single process to distributed deployment through the A2A protocol, with Nacos serving as an agent registry, message-driven agent communication built on RocketMQ, and team collaboration organised around unified metadata.

## Generation Notes

- This chapter is part of a continuously-updated online whitepaper with no fixed publication date of its own, so it was not treated as a source-as-entity.
- "Nacos" and "RocketMQ" were not given pages of their own: the chapter describes each only in the role it plays for agents (an A2A registry, a message transport), and the Nacos material is carried on the Agent2Agent Protocol page.
