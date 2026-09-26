---
source:
  type: url
  url: 'https://addyosmani.com/blog/long-running-agents/'
  hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
  license:

schema:
status: generated
last_generated_at: "2026-09-17"
extracted_tokens: 7599
generated_pages:
  - .wikicommit/entity/en/BlogPosting/long-running-agents.md
  - .wikicommit/entity/en/DefinedTerm/long-running-agent.md
  - .wikicommit/entity/en/DefinedTerm/brain-hands-session-split.md
  - .wikicommit/entity/en/DefinedTerm/checkpoint-and-resume.md
  - .wikicommit/entity/en/SoftwareApplication/claude-managed-agents.md
  - .wikicommit/entity/en/SoftwareApplication/gemini-enterprise-agent-platform.md
  - .wikicommit/entity/en/Organization/google.md
  - .wikicommit/entity/en/DefinedTerm/ralph-loop.md
  - .wikicommit/entity/en/DefinedTerm/planner-worker-model.md
  - .wikicommit/entity/en/DefinedTerm/context-rot.md
  - .wikicommit/entity/en/DefinedTerm/compaction.md
  - .wikicommit/entity/en/DefinedTerm/agents-md.md
  - .wikicommit/entity/en/DefinedTerm/human-in-the-loop.md
  - .wikicommit/entity/en/DefinedTerm/git-worktrees.md
  - .wikicommit/entity/en/SoftwareApplication/cursor.md
  - .wikicommit/entity/en/Organization/anthropic.md
failed_pages: []
---

## Summary

This Addy Osmani post surveys "long-running agents" -- AI agents that keep making progress across many sessions and sandboxes over hours, days, or weeks -- distinguishing long-horizon reasoning, long-running execution, and persistent agency, and naming three recurring obstacles: finite context, no persistent state, and no self-verification. It compares how Anthropic (harnesses, then a brain/hands/session split), Cursor (planner/worker/judge roles), and Google (the Gemini Enterprise Agent Platform, including Agent Runtime, Agent Sessions, and Agent Memory Bank) each address those problems, and sets out five production patterns -- checkpoint-and-resume, delegated approval, memory-layered context, ambient processing, and fleet orchestration -- along with practical guidance and current limitations (cost, security, alignment drift, verification, and the human role).

## Generation Notes

"Addy Osmani": excluded, privacy -- the post's living author, whose contributions are attributed to him in body text on the pages this source produced rather than given a page of his own; no existing page.
"Geoffrey Huntley": excluded, privacy -- a living individual credited (with Ryan Carson) with popularizing the Ralph loop; already covered by attribution in [[DefinedTerm/ralph-loop]]'s body; no existing page.
"Ryan Carson": excluded, privacy -- a living individual credited (with Geoffrey Huntley) with popularizing the Ralph loop and with the Compound Product project; already covered by attribution in [[DefinedTerm/ralph-loop]]'s body; no existing page.
"Shubham Saboo": excluded, privacy -- a living individual named as Osmani's co-author on the "five patterns for long-running agents" write-up; attributed in body text rather than given a page; no existing page.

