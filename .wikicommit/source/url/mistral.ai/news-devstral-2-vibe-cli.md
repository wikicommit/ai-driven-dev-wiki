---
source:
  type: url
  url: 'https://mistral.ai/news/devstral-2-vibe-cli'
  hash: sha256:2138589678ecaf64d2613d8944af216e4e3b69049df0e348b80da6cd73da9788
  license:

schema:
status: partial
last_generated_at: "2026-09-22"
extracted_tokens: 3702
generated_pages:
  - .wikicommit/entity/en/BlogPosting/introducing-devstral-2-and-mistral-vibe-cli.md
  - .wikicommit/entity/en/SoftwareApplication/mistral-vibe-cli.md
failed_pages: []
ambiguous_entities:
  - title: "Devstral 2"
    type: "schema:SoftwareApplication"
    alternatives: ["schema:SoftwareApplication", "schema:DefinedTerm"]
---

## Summary

Mistral AI's December 9, 2025 announcement of Devstral 2, an open-weight coding model family released in a 123B and a 24B size under a modified MIT and Apache 2.0 license respectively, together with Mistral Vibe CLI, an Apache 2.0 command-line coding agent built for those models. The post sets out the models' context window and deployment requirements, reports SWE-bench Verified results and a human preference evaluation against DeepSeek V3.2 and Claude Sonnet 4.5, and describes the CLI's project-aware context, multi-file orchestration and IDE integration via the Agent Communication Protocol.

## Generation Notes

- "Devstral 2": ambiguous type, not generated. Candidate types were schema:SoftwareApplication and schema:DefinedTerm. SoftwareApplication.md's boundary rule excludes a model weights release from that type, while DefinedTerm.md's boundary rule excludes a concrete named entity from that one, and Schema.org has no AI-model type for Pass 2b to propose. A human decision is needed; resolve with /wikicommit-reconcile --source https://mistral.ai/news/devstral-2-vibe-cli.
