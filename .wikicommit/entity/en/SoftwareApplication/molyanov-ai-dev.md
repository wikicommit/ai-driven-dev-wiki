---
title: "molyanov-ai-dev"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, agent-skills]
sources:
  - type: url
    url: 'https://habr.com/ru/articles/1022050/'
    hash: sha256:0222b5099a19ac673cf8833d17cfddba8ad4a29c2412b9641b0841aaa1969784
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "An agentic development framework for Claude Code, published on GitHub by Pavel Molyanov, consisting of skills, commands and reviewer subagents. It takes a feature from an interview-driven user spec through a tech spec and atomic tasks to test-first implementation by agents."
  applicationCategory: "Agentic development framework for Claude Code"
  featureList: "Interview-driven user-spec creation; tech-spec writing and decomposition into atomic tasks; reviewer subagents at each stage; do-task and do-feature implementation modes; agent-maintained project documentation updated with a /done command; skill-master and skill-tester skills for building and testing skills"
---

molyanov-ai-dev is a framework for agentic development with
[[SoftwareApplication/claude-code]], published on GitHub as a set of
[[DefinedTerm/agent-skills]], commands and reviewer subagents. Its author describes himself
as a non-developer with a background in marketing and management. He built it over about half
a year of making small projects in Claude Code, adding skills and reviewer agents that look
for bugs and vulnerabilities along the way.

The framework targets people with a technical mindset but no real programming experience. In
it, Claude Code takes the roles of developer, DevOps, security specialist and technical
writer, while the human acts as product owner. The human decides what to build, describes how
it should behave in different scenarios and edge cases, sets tasks, and tests the result at
the end. Development runs in stages: planning, formulating tasks, then doing them. Each stage
has a skill instructing the agent how to behave, plus reviewer subagents that check the work
before the next stage begins.

## Capabilities

- **User spec**: the human describes what they want, and the agent runs an interview mode,
  asking dozens of questions about behaviour, failure cases and trade-offs. It also researches
  the codebase, searches the web and reads documentation. The result is a plain-language
  document the human can read, understand and correct.
- **Tech spec and tasks**: from the approved user spec, an agent writes a tech spec. The tech
  spec covers what functions to write, which files to change and how to test, and goes
  through several rounds of review; the author puts a typical one at 300-400 lines. A second
  agent decomposes it into atomic tasks. Each task states what to change, which documentation
  to study, which tests to write, which skills to use and what the acceptance criteria are.
  Reviewers check the tasks for soundness, vulnerabilities and consistency with both specs.
- **Implementation**: all work follows test-first development, with tests before code. The
  author says the reverse order leads the agent to fit tests to its existing work, errors
  included. In **do-task** mode an agent takes one task, loads the skills it names, checks
  itself against the acceptance criteria, runs tests and then calls reviewers, typically a
  code reviewer and a security audit. Each task gets a fresh chat. **do-feature** is a one-shot
  mode built on Claude Code's [[DefinedTerm/agent-teams]]. A lead agent starts a developer
  agent for each open task, then reviewer agents, and finally a QA pass over the whole feature.
- **Project documentation**: agents maintain a project knowledge base covering purpose, tech
  stack, architecture and deployment. A first version is built from the interview, and after
  each feature a `/done` command has the agent go through commits and logs and update it.
- **Skills for building skills**: a skill-master skill gives instructions for writing working
  skills and their reviewer subagents. A skill-tester skill invents test tasks for a skill, runs
  an agent on them, and records how it performs, with the feedback used to revise the skill.

## Adoption & Ecosystem

Installation is either by giving Claude Code the GitHub link and asking it to install the
framework, or by copying its contents into the user's `.claude` folder, renaming anything that
clashes with existing skills or subagents. The author developed the framework over about a dozen
small projects built in Claude Code: personal tools, an internal RAG agent for his team, and a
couple of monetised projects, one of them a bot. In his experience do-feature works for simple tasks, and he once left agents
coding unattended for eight hours with a working result. For complex work on projects with live
users he prefers do-task, checking each task by hand.
