---
title: "AIDev: Studying AI Coding Agents on GitHub"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, dataset, software-engineering]
sources:
  - type: url
    url: https://arxiv.org/pdf/2602.09185
    hash: sha256:3d94ab700934f9544d412431d530fd11f6856381d3e23f9b57ac0adcd28f9989
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "The paper introducing the AIDev dataset: 932,791 agent-authored pull requests (Agentic-PRs) from OpenAI Codex, Devin, GitHub Copilot, Cursor, and Claude Code across 116,211 GitHub repositories, plus a curated 33,596-PR subset enriched with review, commit, and issue data."
  author: ["Hao Li", "Haoxiang Zhang", "Ahmed E. Hassan"]
  datePublished: "2026-02"
  keywords: ["AI Agent", "Agentic AI", "Coding Agent", "Agentic Coding", "Software Engineering Agent"]
---

This paper (MSR '26) introduces [[Dataset/aidev]], a dataset of 932,791 agent-authored pull
requests ("Agentic-PRs") drawn from 116,211 real-world GitHub repositories and 72,189 developers,
authored by five coding agents: OpenAI Codex, Devin, GitHub Copilot, Cursor, and Claude Code, with a
dataset cutoff of August 1, 2025. A curated subset of 33,596 Agentic-PRs from 2,807 repositories
with more than 100 GitHub stars is additionally enriched with review comments, commit-level diffs,
issue links, and full pull-request event timelines. The dataset is distributed through Hugging Face
and Zenodo, with example Jupyter notebooks published on GitHub.

The paper motivates AIDev by arguing that much of the existing evidence on AI coding agents derives
from controlled studies, benchmarks, or small-scale deployments rather than large-scale real-world
activity, and proposes it as a foundation for empirical study of adoption, code-patch
characteristics, testing behavior, review dynamics, and failure patterns and risks of coding agents
operating on real repositories.

## Key Points
- Introduces AIDev, aggregating 932,791 Agentic-PRs across 116,211 repositories and 72,189
  developers, authored by five agents (OpenAI Codex, Devin, GitHub Copilot, Cursor, Claude Code)
- Provides a curated enriched subset of 33,596 Agentic-PRs from 2,807 repositories with over 100
  GitHub stars, additionally carrying comments, reviews, commits, and related issues
- Includes automated PR-purpose annotations (bug fix, feature, documentation, etc.) following the
  Conventional Commits categories, generated with GPT-based classification
- Proposes example research questions across five areas: adoption and practices, code patch
  characteristics, testing behavior, review dynamics, and failure patterns and risks
- Situates Agentic-PRs against earlier automation research in its related-work review, noting that
  rule-based and dependency-update bots rarely exhibit the initiative, contextual reasoning, or
  dialogical interaction seen in human contributors, and that PRs involving LLM assistance take
  longer to close and receive heavier review than routine bot contributions

## Notes
- The dataset's cutoff date is August 1, 2025; findings drawn from it reflect agent behavior up to
  that date only
- The paper is presented at MSR '26 rather than being an empirical-findings paper — it describes
  the dataset's structure and proposes research questions rather than answering them
