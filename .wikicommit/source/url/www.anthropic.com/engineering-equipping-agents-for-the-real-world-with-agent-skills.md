---
source:
  type: url
  url: 'https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills'
  hash: sha256:e884d6fd1fe5becb8f432c99a20cf8b36e39d087e507037696b411e11d077ef5
  license:

schema:
status: partial
last_generated_at: "2026-09-19"
extracted_tokens: 4220
generated_pages:
  - .wikicommit/entity/en/BlogPosting/equipping-agents-for-the-real-world-with-agent-skills.md
  - .wikicommit/entity/en/DefinedTerm/agent-skills.md
  - .wikicommit/entity/en/DefinedTerm/progressive-disclosure.md
failed_pages: []
---

## Summary

Anthropic's engineering post introducing Agent Skills: organized folders of instructions, scripts and resources that an agent discovers and loads dynamically, built around a required SKILL.md file whose YAML frontmatter carries a name and description. It presents progressive disclosure as the format's core design principle — metadata pre-loaded into the system prompt, the SKILL.md body read on trigger, and bundled files navigated only as needed — and works the arrangement through the PDF skill behind Claude's document-editing abilities, including a bundled script the model runs without loading it into context. It closes with authoring guidance (start from evaluation, split for scale, attend to name and description, iterate with the model), a warning to audit skills from less-trusted sources, and stated intentions to explore complementing MCP servers and to let agents author their own Skills.

## Generation Notes

- "Barry Zhang": excluded (privacy) — a named author of the source post; a living individual named by the source without being its subject, per entity-policy.md.
- "Keith Lazuka": excluded (privacy) — a named author of the source post; a living individual named by the source without being its subject, per entity-policy.md.
- "Mahesh Murag": excluded (privacy) — a named author of the source post; a living individual named by the source without being its subject, per entity-policy.md.
