---
source:
  type: url
  url: 'https://www.anthropic.com/news/context-management'
  hash: sha256:2e78b9b42dd4fb917dd77e613ca45a3b65b4417a8499eb5d55167da969001cf6
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 5672
generated_pages:
  - .wikicommit/entity/en/BlogPosting/managing-context-on-the-claude-developer-platform.md
  - .wikicommit/entity/en/DefinedTerm/context-editing.md
failed_pages: []
---

## Summary

Anthropic introduced two context-management capabilities on the Claude Developer Platform in September 2025: context editing, which automatically clears stale tool calls and results from the context window as it approaches token limits, and the memory tool, which lets Claude store and consult information in a client-side, file-based memory directory that persists across conversations. On an internal agentic-search evaluation, Anthropic reports that the two combined improved performance by 39% over baseline and context editing alone by 29%, and that in a 100-turn web search evaluation context editing reduced token consumption by 84%.
