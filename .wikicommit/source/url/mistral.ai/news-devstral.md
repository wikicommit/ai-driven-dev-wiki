---
source:
  type: url
  url: 'https://mistral.ai/news/devstral'
  hash: sha256:391e456654323c32f4e71ba4eaf0b08ccd8b7650155b2bf99f04f989ea5772cb
  license:

schema:
status: partial
last_generated_at: "2026-09-22"
extracted_tokens: 2952
generated_pages:
  - .wikicommit/entity/en/BlogPosting/devstral.md
failed_pages: []
ambiguous_entities:
  - title: "Devstral"
    type: "schema:SoftwareApplication"
    alternatives: ["schema:SoftwareApplication", "schema:DefinedTerm"]
---

## Summary

Mistral AI's May 21, 2025 announcement of Devstral, an Apache 2.0 agentic LLM for software engineering built in collaboration with All Hands AI and trained to resolve real GitHub issues while running over code agent scaffolds such as OpenHands or SWE-Agent. The post reports the model's SWE-Bench Verified result against other open and closed models, and presents it as light enough to run on a single consumer GPU, which the post frames as suiting local deployment and privacy-sensitive enterprise repositories.

## Generation Notes

- "Devstral": ambiguous type, not generated. Candidate types were schema:SoftwareApplication and schema:DefinedTerm, for the same reason recorded against Devstral 2 in the news-devstral-2-vibe-cli source: the two installed schema files each exclude the other's case for an LLM model release. A human decision is needed; resolve with /wikicommit-reconcile --source https://mistral.ai/news/devstral.
