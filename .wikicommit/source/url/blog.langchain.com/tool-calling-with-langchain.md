---
source:
  type: url
  url: 'https://blog.langchain.com/tool-calling-with-langchain/'
  hash: sha256:272d889d15308a542b7029c3aae6528c22e13a794ef6e75763f377ff9e0b206a
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 4629
generated_pages:
  - .wikicommit/entity/en/BlogPosting/tool-calling-with-langchain.md
  - .wikicommit/entity/en/DefinedTerm/tool-use-design-pattern.md
  - .wikicommit/entity/en/SoftwareApplication/langchain.md
failed_pages: []
---


## Summary

An April 2024 LangChain blog post introducing a standard interface for tool calling across model providers: ChatModel.bind_tools() for attaching tool definitions to model calls, an AIMessage.tool_calls attribute that returns the model's tool invocations in a common format, and create_tool_calling_agent(), an agent constructor that works with any model implementing both. It recounts how providers from OpenAI onward added native tool calling through mutually incompatible interfaces, and explains how with_structured_output, built on tool calling for most models, differs from binding tools directly.
