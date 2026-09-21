---
source:
  type: url
  url: 'https://aws.amazon.com/cn/blogs/china/agentic-ai-infrastructure-practice-series-nine-context-engineering/'
  hash: sha256:1ea97ed3d4e23cb29114ffee329716c05e979b914a7a52d5b181bf258202267f
  license:

schema:
status: generated
last_generated_at: "2026-09-21"
extracted_tokens: 8845
generated_pages:
  - .wikicommit/entity/en/BlogPosting/agentic-ai-infrastructure-context-engineering.md
  - .wikicommit/entity/en/SoftwareApplication/amazon-bedrock-agentcore.md
  - .wikicommit/entity/en/SoftwareApplication/strands-agents.md
  - .wikicommit/entity/en/DefinedTerm/context-engineering.md
failed_pages: []
---

## Summary

The ninth post in AWS China's Agentic AI infrastructure practice series, setting out context engineering as a technical methodology for managing what enters an LLM's context window in agent systems. It defines context engineering against traditional prompt engineering — treating context as a collection of dynamic, structured components rather than a static string — and decomposes it into three core components: context retrieval and generation, context processing, and context management. The second half maps these onto AWS services, with worked code for Amazon Bedrock prompt caching, Strands Agents conversation managers, and Amazon Bedrock AgentCore Memory and Gateway.
