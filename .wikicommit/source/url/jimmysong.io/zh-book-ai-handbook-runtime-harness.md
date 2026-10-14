---
source:
  type: url
  url: 'https://jimmysong.io/zh/book/ai-handbook/runtime/harness/'
  hash: sha256:82cf9e7387cf2117eac969bb6ccb6061e9f58fd5de7e0191c1baed3aae3a014b
  license:
  lang: zh

schema:
status: generated
last_generated_at: "2026-10-14"
extracted_tokens: 4718
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/agent-harness.md
  - .wikicommit/entity/en/SoftwareApplication/hermes-agent.md
  - .wikicommit/entity/en/DefinedTerm/agent-runtime.md
failed_pages: []
---


## Summary

This chapter of Jimmy Song's online book on building AI agents defines the harness as the runtime substrate between the model and the application that mediates observation, action, feedback and completion, and lists six core responsibilities (observation, action, feedback, completion/verification, permission and memory) whose completeness separates a harness from a framework. It contrasts the framework and harness paradigms, presents Hermes Agent (always-on), Claude Code (developer-facing) and OpenAI Codex (cloud-asynchronous) as three productized forms, and positions the harness as the single-agent execution layer beneath a multi-agent Agent Runtime. It closes with the security risks of always-on agents, such as prompt injection, confused-deputy attacks and permission escape, and argues for least-privilege design.
