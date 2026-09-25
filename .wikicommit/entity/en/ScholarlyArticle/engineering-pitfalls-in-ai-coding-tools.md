---
title: "Engineering Pitfalls in AI Coding Tools: An Empirical Study of Bugs in Claude Code, Codex, and Gemini CLI"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, software-reliability, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2603.20847'
    hash: sha256:0cdc6f16119b99dddf98bae8084b1f927f48cea23382ac797220432711462d44
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An empirical study that manually analyses over 3.8K publicly reported bugs in the open-source repositories of Claude Code, Codex and Gemini CLI to characterize the engineering pitfalls of building AI-assisted coding tools."
  author: ["Ruixin Zhang", "Wuyang Dai", "Hung Viet Pham", "Gias Uddin", "Jinqiu Yang", "Song Wang"]
  datePublished: "2026-03-21"
  keywords: ["AI coding tools", "bug study", "empirical software engineering", "coding agents"]
---

The paper studies the engineering of AI-assisted coding tools such as [[SoftwareApplication/claude-code]], Codex and [[SoftwareApplication/gemini-cli]]. It argues that while these tools promise significant productivity gains, building them — at the intersection of traditional software engineering, AI system design and human-computer interaction — is fraught with unique and poorly understood challenges, and presents itself as the first empirical study of the engineering pitfalls involved.

The authors systematically and manually analyse over 3.8K publicly reported bugs in the open-source GitHub repositories of those three tools. Using an open-coding methodology, they examine each issue description together with the associated user discussion and developer responses, and categorize every bug by type, location, root cause and observed symptoms. This annotation is used to characterize common failure patterns and recurring engineering challenges, which the authors offer as a roadmap for developers designing more reliable AI coding assistants.

## Key Points

- More than 67% of the bugs studied are related to functionality.
- In terms of root causes, 36.9% of the bugs stem from API, integration or configuration errors.
- The most commonly observed symptoms are API errors (18.3%), terminal problems (14%) and command failures (12.7%).
- The bugs predominantly affect the tool invocation (37.2%) and command execution (24.7%) stages of the system workflow.
- All of these figures are drawn from publicly reported issues in the repositories of three tools — Claude Code, Codex and Gemini CLI.

## Notes

The paper was submitted to arXiv on 21 March 2026 and is filed under Software Engineering (cs.SE).
