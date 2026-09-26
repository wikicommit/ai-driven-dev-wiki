---
source:
  type: url
  url: 'https://simonwillison.net/guides/agentic-engineering-patterns/how-coding-agents-work/'
  hash: sha256:a8be3f0926e2b75d77e83036446bf575cf49b7dff42641018af0909da9d387eb
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 2669
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/ai-coding-agent.md
  - .wikicommit/entity/en/DefinedTerm/chat-templated-prompt.md
  - .wikicommit/entity/en/DefinedTerm/token-caching.md
  - .wikicommit/entity/en/DefinedTerm/harness-engineering.md
failed_pages: []
---

## Summary

A guide chapter explaining the machinery under a coding agent: the agent is a harness around a language model, extending it with invisible prompts and callable tools. It walks through tokens and pricing, the chat-templated prompt that simulates a conversation over a stateless completion engine, the cached-prefix pricing that makes agents avoid rewriting earlier conversation, how a tool call is expressed in the prompt and its result fed back, the hidden system prompt, and reasoning as spending extra tokens before replying — concluding that an agent is little more than a model, a system prompt and tools in a loop.

## Generation Notes

- "Simon Willison": excluded, privacy — the chapter's author, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. No page exists for this entity.
- The chapter is part of a continuously-updated guide rather than a dated work, so it was not treated as a source-as-entity and no page was created for the chapter itself.
