---
title: "AI-assisted code review with Antigravity CLI and SDK"
type: "schema:HowTo"
lang: en
tags: [code-review, agent-skills, ci, security]
sources:
  - type: url
    url: 'https://codelabs.developers.google.com/agy-cli-sdk-code-review'
    hash: sha256:283b349fe5d611bf6d0c0d2b5ac36978aaa667fac020078c52e2bf0412ba54ae
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Google Codelabs procedure for reviewing AI-generated changes with Antigravity: interactively with the Antigravity CLI and an installed code-review agent skill, and automatically on every pull request with a read-only review agent built on the Antigravity SDK and run as a GitHub Action."
  tool: ["[[SoftwareApplication/antigravity-cli]]", "[[SoftwareApplication/antigravity-sdk]]", "GitHub Actions", "gh CLI", "uv"]
---

This procedure, from a Google Codelabs tutorial, sets up two ways of using Antigravity as the reviewer
of code an agent wrote: an interactive review of a feature branch with the
[[SoftwareApplication/antigravity-cli]], and an automated review of every pull request by an agent
built on the [[SoftwareApplication/antigravity-sdk]] and run in CI. The tutorial's premise is that in
[[DefinedTerm/vibe-coding]] the developer approves code rather than writing it, so functional code can
be merged without a thorough security review — and reading every line would give up the speed that
motivated vibe coding in the first place.

## Prerequisites

- A Google Cloud account and a GitHub account, with basic familiarity with a terminal, version control and CI/CD.
- A repository to review. The tutorial uses a fork of a demonstration CRM app with two feature branches that deliberately contain vulnerabilities — SQL built by string concatenation, missing input validation, hard-coded admin credentials, unauthenticated admin endpoints and path-traversal risk.
- The Antigravity CLI (`agy`), installed and authenticated; the tutorial uses Cloud Shell, where it is preinstalled.
- A Gemini API key for the SDK agent.

## Steps

### Interactive review with the CLI

1. Check out the feature branch to be reviewed.
2. Install a code-review agent skill (see [[DefinedTerm/agent-skills]]) into the workspace with `npx skills add addyosmani/agent-skills --skill code-review-and-quality -y`. It lands in `.agents/skills/`, so it can be committed with the repository and shared by everyone working on it, CI included.
3. Launch the CLI and confirm the skill is listed with `/skills`. The tutorial launches with `--dangerously-skip-permissions` to save time and warns that the flag permits every action.
4. Ask the agent to review the diff between `main` and the current branch, write its findings and a fix plan to `code_review.md`, and not apply fixes yet. The agent picks up the relevant skill on its own.
5. Read the findings and the plan, then ask the agent to apply the proposed fixes.
6. Run the app to confirm it still works, iterating with the agent if not, then commit.

### Automated review with the SDK

1. Check out the branch to be reviewed, create a Python project for the review agent with `uv`, and add the `google-antigravity` package.
2. Install the same review skill and copy it into the agent's project, so the SDK can load it through its `skills_paths` setting.
3. Write the review agent. The tutorial's agent denies every tool by default and allows only file-reading tools, `run_command` and `finish`; a pre-tool-call hook further blocks any command that does not start with `git`; a post-tool-call hook logs each tool result for audit; the system instruction says it never modifies files; and a response schema makes it return structured findings (file, line, severity, category, description, proposed fix), which it writes as Markdown to `code_review.md`.
4. Run the agent locally against the branch with the API key in the environment, and check the output.
5. Add a GitHub Actions workflow that runs on pull requests being opened or updated, checks out full history so the agent can run `git diff main...HEAD`, runs the agent, and posts `code_review.md` as a pull-request comment.
6. Store the API key as a repository secret named `GEMINI_API_KEY`, push the branch, and open a pull request against your own fork; the workflow posts the review as a comment.

## Notes

- The tutorial describes agent skills as declarative Markdown files that become slash commands once installed, portable across agents and shareable through Git. Workspace skills for the Antigravity CLI live in `.agents/skills/`, global ones in `~/.gemini/config/skills/`. The skill it installs reviews on five axes — correctness, readability, architecture, security and performance — and labels findings by severity. The tutorial names it as an example, not the only option.
- Its stated reason for using a skill at all is repeatability: without one the CLI can still review, but relies on general training knowledge and may apply inconsistent criteria between sessions.
- Enforcement in the SDK agent sits at two layers — policies at the framework level and the hook as a second check — and the tutorial scopes the review to the branch's diff rather than the whole codebase.
- The workflow's trigger can be narrowed, for example to specific paths, or switched to a comment command such as `/review` for on-demand review.
- When cleaning up, the tutorial warns not to merge the second feature branch's pull request, since it still contains the unpatched vulnerable code.
