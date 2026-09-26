---
source:
  type: url
  url: 'https://addyosmani.com/blog/coding-agents-manager/'
  hash: sha256:fc697c3fcc830075a1a6b6751a1f242d4b6ff4ea9a385c1ec60a0c6f8a6e50a1
  license:

schema:
status: generated
last_generated_at: "2026-09-17"
extracted_tokens: 4270
generated_pages: [".wikicommit/entity/en/BlogPosting/your-ai-coding-agents-need-a-manager.md", ".wikicommit/entity/en/Book/beyond-vibe-coding.md", ".wikicommit/entity/en/DefinedTerm/human-in-the-loop.md", ".wikicommit/entity/en/DefinedTerm/verification-loop.md", ".wikicommit/entity/en/DefinedTerm/git-worktrees.md", ".wikicommit/entity/en/SoftwareApplication/github-copilot-coding-agent.md", ".wikicommit/entity/en/SoftwareApplication/openai-codex.md", ".wikicommit/entity/en/DefinedTerm/conductor-and-orchestrator-modes.md", ".wikicommit/entity/en/DefinedTerm/agents-md.md"]
failed_pages: []
---

## Summary

A blog post by Addy Osmani arguing that as AI coding agents increasingly do meaningful work in the background, the highest-leverage developers act as "async-first managers" running a small fleet of parallel agents, and that core engineering-management skills — clear task scoping, delegation, verification loops, and async check-ins — transfer directly to doing this well. It sets out a two-mode model (local, human-in-the-loop sessions versus asynchronous background sessions), covers practical patterns such as git worktrees and explicit task-boundary rules for avoiding merge conflicts between parallel agents, and proposes a repeatable plan/spawn/monitor/verify/integrate/retro loop for running the resulting workflow.

## Generation Notes

- "Addy Osmani": excluded (privacy) — the post's living author; no existing page.
- "Boris Cherny": excluded (privacy) — described in the source as Claude Code's creator and as running a widely-discussed multi-session parallel-agent workflow; a living public figure, so entity-policy.md's exclude_living_persons rule applies; no existing page. His workflow is attributed to him in the body of [[BlogPosting/your-ai-coding-agents-need-a-manager]] instead.
- "Simon Willison": excluded (privacy) — a living public figure whose view on parallel-agent review bottlenecks is discussed in the source; entity-policy.md's exclude_living_persons rule applies; no existing page. His view is attributed to him in the body of [[BlogPosting/your-ai-coding-agents-need-a-manager]] instead.
- "Beyond Vibe Coding": the source states the book's publisher (O'Reilly), but `Book.md`'s `properties:` block has no `publisher` field, so it is recorded in the page body only.

