---
title: "GitHub Agentic Workflows"
type: "schema:SoftwareApplication"
lang: en
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/automate-repository-tasks-with-github-agentic-workflows/'
    hash: sha256:fe960a60c7701f39e63a0ed24e1c6bf08fa8edfae0c3c9484ea13fd5fbf860e2
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"
tags: [agents, continuous-ai, agent-tooling, guardrails, agent-safety]

properties:
  description: "GitHub's system for repository automation written as plain Markdown and executed by coding agents inside GitHub Actions, with read-only permissions by default and writes routed through pre-approved safe outputs."
  applicationCategory: "Repository automation"
  author: "[[Organization/github]]"
  featureList: "Markdown workflow files compiled to GitHub Actions lock files; read-only default permissions; safe outputs for write operations; sandboxed execution, tool allowlisting and network isolation; pluggable coding agent engines"
---

GitHub Agentic Workflows are automated, intent-driven repository workflows that run in
GitHub Actions, are authored in plain Markdown, and are executed by coding agents. They
began at GitHub Next as an investigation into what repository automation with strong
guardrails looks like in the era of AI coding agents, and are described as a collaboration
between GitHub, Microsoft Research and Azure Core Upstream. GitHub announced them in
technical preview in February 2026.

The design premise is that a maintainer describes the outcomes they want in plain Markdown,
adds it to the repository as a workflow, and a coding agent executes it inside GitHub
Actions. GitHub's stated reason for building on Actions is that it is where the necessary
infrastructure already exists for permissions, logging, auditing, sandboxed execution and
rich repository context.

## Capabilities

A workflow file has two parts: YAML frontmatter carrying configuration — the trigger,
permissions, tools, and allowed outputs — and Markdown instructions describing the job in
natural language. GitHub's framing is that the Markdown is the intent while the trigger,
permissions, tools and allowed outputs are spelled out up front. Each Markdown workflow has
a corresponding `.lock.yml` lock file, which is what GitHub Actions actually executes;
the `gh-aw` CLI extension compiles one from the other via `gh aw compile`. GitHub notes
that in practice workflows are usually created with the help of an interactive coding
agent, which writes the Markdown file and checks its validity for review.

Which coding agent runs the workflow is configurable: GitHub names Copilot CLI, Claude Code
and OpenAI Codex as engines that can be used depending on configuration.

GitHub describes the security architecture as defense-in-depth, aimed at unintended
behaviours and at prompt-injection attacks. Workflows run with read-only permissions by
default, and write operations require explicit approval through
[[DefinedTerm/safe-outputs]], which map to pre-approved, reviewable GitHub operations such
as creating a pull request or adding a comment. Sandboxed execution, tool allowlisting and
network isolation are described as keeping agents within controlled boundaries. GitHub
contrasts this with the alternative of running a coding agent CLI directly inside a
standard Actions YAML workflow, which it says often grants more permission than a given
task requires.

GitHub states that pull requests are never merged automatically and that humans must always
review and approve.

## Adoption & Ecosystem

GitHub presents the system as the vehicle for [[DefinedTerm/continuous-ai]] — its term for
the integration of AI into the SDLC, which it describes as enhancing automation and
collaboration similarly to continuous integration and continuous deployment practices. The categories it gives as newly practical are continuous triage, continuous
documentation, continuous code simplification, continuous test improvement, continuous
quality hygiene, and continuous reporting. GitHub is explicit that these augment rather
than replace CI/CD: they do not replace build, test or release pipelines, and their use
cases are said largely not to overlap with deterministic CI/CD workflows.

Published design patterns include ChatOps, DailyOps, DataOps, IssueOps, ProjectOps,
MultiRepoOps and Orchestration. GitHub's practical guidance is to start with low-risk
outputs such as comments, drafts or reports before enabling pull request creation; to begin
with goal-oriented code improvements such as refactoring, test coverage or simplification
rather than feature work; to be specific about what a good report looks like; to keep
humans in the broader loop even though the agent operates in an autonomous sub-loop; and to
treat the workflow Markdown as code, reviewing changes and evolving it intentionally.

Running a workflow uses a coding agent at runtime and so incurs billing cost. The
announcement is described in [[BlogPosting/automate-repository-tasks-with-agentic-workflows]].
