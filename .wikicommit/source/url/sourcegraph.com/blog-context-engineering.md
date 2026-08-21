---
source:
  type: url
  url: 'https://sourcegraph.com/blog/context-engineering'
  hash: sha256:004e8195be79c691c84abc9a3ab6d698b8815f7ee396e367c8aca94f56715dc3

schema:
status: partial
last_generated_at: "2026-08-21"
extracted_tokens: 5891
generated_pages:
  - .wikicommit/entity/en/BlogPosting/context-engineering-a-practical-guide-for-ai-agents.md
  - .wikicommit/entity/en/Dataset/codescalebench.md
  - .wikicommit/entity/en/Organization/sourcegraph.md
  - .wikicommit/entity/en/DefinedTerm/context-engineering.md
failed_pages: []
---


## Summary

A Sourcegraph guide of 28 May 2026 by Matt Tanner, companion to the same author's agentic coding guide a week earlier. The context engineering page gained its four-pillar organisation (instructions, retrieval, memory, tools), its usable test for the prompt-engineering boundary — rewording versus rewiring — and two mechanisms the vendor accounts there had not covered: token budget management as pre-filtering, and re-ranking as the step where naive RAG pipelines either start or stop working. Its CodeScaleBench retrieval figures went to that benchmark's page.

Excluded as unrelated to the configured theme:
- "Sourcegraph MCP server" (theme_mismatch): the publisher's own product, presented as the answer to the retrieval pillar. Vendor product marketing is excluded by the configured theme; its capabilities are noted in prose on the Sourcegraph organisation page instead.
- "Vector database and orchestration tool listings" (theme_mismatch): the guide's category sketch of Weaviate, Pinecone, Qdrant, Milvus, pgvector, LangChain, LlamaIndex, DSPy, mem0 and Letta is a comparison listing of general AI infrastructure, which the theme excludes; none is discussed as an independent subject.

Its citations of Phil Schmid, Anthropic, and the Liu et al. "lost in the middle" paper are recorded as this guide's characterisations rather than as directly sourced claims, since none of those documents was ingested.

Re-checked on 2026-08-21 (content unchanged, cache hit) as a dedicated coverage comparison. Three uncovered items were found and added: the per-turn context assembly pipeline (user query, parallel retrieval steps, merge into a candidate set, then memory, system instructions and tool definitions, with each subagent running the same pipeline against a narrower scope); the quadratic-attention cost argument for why token budgets matter beyond recall; and the operational instrumentation the guide prescribes — tracking token usage and tool-call counts per task, setting budgets, and alerting when an agent class exceeds them. The context engineering page separately gained the guide's definition of "context engineer" as a platform-team role. The status stays `partial` because of the theme exclusions above.
