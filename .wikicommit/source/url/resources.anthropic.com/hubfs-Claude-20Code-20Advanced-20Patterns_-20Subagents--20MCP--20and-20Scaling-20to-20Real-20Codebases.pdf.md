---
source:
  type: url
  url: 'https://resources.anthropic.com/hubfs/Claude%20Code%20Advanced%20Patterns_%20Subagents,%20MCP,%20and%20Scaling%20to%20Real%20Codebases.pdf'
  hash: sha256:143e1a9f91063648c6ee3a39d9db2b5f2b9c7d42efa9188abdc46b3e3b104a9d

schema:
status: generated
last_generated_at: "2026-08-21"
extracted_tokens: 2007
generated_pages:
  - .wikicommit/entity/en/PresentationDigitalDocument/claude-code-advanced-patterns.md
  - .wikicommit/entity/en/SoftwareApplication/claude-code.md
  - .wikicommit/entity/en/DefinedTerm/subagents.md
failed_pages: []
---


## Summary

An Anthropic webinar slide deck of 24 March 2026 on scaling Claude Code to large codebases, organised around two "when to use which feature" decision tables — CLAUDE.md versus hooks versus MCP for customization, and parallel sessions versus subagents versus agent teams for parallelization — followed by GitHub Actions and Code Review integrations and a live demo. What it adds beyond the written documentation already on the Claude Code page is the side-by-side decision framing and the CLAUDE.md scaling practices: hierarchical discovery by walking up the directory tree, a 200-line ceiling per file, `.claude/rules/` with path-scoped frontmatter, and the `claudeMdExcludes` setting.

No entities were excluded. Agent Teams is a Claude Code feature rather than an independent concept, so it is recorded on that product's page rather than as its own DefinedTerm, per DefinedTerm.md's named-entity boundary. The deck credits no individual presenter.
