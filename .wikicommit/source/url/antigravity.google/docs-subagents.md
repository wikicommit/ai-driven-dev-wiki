---
source:
  type: url
  url: 'https://antigravity.google/docs/subagents/'
  hash: sha256:5be9ef15339e691ef64f32feff17f95fe5b9fb784ff700b261fe1757ec8ce1a7
  license:

schema:
status: generated
last_generated_at: "2026-09-24"
extracted_tokens: 5957
generated_pages:
  - .wikicommit/entity/en/SoftwareApplication/google-antigravity.md
  - .wikicommit/entity/en/SoftwareApplication/antigravity-cli.md
failed_pages: []
---


## Summary

This page of the Google Antigravity documentation describes subagents in Antigravity 2.0 and the Antigravity CLI. A parent agent spawns concurrent subagents with the invoke_subagent tool; each starts with a clean context and can share the parent's workspace, get an isolated Git worktree or share directory storage. The page covers the built-in research, browser and self subagents, custom subagents defined as Markdown files with YAML frontmatter, the running, idle and killed lifecycle states, message-based communication between agents with a nesting limit of ten levels, inheritance of the parent's permissions, the /boost and /teamwork-preview multi-agent orchestrators, and the CLI's /agents and /tasks panels.
