---
source:
  type: url
  url: 'https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview'
  hash: sha256:3f2567f8a7cd1948e582601407ccfd2804e66152973859636da7ba44f9ff235f
  license:

schema:
status: generated
last_generated_at: "2026-09-19"
extracted_tokens: 7398
generated_pages:
  - .wikicommit/entity/en/DefinedTerm/agent-skills.md
  - .wikicommit/entity/en/DefinedTerm/progressive-disclosure.md
failed_pages: []
---

## Summary

Anthropic's overview documentation for Agent Skills, a filesystem-based format packaging instructions, metadata and optional scripts into a directory an agent loads on demand. It specifies the required SKILL.md frontmatter fields and their constraints, describes a three-level progressive-disclosure loading model with stated token costs, compares availability across the API, Claude Code and claude.ai, and sets out the security assumptions the format carries.

## Generation Notes

- "Agent Skills" was created as schema:DefinedTerm, not schema:SoftwareApplication: SoftwareApplication.md's boundary rule reserves that type for something installable, invocable or hosted and sends a specification or file format to DefinedTerm. Note that an unrelated SoftwareApplication/agent-skills page already exists for a third party's skill *library* of the same name — a name collision between two distinct subjects, worth a human's attention.
- The page itself was not extracted as a source entity: it is living vendor documentation with no fixed publication date.
