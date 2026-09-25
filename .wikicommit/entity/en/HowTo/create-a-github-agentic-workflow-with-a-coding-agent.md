---
title: "Create a GitHub Agentic Workflow with a coding agent"
type: "schema:HowTo"
lang: en
tags: [agents, ci-cd, agent-tooling]
sources:
  - type: url
    url: 'https://docs.github.com/en/actions/tutorials/develop-agentic-workflows-in-github-actions'
    hash: sha256:eb619cf2a6199441d330e6e01a95bfeea65309f0629e2997d815df763c1b7c3b
  - type: url
    url: 'https://docs.github.com/en/copilot/how-tos/github-agentic-workflows/creating-github-agentic-workflows'
    hash: sha256:a8e56bd50a0890f7f307b8d7987d63165acf3552883dc367b139df6ca784eb6f
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "GitHub's documented path for authoring a GitHub Agentic Workflow by describing it in natural language to a coding agent, which writes the Markdown workflow, compiles its lock file, and hands both back for review before they are committed."
  tool: ["GitHub CLI", "gh aw extension", "a supported coding agent CLI"]
---

This procedure sets up a repository for [[SoftwareApplication/github-agentic-workflows]] and then
has a coding agent write, compile and commit a workflow from a plain-language description. GitHub's
tutorial walks it through with an automated pull request reviewer that checks whether changes are
adequately tested, and a companion how-to walks through a daily or weekly repository activity report
delivered as an issue. GitHub notes that Agentic Workflows are in public preview and subject to
change.

## Prerequisites

- A repository with GitHub Actions enabled, to which you have write access.
- GitHub CLI 2.0.0 or later, installed and authenticated; the documentation's login command is
  `gh auth login --scopes repo,workflow`.
- Access to a supported coding agent and its credential — the tutorial names Claude Code, OpenAI
  Codex, Google Gemini CLI and Copilot CLI.

## Steps

1. Install the Agentic Workflows extension for GitHub CLI: `gh extension install github/gh-aw`.
   From GitHub CLI 2.90.0, running any `gh aw` command prompts to install it if it is missing.
2. Choose the engine that will run the workflow and make its credential available. For
   [[SoftwareApplication/claude-code]], [[SoftwareApplication/openai-codex]] or
   [[SoftwareApplication/gemini-cli]], store the corresponding API key (`ANTHROPIC_API_KEY`,
   `OPENAI_API_KEY` or `GEMINI_API_KEY`) as a repository secret under Settings → Secrets and
   variables → Actions. Copilot CLI is the default engine; in an organization-owned repository it
   needs no separate secret when `copilot-requests: write` is added to the workflow's frontmatter
   `permissions`, while a personal repository needs a `COPILOT_GITHUB_TOKEN` secret holding a
   fine-grained personal access token with Copilot Requests set to Read. Organization billing also
   requires an organization administrator to enable the "Allow use of Copilot CLI billed to the
   organization" policy in the organization's Copilot policy settings.
3. From the repository root, run `gh aw init`. This adds skills and instructions that help a coding
   agent create and edit workflows.
4. Start a coding agent session in the repository — for example Claude Code, OpenAI Codex, Gemini
   CLI, [[SoftwareApplication/github-copilot-cli]] or VS Code agent mode.
5. Invoke the `agentic-workflows` skill with a description of the workflow, e.g.
   `/agentic-workflows create a pr reviewer that ensure the changes are tested.` The agent creates a
   workflow Markdown file in `.github/workflows/`, compiles the corresponding `.lock.yml` GitHub
   Actions workflow, and asks you to review and commit both.
6. Review the generated workflow, then ask the agent to commit and push the files.
7. Run it. A workflow can be triggered from the repository's Actions tab or with
   `gh aw run YOUR-WORKFLOW-NAME`; the example reviewer triggers on pull requests, so opening or
   updating one runs it, and on completion it leaves a pull request review noting whether the
   changes include enough tests.

## Notes

- The same conversational approach is how the workflow is maintained afterwards: GitHub suggests
  asking the agent to refine the review criteria, add checks, or debug a failed run in natural
  language.
- To update a workflow by hand, edit its Markdown file in `.github/workflows/`, run `gh aw compile`
  to refresh the lock file, commit and push both files, and verify the GitHub Actions checks on a
  pull request.
- Other engines beyond the four above, such as an experimental one called Pi, are listed in the
  project's own authentication reference.
