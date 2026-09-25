---
title: "GitHub Agentic Workflows"
type: "schema:SoftwareApplication"
lang: en
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/automate-repository-tasks-with-github-agentic-workflows/'
    hash: sha256:fe960a60c7701f39e63a0ed24e1c6bf08fa8edfae0c3c9484ea13fd5fbf860e2
  - type: url
    url: 'https://docs.github.com/en/actions/tutorials/develop-agentic-workflows-in-github-actions'
    hash: sha256:eb619cf2a6199441d330e6e01a95bfeea65309f0629e2997d815df763c1b7c3b
  - type: url
    url: 'https://docs.github.com/en/copilot/how-tos/github-agentic-workflows/creating-github-agentic-workflows'
    hash: sha256:a8e56bd50a0890f7f307b8d7987d63165acf3552883dc367b139df6ca784eb6f
  - type: url
    url: 'https://github.blog/changelog/2026-02-13-github-agentic-workflows-are-now-in-technical-preview/'
    hash: sha256:3a42888c4bda0dd7a8257cbea68e434226f40b820a649da9288c35de9602287d
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
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
technical preview in February 2026; GitHub's documentation describes them as in public
preview and subject to change.

The design premise is that a maintainer describes the outcomes they want in plain Markdown,
adds it to the repository as a workflow, and a coding agent executes it inside GitHub
Actions. GitHub's stated reason for building on Actions is that it is where the necessary
infrastructure already exists for permissions, logging, auditing, sandboxed execution and
rich repository context. The documentation extends the same premise to the workflow's own
lifecycle: authoring, debugging and optimizing a workflow are themselves meant to be done by
describing what you want to a coding agent, which creates, refines and troubleshoots it.

## Capabilities

A workflow file has two parts: YAML frontmatter carrying configuration — the trigger,
permissions, tools, and allowed outputs — and Markdown instructions describing the job in
natural language. GitHub's framing is that the Markdown is the intent while the trigger,
permissions, tools and allowed outputs are spelled out up front. Each Markdown workflow has
a corresponding `.lock.yml` lock file, which is what GitHub Actions actually executes;
the `gh-aw` CLI extension compiles one from the other via `gh aw compile`. GitHub notes
that in practice workflows are usually created with the help of an interactive coding
agent, which writes the Markdown file and checks its validity for review. Running
`gh aw init` in a repository adds skills and instructions for that authoring agent, and the
documented path is to invoke an `agentic-workflows` skill with a plain-language description
(see [[HowTo/create-a-github-agentic-workflow-with-a-coding-agent]]). The documentation also
describes creating workflows in the GitHub web interface or by editing the files by hand, and
running one from the Actions tab or with `gh aw run`.

The documentation's reference for the frontmatter names four key fields: `on`, the event trigger,
in the same syntax as GitHub Actions triggers; `permissions`, the repository permissions granted to
the agent, which default to `read-all`; `safe-outputs`, the write operations the agent is allowed
to perform; and `engine`, the AI engine to use. Its example weekly issue-activity report also
declares `network` and `tools` settings, granting the agent the GitHub issues toolset. Editing a
workflow means recompiling the lock file with `gh aw compile` and committing both files.

Which coding agent runs the workflow is configurable. The announcement names Copilot CLI,
Claude Code and OpenAI Codex as engines that can be used depending on configuration; the
documentation lists Copilot CLI as the default and [[SoftwareApplication/claude-code]],
[[SoftwareApplication/openai-codex]] and [[SoftwareApplication/gemini-cli]] as alternatives,
with further engines such as an experimental one named Pi also supported. The three alternatives
each run on an API key stored as a repository secret. For Copilot, a personal repository needs a
`COPILOT_GITHUB_TOKEN` secret holding a fine-grained personal access token, while an
organization-owned repository can instead use GitHub Actions' built-in `GITHUB_TOKEN`: with
`copilot-requests: write` in the workflow's `permissions`, and an organization policy allowing
Copilot CLI to be billed to the organization, Copilot requests are billed directly to the
organization, which the documentation recommends.

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

The technical-preview changelog entry adds a few specifics to this picture: workflows are added as
Markdown files under `.github/workflows/`, and the `gh aw` CLI converts them into standard GitHub
Actions workflows; the security design includes SHA-pinned dependencies and sanitized write operations
alongside sandboxing and network isolation; the GitHub MCP Server gives native access to repositories,
issues, pull requests, actions and security, with additional tools for browser automation, web search
and custom MCP servers; and workflows can be triggered by issue and pull request events, on a schedule,
by manual dispatch, or by commands in comments. It also states that the implementation is fully open
source under the MIT license in the `gh-aw` repository.

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

Workflows can be shared between repositories. `gh aw add-wizard` (or the non-interactive
`gh aw add`, optionally pinned to a version) imports a workflow from another repository — the
documentation's example comes from `githubnext/agentics` — and records a `source:` value in its
frontmatter so that `gh aw update` can later pull upstream changes while trying to preserve local
edits. Workflows marked `private: true` cannot be imported, and the documentation advises importing
only from trusted sources and reviewing what a workflow does before adding it.

For examples, the changelog points to Peli's Agent Factory, which it says showcases over 50
specialized agentic workflows for different use cases.

Running a workflow uses a coding agent at runtime and so incurs billing cost. The
announcement is described in [[BlogPosting/automate-repository-tasks-with-agentic-workflows]].
