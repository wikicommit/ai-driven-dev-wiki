---
source:
  type: url
  url: 'https://developer.nvidia.com/blog/securing-llm-systems-against-prompt-injection/'
  hash: sha256:3586be2459ba07a9385bba9fe13f4902a44075110ce0e0594535f80200bc5848
  license:

schema:
status: partial
last_generated_at: '2026-09-19'
extracted_tokens: 7494
generated_pages:
  - .wikicommit/entity/en/BlogPosting/securing-llm-systems-against-prompt-injection.md
  - .wikicommit/entity/en/DefinedTerm/control-data-plane-confusion.md
  - .wikicommit/entity/en/SoftwareApplication/langchain.md
  - .wikicommit/entity/en/DefinedTerm/prompt-injection.md
  - .wikicommit/entity/en/Organization/nvidia.md
failed_pages: []
---
## Summary

The NVIDIA AI Red Team discloses three vulnerabilities in LangChain chains — remote code execution in `llm_math` (CVE-2023-29374), server-side request forgery in `APIChain.from_llm_and_api_docs` (CVE-2023-32786) and SQL injection in `SQLDatabaseChain` (CVE-2023-32785) — all reachable by prompt-injecting the model whose output the chain then turns into a call to an external service. The post is explicit that these affect specific chains rather than LangChain's core engine, and that the affected components had been removed from the core library by the time of writing. Its general argument is that control and data planes are not separable in an LLM prompt, so every model production should be treated as potentially malicious and external calls strictly parameterized at least privilege.

## Generation Notes

- "Rich Harang": excluded, privacy — the post's author, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. Not a relevance judgment. No page exists for this entity.
