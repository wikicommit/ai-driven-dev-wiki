---
source:
  type: url
  url: 'https://github.blog/news-insights/product-news/github-copilot-meet-the-new-coding-agent/'
  hash: sha256:f3a6917c79f2f70870a12536be1e700c8b33381be9f7cfe35243aba5ec7dab46
  license:

schema:
status: generated
last_generated_at: '2026-09-19'
extracted_tokens: 8146
generated_pages:
  - .wikicommit/entity/en/BlogPosting/github-copilot-meet-the-new-coding-agent.md
  - .wikicommit/entity/en/SoftwareApplication/github-copilot-coding-agent.md
  - .wikicommit/entity/en/SoftwareApplication/github-copilot.md
  - .wikicommit/entity/en/Organization/github.md
failed_pages: []
---

## Summary

GitHub's May 2025 announcement of the Copilot coding agent, whose delegation interface is assigning a GitHub issue to Copilot: the agent then boots a virtual machine on GitHub Actions, clones the repository, analyses the codebase with retrieval-augmented generation powered by GitHub code search, and pushes commits to a draft pull request while exposing its reasoning in session logs. It supports Model Context Protocol servers configured per repository and reads images attached to the issues it is given. The post sets out four default security policies -- branch restrictions, a bar on the requester approving the agent's own pull request, a limited network allowlist, and CI workflows requiring human approval -- and states the agent is strongest on low-to-medium complexity tasks in well-tested codebases.

## Generation Notes

- "Thomas Dohmke": excluded, privacy -- the post's author, a living individual, which `.wikicommit/entity-policy.md`'s `exclude_living_persons` switch rules out. Not a relevance judgment. No page exists for this entity; he is named in the page's `author` property as plain text instead.
