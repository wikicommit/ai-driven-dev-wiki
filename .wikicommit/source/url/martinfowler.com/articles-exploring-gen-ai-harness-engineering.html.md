---
source:
  type: url
  url: 'https://martinfowler.com/articles/exploring-gen-ai/harness-engineering.html'
  hash: sha256:cf7369071f56e7b3b36f7b003d612f4aa69fef17a7135ba19f2e22f2ad7e1cc6
  license:

schema:
status: generated
last_generated_at: "2026-09-25"
extracted_tokens: 6617
generated_pages:
  - .wikicommit/entity/en/BlogPosting/harness-engineering-for-coding-agent-users.md
  - .wikicommit/entity/en/DefinedTerm/guides-and-sensors.md
  - .wikicommit/entity/en/DefinedTerm/harnessability.md
  - .wikicommit/entity/en/DefinedTerm/harness-templates.md
failed_pages: []
---


## Summary

In this April 2026 article, which supersedes her February 2026 memo on the subject, Birgitta Böckeler proposes a mental model of harness engineering for users of coding agents: an outer harness of guides (feedforward controls) and sensors (feedback controls), each either computational (deterministic tools such as tests and linters) or inferential (LLM-based review), which humans steer by iterating on it whenever an issue recurs. She discusses distributing controls across the change lifecycle to keep quality left, distinguishes maintainability, architecture fitness and behaviour harnesses (calling the last the least solved), introduces harnessability and speculative harness templates tied to service topologies, and argues that a harness should direct human input to where it matters most rather than eliminate it, closing with open questions about harness coherence and coverage.

## Generation Notes

- "Birgitta Böckeler": excluded (privacy) — the article's author, a living individual named by the source without being its subject, per entity-policy.md.
- "Ned Letcher": excluded (privacy) — a colleague quoted for the term "ambient affordances", a living individual named in passing, per entity-policy.md.
- "Kief Morris": excluded (privacy) — named in the acknowledgements, a living individual named in passing, per entity-policy.md.
