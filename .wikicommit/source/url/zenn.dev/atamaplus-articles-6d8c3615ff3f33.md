---
source:
  type: url
  url: 'https://zenn.dev/atamaplus/articles/6d8c3615ff3f33'
  hash: sha256:ca7b63ec337b963433b4413e2e2821307e56ce9248f4a9ff5d3f2cc95316d76a
  license:
  lang: ja

schema:
status: generated
last_generated_at: "2026-10-04"
extracted_tokens: 2759
generated_pages:
  - .wikicommit/entity/en/BlogPosting/sharing-skills-across-multiple-coding-agents.md
failed_pages: []
---

## Summary

A post on the atama plus tech blog describing how a team whose members use both Claude Code and OpenAI Codex shares one set of Agent Skills between the two agents: the skills live in a common `.agent/skills/` directory and each agent's own skills directory is a symbolic link to it, following the same approach the team already used to make `CLAUDE.md` a symlink to `AGENTS.md`. The author reports that moving the team's guidelines into skills cut its `AGENTS.md` from over 600 lines to about 100 and stopped unrelated guidelines from being loaded into context, and notes how VS Code and Cursor can pick up the same skills.

## Generation Notes

- "yutake27": privacy — the post's author, a private individual rather than a public figure; entity-policy.md rules out pages about such individuals.
- "atama plus": theme_mismatch — the EdTech company publishing the blog; named only as the author's employer and not itself a subject related to AI-driven development.
