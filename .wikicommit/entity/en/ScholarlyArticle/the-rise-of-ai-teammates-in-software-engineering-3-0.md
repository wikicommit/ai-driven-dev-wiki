---
title: "The Rise of AI Teammates in Software Engineering (SE) 3.0: How Autonomous Coding Agents Are Reshaping Software Engineering"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, ai-teammates, pull-requests, code-review, dataset]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2507.15003'
    hash: sha256:b606da9c64693060e32a07080b2f9686773353b1bf3df05702abeea29a093a76
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A 2025 paper introducing AIDev, a large-scale dataset of pull requests authored by five autonomous coding agents on GitHub, and using it to show that agent-authored pull requests are accepted less often than human ones despite their speed."
  author: ["Hao Li", "Haoxiang Zhang", "Ahmed E. Hassan"]
  datePublished: "2025"
  keywords: ["AI Agent", "Agentic AI", "Coding Agent", "Agentic Coding", "Software Engineering Agent"]
---

This paper, from researchers at Queen's University, argues that the era of autonomous coding agents
in software engineering is not an impending future but an unfolding reality, and introduces
[[Dataset/aidev]] to ground that claim. As the paper describes it — presenting it as a living,
extensible resource — AIDev contains 456,535 pull requests created by five autonomous coding agents
([[SoftwareApplication/openai-codex]], [[SoftwareApplication/devin]], GitHub Copilot,
[[SoftwareApplication/cursor]] and [[SoftwareApplication/claude-code]]) across 61,453 GitHub
repositories and 47,303 developers, collected up to June 22, 2025. The paper calls such pull requests
Agentic-PRs, and frames the agents that open them as the AI teammates of
[[DefinedTerm/software-engineering-3-0]].

The pull requests were mined through the GitHub REST API with agent-specific search queries — bot
author names, branch prefixes such as `head:copilot/`, and body text such as "Co-Authored-By:
Claude" — with start-date filters. The paper contrasts this real-world data with static, curated
benchmarks such as SWE-bench, which it argues fail to capture the messy, emergent nature of software
engineering in practice. Its three case studies use AIDev-pop, a subset restricted to repositories
with at least 500 stars (7,122 pull requests from 856 repositories), compared against 6,628
human-authored pull requests from the same popular repositories.

## Key Points

- The paper proposes SE 1.5 ("predictive coding") as an intermediate step between SE 1.0 and SE 2.0,
  for token-level, context-aware assistance such as autocomplete, and describes SE 3.0 as agentic
  software engineering in which agents work at the task level and the developer's role shifts to
  orchestration.
- Over 55% of agent pull requests are feature development or bug fixes, matching the human
  distribution, though individual agents differ — 42.2% of GitHub Copilot's are bug fixes.
- Agent pull requests are accepted less often than human ones, particularly for features, bug fixes
  and performance work: OpenAI Codex's acceptance rate is 64%, Devin's 49% and GitHub Copilot's 35%,
  15 to 40 percentage points below humans — a gap the authors contrast with top SWE-bench Verified
  success rates above 70%.
- Documentation is a strength: OpenAI Codex (88.6%) and Claude Code (85.7%) exceed the human
  acceptance rate (76.5%) on documentation pull requests.
- GitHub Copilot completes half of its pull request jobs within 12.8 minutes and 75% within 18.5
  minutes, with a long tail past an hour.
- Accepted OpenAI Codex pull requests close in a median of 0.3 hours against 3.9 hours for human
  ones, which the authors read as efficiency but also as raising questions about review depth.
- Bot reviewers appear on 20.1% of agent pull requests against 10.0% of human ones; agents and their
  review bots often come from the same provider, forming closed loops the authors warn may reinforce
  provider-specific biases.
- In one project, a single developer submitted 164 Codex pull requests in a few days, nearly matching
  the 176 human pull requests of the preceding three and a half years, yet only 9.1% of those agent
  pull requests changed cyclomatic complexity against 23.3% of human ones.
- Authorship attribution is inconsistent — Devin, GitHub Copilot and Cursor mark authorship in commit
  metadata, Claude Code adds a default co-author line that can be disabled, and OpenAI Codex gives
  none — and the authors argue standardised authorship labelling should be a basic requirement.

## Notes

The paper derives nine research directions from its findings, among them integration-oriented
benchmarks grounded in real workflows, analysis of rejected pull requests to identify agent failure
modes, reducing the human cost of reviewing agent changes, and triage systems for reviewer effort.
Looking further ahead, it proposes treating software repositories as training environments for
agents, with merged pull requests and passing CI as reward signals, and dynamic benchmarking with a
living leaderboard built from live repository data. It closes by arguing that practices such as
Agile, Scrum and DevOps assumed an all-human workforce, and that SE 3.0 needs new methodologies for
orchestration, review and governance. The authors caution that the acceptance gaps were measured
only about two months into the public release of many of these agents.
