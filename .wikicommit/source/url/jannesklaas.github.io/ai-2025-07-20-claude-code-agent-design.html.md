---
source:
  type: url
  url: 'https://jannesklaas.github.io/ai/2025/07/20/claude-code-agent-design.html'
  hash: sha256:4a0473d4cac9881fc7c599ead1e961497f8b69dd92f740662432f38a1d48ce18
  license:
  lang: en

schema:
status: generated
last_generated_at: "2026-09-30"
extracted_tokens: 3218
generated_pages: [.wikicommit/entity/en/BlogPosting/agent-design-lessons-from-claude-code.md, .wikicommit/entity/en/DefinedTerm/system-reminder.md, .wikicommit/entity/en/SoftwareApplication/claude-code.md]
failed_pages: []
---


## Summary

Jannes Klaas's July 2025 blog post reports what he learned about agent design by inspecting Claude Code's API requests through a proxy. He finds its design relatively simple — a single `while(tool_use)` agent loop with 14 tools — and attributes its ability to stay on track over long sessions to a few techniques: TODO lists for planning, fixed instructions appended to tool results, statically generated system reminders, sub-agents dispatched through a Task tool, and a call to Claude Haiku that extracts file paths from commands.

## Generation Notes

"Jannes Klaas": privacy — the post's author, a living individual writing in 2025; entity-policy.md rules out pages about living individuals.
