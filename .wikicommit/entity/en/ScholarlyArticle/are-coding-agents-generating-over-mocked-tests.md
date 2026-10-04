---
title: "Are Coding Agents Generating Over-Mocked Tests? An Empirical Study"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, testing, mining-software-repositories]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2602.00409'
    hash: sha256:a2792d9e0c3d11cf7fd525bf183b0e20c95aab7066d7842e3ae2860c1ffce012
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "An empirical study of mocking in tests written by coding agents, based on more than 1.2 million commits made in 2025 across 2,168 TypeScript, JavaScript and Python repositories. It finds coding agents more likely than non-agents both to change tests and to add mocks to them."
  author: ["Andre Hora", "Romain Robbes"]
  datePublished: "2026-01-30"
  abstract: "Coding agents work with autonomy and leave visible traces in repositories, such as authored commits, and may generate tests autonomously, though the quality of those tests is uncertain; excessive mocking in particular can make tests harder to understand and maintain. The paper investigates mocks in agent-generated tests of real-world software, analysing over 1.2 million 2025 commits in 2,168 TypeScript, JavaScript and Python repositories."
---

This paper investigates whether coding agents write tests that lean too heavily on mocks. Its starting point is that coding agents, unlike traditional LLM-based code completion tools, act with autonomy — invoking external tools, for instance — and leave visible traces in repositories such as the commits they author. Among their tasks they may generate tests autonomously, and the authors flag excessive mocking as a specific quality risk, since it can make tests harder to understand and maintain.

The authors describe it as the first study of mocks in agent-generated tests of real-world software systems. They analysed over 1.2 million commits made in 2025 in 2,168 TypeScript, JavaScript and Python repositories: 48,563 of those commits were made by coding agents, 169,361 modified tests and 44,900 added mocks to tests. The overall finding is that coding agents are more likely than non-coding agents both to modify tests and to add mocks to them, and that recently created repositories carry a higher share of agent-made test and mock commits.

The paper was submitted to arXiv on 30 January 2026 (arXiv:2602.00409) under Software Engineering (cs.SE), and is marked as accepted for publication at MSR 2026.

## Key Points

- 60% of repositories with agent activity also contain agent test activity.
- 23% of commits made by coding agents add or change test files, compared with 13% of commits by non-agents.
- 68% of repositories with agent test activity also contain agent mock activity.
- 36% of commits made by coding agents add mocks to tests, compared with 26% by non-agents.
- Repositories created recently contain a higher proportion of test and mock commits made by agents.
- The authors suggest that tests with mocks may be easier to generate automatically but less effective at validating real interactions.
- They call for guidance on mocking practices to be included in agent configuration files.
