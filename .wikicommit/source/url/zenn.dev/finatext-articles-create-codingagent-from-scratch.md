---
source:
  type: url
  url: 'https://zenn.dev/finatext/articles/create-codingagent-from-scratch'
  hash: sha256:f2f67945e5431dbe4a2a268e3e16b3b5db6f49d349699e7530f7ec02476812bc
  license:
  lang: ja

schema:
status: generated
last_generated_at: "2026-10-04"
extracted_tokens: 6722
generated_pages:
  - .wikicommit/entity/en/BlogPosting/building-a-coding-agent-from-scratch-in-python.md
failed_pages: []
---

## Summary

A Nowcast data engineer describes building a multi-agent coding agent from scratch in Python with LangChain and Azure OpenAI GPT-4.1, originally for an internal generative-AI contest within the Finatext group. The system pairs a ProgrammerAgent that generates code with tools for reading, writing and branching files, a ReviewerAgent that reviews diffs, runs pytest and records LGTM, and an AgentCoordinator that loops the two until the reviewer approves or an iteration limit is reached; the post walks through the tool design and shows example runs.

## Generation Notes

- "Takumi": privacy — the post's author, a private individual rather than a public figure; entity-policy.md rules out pages about such individuals.
- "Finatext / Nowcast": theme_mismatch — the fintech group and its subsidiary that employ the author and publish the blog; named only as the author's employer and contest organiser.
