---
source:
  type: url
  url: 'https://zenn.dev/finatext/articles/create-codingagent-from-scratch'
  hash: sha256:dc3fb228a4ac418cfef6ff002cdd3cf3b07882e14c889527dfe2db2599a5e249
  license:
  lang: ja

schema:
status: generated
last_generated_at: "2026-10-16"
extracted_tokens: 6829
generated_pages:
  - .wikicommit/entity/en/BlogPosting/building-a-coding-agent-from-scratch-in-python.md
failed_pages: []
---

## Summary

A Nowcast data engineer describes building a multi-agent coding agent from scratch in Python with LangChain and Azure OpenAI GPT-4.1, originally for an internal generative-AI contest within the Finatext group. The system pairs a ProgrammerAgent that generates code with tools for reading, writing and branching files, a ReviewerAgent that reviews diffs, runs pytest and records LGTM, and an AgentCoordinator that loops the two until the reviewer approves or an iteration limit is reached; the post walks through the tool design and shows example runs.

## Generation Notes

- "Takumi": privacy — the post's author, a private individual rather than a public figure; entity-policy.md rules out pages about such individuals.
- "Finatext / Nowcast": theme_mismatch — the fintech group and its subsidiary that employ the author and publish the blog; named only as the author's employer and contest organiser.
