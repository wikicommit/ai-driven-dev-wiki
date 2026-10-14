---
title: "約2,000人が使うClaude Codeと向き合う。"
type: "schema:BlogPosting"
lang: en
tags: [ai-adoption, agent-governance, enterprise]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/64334/'
    hash: sha256:dc18d8b45978e25db5c716ec05dbb95fe49177aa52fd0b8812a9a63fd1f9b1b2
review_status: pending
generated_at: "2026-10-14"
generated_by: "claude-opus-5-5"
generated_with: "0.10.0"

properties:
  description: "A CyberAgent Developers Blog post reporting a Q&A session held on 12 June 2026 between CyberAgent engineers and Boris Cherny, who develops Claude Code at Anthropic, at a time when about 2,000 people inside the company were using Claude Code. It sets out the themes discussed and five lessons the company drew for using an AI coding agent at organizational scale."
  author: ["Ken Takao"]
  datePublished: "2026-06-18"
  publisher: "[[Organization/cyberagent]]"
---

This post on [[Organization/cyberagent]]'s developers' blog reports a Q&A session the company held on
12 June 2026 with Boris Cherny, whom the post introduces as the creator of
[[SoftwareApplication/claude-code]] at Anthropic. The post places the session at a point where use of
Claude Code inside CyberAgent had moved from individual engineers' experiments to an organization-wide
phase, with about 2,000 users, and where operational design covering governance, cost management,
security, education and knowledge sharing had become important, not only development productivity.

Members who use Claude Code heavily in their daily work collected questions in advance; several dozen
were gathered, and on the day Cherny answered twenty or more of them. The post describes the session as
a discussion driven by CyberAgent's own practical problems rather than a briefing on new features, and
notes that because parts of it were covered by an NDA or were non-public, it reports only what could be
made public. One thread of discussion was the company's goal of fully automating its development
process by 2028: which areas would be automated first over the next two to three years, and which
should remain with people to the end.

## Key Points

- The themes covered included Claude Code's future direction, AI-driven development and automation of the whole software development lifecycle inside Anthropic, the feasibility of the 2028 full-automation goal, use in PR review, security review and operations, visibility and governance of agent use in a large organization, permission, configuration and cost management at the scale of about 2,000 users, the design of `CLAUDE.md`, organizational rules, skills, loops and routines, and how engineers should be evaluated as AI use advances.
- The post values discussing Claude Code not as a tool for writing code but in terms of which stages of the whole development lifecycle to automate and how, and argues that an organization with diverse businesses and technology stacks should grow reproducible ways of use fitted to each team rather than impose one company-wide way.
- According to the session, how far an AI agent can automate work is not decided simply by the size or difficulty of the codebase but is strongly shaped by how long and how continuously a team has used it; the post concludes that distributing the tool is not enough, and that teams need to accumulate working practices and turn individual know-how into organizational assets.
- Cherny stressed keeping the harness and context minimal and making sure Claude can reach the information it needs itself, rather than loading it with detailed rules and long context.
- The post adds, in its own explanation, that giving the agent feedback loops with which to check its own work — tests, builds, screenshot comparison, logs and CI — brings it closer to stable autonomous work than having a person instruct it step by step.
- Rising token use and cost at scale should be judged as return on investment rather than as something to minimize: the post argues for making visible which stages relieve bottlenecks when automated, which teams see results and which usage patterns are reproducible, and tying that to investment decisions.
- Cherny shared an approach of taking stock of daily work, grouping similar tasks, turning manual work into skills and growing repeated work into loops or routines; the post sees this as particularly useful where many teams develop in parallel, since a review procedure, investigation procedure, pre-release check or incident first response made reusable by one team can raise standardization and quality across the organization.
- As writing code gets easier, the post argues, what matters more is defining what to build, which constraints to respect and what state counts as success; the engineer's role widens from writing code to designing purpose, constraints, verification methods and operational rules.

## Context

The post is written from inside CyberAgent, and its lessons are the company's own reading of the
session as filtered for publication. As next steps it names further work on making usage, cost,
permissions, settings and security visible at the scale of about 2,000 users, and sharing good team
practices as skills and routines, and it points to initiatives already spreading across the CyberAgent
group — visualization of AI utilization and Claude Code training for non-engineers — into which the
session's findings are to be fed through development processes, training, guidelines and operational
design.
