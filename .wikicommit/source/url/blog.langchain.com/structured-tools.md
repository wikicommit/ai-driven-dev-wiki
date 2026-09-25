---
source:
  type: url
  url: 'https://blog.langchain.com/structured-tools/'
  hash: sha256:e4617b3533e7c5a963a20bc2b7e5763d3a2a4cfe73dd16914c5abd6772686b08
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 4431
generated_pages:
  - .wikicommit/entity/en/BlogPosting/structured-tools.md
  - .wikicommit/entity/en/DefinedTerm/structured-tool.md
  - .wikicommit/entity/en/SoftwareApplication/langchain.md
failed_pages: []
---


## Summary

A May 2023 LangChain blog post introducing structured tools: a new tool abstraction that takes an arbitrary number of inputs of arbitrary types instead of the single string earlier LangChain tools accepted, together with a StructuredChatAgent built to work with them. It defines a structured tool by its name, description, args_schema (a Pydantic model) and _run/_arun functions, shows how to create one from a function or by subclassing BaseTool, announces file-management and PlayWright browser toolkits built on the new class, and explains how structured tools interoperate with older string tools and agents.
