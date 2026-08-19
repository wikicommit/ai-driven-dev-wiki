---
source:
  type: url
  url: 'https://developer.microsoft.com/blog/protecting-against-indirect-injection-attacks-mcp/'
  hash: sha256:75eb803ce303bb04ab925d41277a47055f64ccef01e15cfc3d3a0ed89110bbe6

schema:
status: generated
last_generated_at: "2026-08-19"
extracted_tokens: 6074
generated_pages:
  - .wikicommit/entity/en/TechArticle/protecting-against-indirect-prompt-injection-attacks-in-mcp.md
  - .wikicommit/entity/en/DefinedTerm/indirect-prompt-injection.md
  - .wikicommit/entity/en/DefinedTerm/tool-poisoning.md
  - .wikicommit/entity/en/DefinedTerm/model-context-protocol.md
failed_pages: []
---

## Summary

Microsoft developer-blog guidance of 28 April 2025 by Sarah Young and Den Delimarsky on mitigating prompt injection in Model Context Protocol deployments. It defines indirect prompt injection (also cross-domain prompt injection or XPIA) and treats tool poisoning — malicious instructions embedded in MCP tool descriptions — as a subset of it, flagging hosted servers where definitions can be amended after user approval. Its two recommended defences are Microsoft's AI Prompt Shields and extending supply chain security to foundation models, embeddings services and context providers.
