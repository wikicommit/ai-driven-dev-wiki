---
title: "GitHub Copilot coding agent"
type: "schema:SoftwareApplication"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/coding-agents-manager/'
    hash: sha256:fc697c3fcc830075a1a6b6751a1f242d4b6ff4ea9a385c1ec60a0c6f8a6e50a1
  - type: url
    url: 'https://arxiv.org/pdf/2508.11126'
    hash: sha256:d8a0f4c103987a46e21f37fca41b5ebfa795945e9c798921c4fdfbfc18bd9346
  - type: url
    url: 'https://github.blog/news-insights/product-news/github-copilot-meet-the-new-coding-agent/'
    hash: sha256:f3a6917c79f2f70870a12536be1e700c8b33381be9f7cfe35243aba5ec7dab46
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/from-idea-to-pr-a-guide-to-github-copilots-agentic-workflows/'
    hash: sha256:d26a28f8e99d98794a771d2e9f313c93e3141162781714ff1bfd49653195fa0b
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "GitHub's asynchronous background coding agent: assign it a GitHub issue and it works on GitHub Actions compute, pushing commits to a draft pull request and iterating as a human comments on it."
  applicationCategory: "Agentic coding tool"
  featureList: "Assigned by issue assignment; runs on GitHub Actions; opens a draft pull request; session logs; MCP server configuration; image input from issues; default branch, approval and network policies"
  author: "[[Organization/github]]"
---

GitHub Copilot coding agent is GitHub's asynchronous background coding agent. Osmani describes it as
framing itself as a background agent that opens a draft pull request, works in the background, and
then requests review, where a human can comment and have it iterate.

GitHub announced it in May 2025 (see
[[BlogPosting/github-copilot-meet-the-new-coding-agent]]) with the delegation interface as its
central idea: one or more GitHub issues are assigned to Copilot the same way they would be assigned
to a team member — from github.com, GitHub Mobile or the GitHub CLI — and the agent takes it from
there. It can also be asked to open a pull request from Copilot Chat on GitHub or in VS Code.

## Capabilities

- Works on a task asynchronously in the background rather than requiring a developer to pair with it
  in real time.
- Opens a draft pull request as its unit of output.
- Requests review and iterates on a human's comments.
- On being assigned an issue it reacts with an eyes emoji, then boots a virtual machine, clones the
  repository, configures the environment, and analyses the codebase with retrieval augmented
  generation powered by GitHub code search. It pushes changes to the draft pull request as git
  commits and updates that pull request's description as it works.
- Its reasoning and validation steps are exposed in session logs, which GitHub presents as the way
  to trace decisions and spot problems.
- [[DefinedTerm/model-context-protocol]] servers configured in a repository's settings give it
  access to data and capabilities outside GitHub, GitHub's own MCP server included.
- It reads images attached to the issues assigned to it, so a screenshot of a bug or a mockup of a
  feature can form part of the task.
- It incorporates context from related issue and pull request discussions and follows custom
  repository instructions.
- A GitHub developer advocate's walkthrough ([[BlogPosting/from-idea-to-pr]]) gives the sequence
  after assignment as: create a branch; start a new session, first configuring a development
  environment if the repository has a `copilot-setup-steps.yml`; review the task, explore the
  codebase and form a plan; use any custom instructions as context (the example requires
  `npm run lint` and `npm run test` to pass before committing); and open a draft pull request for
  review. Feedback posted as a pull request comment starts another session in which it works on
  the requested changes.
- The same walkthrough contrasts it with Copilot agent mode, which works synchronously alongside
  the developer in the editor, whereas the coding agent works on its task asynchronously.
- A survey on AI agentic programming describes a "GitHub Copilot Agent" — without saying which
  Copilot product it means — as able to hold a conversation across multiple steps, remember earlier function names, and build a complete module through back-and-forth
  iterations between agents — contrasted in the survey with single-turn tools such as classic
  [[SoftwareApplication/github-copilot]], which do not preserve state between interactions.
- That same survey catalogues a subset of the tools it says the "GitHub Copilot agent" supports, spanning
  compilers (gcc, clang), debuggers (gdb, pdb), test frameworks (pytest, Jest), linters (eslint,
  black), version control (git), build systems (make, npm), package managers (pip, cargo) and
  language servers (pyright, tsserver).
- GitHub states it is strongest on low-to-medium complexity tasks in well-tested codebases — adding
  features, fixing bugs, extending tests, refactoring, improving documentation. This is GitHub's own
  scoping claim rather than a measured result.

The walkthrough pairs it with drafting the issue itself with Copilot — a natural-language prompt
turned into an issue with a title, acceptance criteria and pointers to the files to change — and
its advice for delegation is to keep issues tightly scoped, provide acceptance criteria rather than
assume the agent knows the intent, review its changes as carefully as any other pull request before
running or merging them, and expect to iterate rather than get the result right first time. This is
one practitioner's guidance from a demo, not a measured result.

## Security & Controls

GitHub's stated design goal is that adding the agent to a team should not require relaxing the
repository's existing controls, and it describes four policies applied by default: the agent may
push only to branches it created, leaving the default branch and human-created branches untouched;
the developer who asked the agent to open a pull request cannot approve it, so any required-review
rule is honored; the agent's internet access is limited to a customizable trusted list of
destinations; and GitHub Actions workflows do not run without human approval. Existing repository
rulesets and organization policies are said to apply as well.

The compute layer is GitHub Actions, which GitHub chose on grounds of scale — it describes Actions,
introduced in 2018, as the largest CI/CD ecosystem in the world, with over 25,000 actions in the
GitHub Marketplace and more than 40 million jobs run every weekday.

## Adoption & Ecosystem

At announcement it was available to Copilot Enterprise and Copilot Pro+ customers and was enabled
per repository; for Copilot Enterprise users, an administrator also had to turn on a policy.

Osmani groups it with other cloud agents — Claude Web, Codex, and Jules — as tools explicitly
positioned for parallelizable, sandboxed tasks that write code, run commands, and propose changes
for review, and reports that GitHub previewed "Agent HQ," a control plane for coordinating
multiple third-party coding agents in one place, including running them in parallel on the same
tasks to compare outputs, as part of a broader move toward "mission control" dashboards for
managing multiple agents rather than one.
