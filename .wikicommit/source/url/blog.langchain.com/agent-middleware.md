---
source:
  type: url
  url: 'https://blog.langchain.com/agent-middleware'
  hash: sha256:071e79d936c9e2d2b07b0eab257fff6823cbeb8a320c72649b9ca211b9cd7179
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 3610
generated_pages:
  - .wikicommit/entity/en/BlogPosting/agent-middleware.md
  - .wikicommit/entity/en/DefinedTerm/agent-middleware.md
  - .wikicommit/entity/en/DefinedTerm/agent-framework.md
  - .wikicommit/entity/en/SoftwareApplication/langchain.md
failed_pages: []
---

## Summary

This September 2025 LangChain blog post argues that agent frameworks sharing the simple model-prompt-tools loop fail in production because they give developers too little control over context engineering, and recounts the parameters LangChain added over two years (dynamic prompts, pre- and post-model hooks, dynamic model selection) before they became hard to coordinate. It introduces Middleware in LangChain 1.0 as the replacement: composable units with before_model, after_model and modify_model_request hooks that run like web-server middleware, shipped initially as human-in-the-loop, summarization and Anthropic prompt caching implementations.
