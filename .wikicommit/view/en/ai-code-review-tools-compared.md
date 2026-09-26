---
title: "AI code review tools compared"
lang: en
kind: comparison
review_status: pending
generated_at: "2026-09-26"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
derived_from:
  - path: .wikicommit/entity/en/SoftwareApplication/coderabbit.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/SoftwareApplication/greptile.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/SoftwareApplication/github-copilot-code-review.md
    source_commit: 918f7af409eaecc35e50dea8e21fc3277faf15bf
  - path: .wikicommit/entity/en/SoftwareApplication/codex-code-review.md
    source_commit: bcf2a6e3499612efcdde4e63a1d4d23bb9dc9e6f
  - path: .wikicommit/entity/en/SoftwareApplication/sourcery.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/SoftwareApplication/claude-code-action.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/SoftwareApplication/open-code-review.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/SoftwareApplication/codestrike.md
    source_commit: abe7dbaa9cb573068b927bda52cc565d6ba058e6
  - path: .wikicommit/entity/en/SoftwareApplication/pr-agent.md
    source_commit: abe7dbaa9cb573068b927bda52cc565d6ba058e6
  - path: .wikicommit/entity/en/SoftwareApplication/asyncreview.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/SoftwareApplication/antigravity-sdk.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/SoftwareApplication/claude-code-security-review.md
    source_commit: f948f309cb907fd940528e22bdf1a82e1e673130
  - path: .wikicommit/entity/en/SoftwareApplication/compound-engineering-plugin.md
    source_commit: b5ca703338b47ee427f9fd85de1f456b7453f357
  - path: .wikicommit/entity/en/SoftwareApplication/conductor-gemini-cli-extension.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/SoftwareApplication/devin.md
    source_commit: 20326ae2b2d3074fa7e5e75e7d6a666eb50f9daf
  - path: .wikicommit/entity/en/SoftwareApplication/open-swe.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/SoftwareApplication/unit-mesh-auto-dev.md
    source_commit: 19bc48f9255734f269436c88f52086be2c4420a5
  - path: .wikicommit/entity/en/SoftwareApplication/qoder.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/SoftwareApplication/ast-grep.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
---

This page compares eighteen tools whose pages in this wiki describe an AI reviewer of code changes as a substantial part of what they do:

- Dedicated review tools: [[SoftwareApplication/coderabbit]], [[SoftwareApplication/greptile]], [[SoftwareApplication/sourcery]], [[SoftwareApplication/pr-agent]], [[SoftwareApplication/codestrike]], [[SoftwareApplication/open-code-review]] and [[SoftwareApplication/asyncreview]]
- Review features of larger products: [[SoftwareApplication/github-copilot-code-review]], [[SoftwareApplication/codex-code-review]], [[SoftwareApplication/claude-code-security-review]], and the Code Review agent that an Alibaba Cloud guide describes for a product it calls Qoder CN, recorded on the [[SoftwareApplication/qoder]] page
- Tools that can be set up to review: [[SoftwareApplication/claude-code-action]], [[SoftwareApplication/antigravity-sdk]] and [[SoftwareApplication/devin]]
- Broader agents or workflows with a review stage: [[SoftwareApplication/open-swe]], [[SoftwareApplication/unit-mesh-auto-dev]], [[SoftwareApplication/conductor-gemini-cli-extension]] and [[SoftwareApplication/compound-engineering-plugin]]

[[SoftwareApplication/ast-grep]] appears below as a component one of them uses, not as a reviewer of its own. The Qoder page states that whether Qoder CN is Qoder under another name, a regional edition or a different product is left open, and that what the guide says about Qoder CN should not be read as established of Qoder. Everything below about that review agent is therefore attributed to Qoder CN as the guide describes it.

They differ in several ways:

- where the reviewer runs
- how much of the repository it reads
- how its noise is kept down
- how a team tells it what matters
- whether it stops at comments
- what kind of evidence stands behind what is said about it

This page sets those differences side by side. It does not rank the tools. The pages it draws on do not support ranking them either: most of what they record is each project's own account or one team's impressions.

## Where the reviewer lives

The tools reach the code under review by quite different routes.

- **A bot account or service on the pull request.** CodeRabbit posts line-level comments and review decisions under its own vendor-controlled login, `coderabbitai[bot]`. Greptile is recorded as a service that comments on pull requests and replies when consulted there.
- **A feature of the forge itself.** GitHub Copilot code review is part of [[SoftwareApplication/github-copilot]]. It can be requested manually or triggered automatically, and it is usable from GitHub.com, the GitHub CLI, GitHub Mobile and several IDEs. Its agentic capabilities run on GitHub Actions runners.
- **A coding agent's capability, enabled on the repository.** Codex Code Review is the code-review capability of [[SoftwareApplication/openai-codex]]. It is turned on for a GitHub repository, and a review can also be requested with `@codex review`.
- **A CI step that runs an agent.**
  - Claude Code Action is a GitHub Action that puts a [[SoftwareApplication/claude-code]] agent on the pull request. There it can review, diagnose CI failures and act on review comments.
  - Claude Code Security Review ships as a GitHub Action that runs when a pull request is opened and comments inline on vulnerabilities.
  - A Google codelab runs a read-only review agent built with the Antigravity SDK in a GitHub Actions workflow on each pull request, posting its findings as a comment.
  - A team at Yayoi wires Devin into GitHub Actions as a reviewer: it creates review sessions through Devin's API when a pull request is opened, updated or reopened, and Devin posts its findings as comments.
- **A command inside a coding agent.**
  - Claude Code Security Review also exists as a `/security-review` command run in Claude Code before code is committed.
  - Qoder CN's Code Review agent, as the guide describes it, is invoked in agent mode with `/code-review` or a natural-language request, scoped to the whole project, specific files, a Git diff or a pull request.
  - The Compound Engineering Plugin adds `/workflows:review` to Claude Code.
  - Conductor produces its review as a post-implementation report once a coding agent has finished its tasks.
- **A standalone command-line tool.**
  - Open Code Review is a CLI invoked as `ocr`. It reviews workspace changes, a branch range or a single commit.
  - codestrike is started with `codestrike review` against a pull request URL. It can also run as an HTTP service for CI pipelines or webhooks to call.
  - PR-Agent exposes slash commands (`/describe`, `/review`, `/improve`, `/ask`) that run either as a pull-request comment or from a CLI.
  - AutoDev's CLI runs review with `autodev review`.
- **One role of a broader agent platform.** Open SWE ships a separate Reviewer entrypoint alongside the agent that writes code. It runs read-only pull request reviews on demand or automatically.
- **A capability another agent installs.**
  - AsyncReview runs through `npx`, and other coding agents can install it as a skill.
  - Open Code Review ships plugins and a portable skill for several coding agents.
  - codestrike ships as a [[SoftwareApplication/cursor]] plugin.
  - Conductor became a plugin usable from tools other than Gemini CLI.
  - Open Code Review's delegation mode inverts the arrangement: the user's own coding agent does the review with its own model, while `ocr` handles file selection and rule resolution.

On portability across forges, PR-Agent's page lists GitHub, GitLab, BitBucket, Azure DevOps and Gitea, and a CLI, GitHub Action, Docker, self-hosted and webhook deployment. Open Code Review documents CI integration for GitHub Actions, GitLab CI, GitFlic CI and Gerrit.

## How far past the diff it reads

The pages record a spread from diff-only to repository-exploring reviewers.

- codestrike reviews the diff by default. A flag has it fetch full file content instead, which its page describes as richer but slower and more token-hungry.
- PR-Agent states that `/review`, `/improve` and `/ask` each run in a single LLM call. It credits a PR compression strategy with handling both small and large pull requests.
- AutoDev's review first collects static information: changed hunks from the Git diff, affected classes and methods located with tools such as CodeGraph, linter results, and related issues and tests. Only then does an LLM analyse it. A CodebaseInvestigatorAgent handles repository-wide investigation.
- Open Code Review's agent can read full files, search the codebase and inspect other changed files. An `ocr scan` mode reviews whole files where there is no meaningful diff.
- Copilot code review moved in March 2026 to an agentic tool-calling architecture. It explores the repository, reads linked issues and pull requests, records issues as it reads, and can keep memory across reviews.
- AsyncReview's loop generates Python code, runs it in a sandboxed REPL, has its file-fetch and search calls served from the GitHub API, and repeats before answering.
- Conductor checks new code against the project's `plan.md` and `spec.md`, and runs the relevant unit and integration tests as part of the review.
- Claude Code Security Review's command searches the codebase for potential vulnerabilities.
- Qoder CN's review scope is set by the developer's request, and the guide advises reviewing large changes module by module for finer-grained feedback.
- The Antigravity SDK review agent in the codelab is limited in two layers. A policy denies everything, then allows file-reading tools, command execution and `finish`. On top of that, a pre-tool hook rejects any command that does not start with `git`.
- Claude Code Action's depth depends on the flow a team writes. One team's flow gathers PR metadata, the issue being solved, the author, the development area and the applicable guidelines before any subagent reviews.

Not every page places its tool on this axis. The CodeRabbit, Greptile, Codex Code Review, Devin, Open SWE and Compound Engineering Plugin pages say nothing about how much surrounding code the reviewer reads. Sourcery's page says only that each chunk is expanded with the surrounding lines it needs.

## How the noise is kept down

Several tools treat unwanted comments as the main thing to engineer against, and they do it in different places.

- **Deterministic work before the model.**
  - Sourcery splits a diff into atomic chunks and drops those that heuristics show cannot affect complexity, such as a new import, without calling the LLM.
  - Open Code Review assigns file selection, bundling, rule matching and comment positioning to ordinary code rather than the model.
  - CodeRabbit uses [[SoftwareApplication/ast-grep]] under the hood for review instructions based on AST patterns. A chapter summarising a CodeRabbit article presents deterministic matching as reducing the noise and variability of generative AI alone.
- **A second pass over the comments.**
  - Sourcery sends each generated comment to another LLM request that discards it if it is too generic. Its page reports this removed most false positives in Sourcery's experiments.
  - Open Code Review has a comment-reflection module.
  - The team flow recorded on the Claude Code Action page adds a severity-evaluation subagent. It checks whether each comment is valid and not fabricated, then inline-comments only high-severity findings and suppresses anything another agent has already said.
  - Claude Code Security Review's Action applies customizable rules to filter out false positives and known issues.
  - Open SWE is described as keeping findings grounded in the diff before publishing them to GitHub.
- **Staying silent.** GitHub reports that Copilot code review surfaces actionable feedback in 71% of reviews and says nothing in the rest. It also clusters repeated instances of one pattern into a single comment.
- **Trading recall for precision.** Open Code Review states that it accepts lower recall as a deliberate trade-off favouring precision over noise.
- **Merging with deterministic findings after the model.** AutoDev merges and prioritizes lint and AI findings together into one fix plan that the user can edit.
- **Grading findings.**
  - Conductor grades its findings High, Medium or Low, each with the exact file path.
  - The Qoder CN guide describes a report sorted into errors, warnings and suggestions.

The Devin page records the problem rather than a mechanism. The Yayoi team reports off-target findings from an insufficient grasp of project context, and false positives on matters the project has deliberately accepted. It names Devin's Knowledge feature as where it intends to record such cases, a direction it states rather than an established practice.

CodeRabbit's page also records something about its comments that it does not present as a way of reducing noise. CodeRabbit tags substantive comments with headers such as Refactor suggestion, Potential issue and Nitpick, and researchers can parse those headers. The study that uses them as its measure of review content is explicit that they are self-declared rather than validated, that it imposes no severity ordering on them, and that they are not independently verified measures of issue type, correctness or code quality.

## How a team tells it what matters

The customization surfaces differ in kind, not only in degree.

| Tool | What the page records as the customization surface |
|---|---|
| Codex Code Review | Rules in root and nested [[DefinedTerm/agents-md]] files, applied to the changed files and cited in each finding |
| Copilot code review | `.github/copilot-instructions.md`, path-scoped `*.instructions.md`, `AGENTS.md` and repository agent skills, read from the head branch; MCP servers usable during review; Lite and Balanced effort levels |
| Devin | `AGENTS.md`, which the Yayoi team reports Devin refers to automatically; a review-perspective file committed to the repository; the prompt the caller assembles for each session |
| codestrike | A YAML file setting system prompt, tone, guardrails and a token budget; review personas mapped to prompt files; optional loading of CLAUDE.md, AGENTS.md and Cursor rules |
| PR-Agent | JSON-based prompting, customizable through configuration files |
| Open Code Review | Review rules matched to each file through a template engine |
| CodeRabbit | Review instructions based on AST patterns, through ast-grep rule configuration |
| Greptile | Custom rules generated automatically from the comments and reactions it receives, applied across all repositories |
| Open SWE | Repository-specific review preferences learned from historical feedback by a separate Analyzer; organization-wide review guidelines; configurable models and reasoning effort |
| Conductor | The project's `plan.md`, `spec.md`, style guides and guideline files generated during planning |
| AutoDev | A chosen review type: comprehensive, performance, security or style |
| Compound Engineering Plugin | Specialized reviewers for security, performance, architecture and complexity |
| Claude Code Security Review | A security-focused prompt; customizable rules and team security policies |
| Qoder CN (per the guide) | Business background the developer explains in the request |
| Antigravity SDK | Allow/deny policies, hooks, agent skills and a response schema in the codelab's agent |
| Claude Code Action | The review flow itself, written by the team as phases and subagents |
| Sourcery, AsyncReview | No customization surface recorded on the page |

Model choice varies along the same line.

- Copilot code review deliberately does not support switching models.
- codestrike accepts any OpenAI-compatible endpoint.
- PR-Agent names several vendors plus anything reachable through [[SoftwareApplication/litellm]].
- Open Code Review's provider and model are configurable.
- AsyncReview requires a Gemini API key.
- The Antigravity SDK authenticates against Gemini or Vertex AI, and can also run agents on local models.

## Whether it stops at comments

Most of these tools comment and leave the next step to a person. Some pages record more.

- **Fixing.**
  - AutoDev generates fixes as a patch that can be rolled back or iterated on, made by a CodingAgent.
  - Claude Code Security Review can be asked to implement a fix for each issue it finds.
  - Copilot code review can hand its suggestions to the Copilot cloud agent to open a pull request with them applied.
  - Conductor lets a track be started to work through its findings.
- **Approving.**
  - Copilot code review includes an approval assessment in every review. By default it does not count toward required approvals.
  - With Copilot approvals enabled (public preview), Copilot can submit an approving review that satisfies a required-approval rule. That approval is dismissed if new commits are pushed.
  - A team at DMM used Claude Code Action to score pull requests on four axes and approve automatically above a threshold. The page reports that the accuracy was workable but the mechanism did not become established in that team. The team's stated reason is that review is also a dialogue for sharing intent.
- **Staying read-only.**
  - Open SWE's Reviewer is read-only.
  - The Antigravity SDK review agent in the codelab is built read-only.
  - Codex Code Review's page states that the tool is an additional reviewer, not an enforcement mechanism: tests, branch protections and required approvals stay the hard gates.
  - Cognition limits Devin's pull-request review role to a first pass that catches obvious issues, saying human review remains necessary.

## What stands behind each account

The evidence behind these pages is uneven, and the pages say so.

- **Vendor documentation and announcements.**
  - Copilot code review draws on GitHub's documentation, blog and changelog.
  - Codex Code Review draws on OpenAI's announcement. OpenAI reports that in its primary eval suite, rule-guided variants recovered 98% of the required custom findings, against 58.3% for a baseline control.
  - Claude Code Security Review draws on Anthropic's announcement, which gives two vulnerabilities the Action caught in Anthropic's own code.
  - Conductor's page notes that its capabilities are Google's own description rather than measured results.
  - The Qoder CN review agent is described in an Alibaba Cloud user guide. That guide itself notes it may not reflect the product's latest features, and the Qoder page does not treat it as established of Qoder.
  - The Antigravity SDK's review use comes from a Google codelab tutorial.
- **Project READMEs.**
  - Open Code Review, codestrike, PR-Agent, AsyncReview and Open SWE draw on their own repositories.
  - Open Code Review's benchmark result is its own, on its own dataset [[Dataset/aacr-bench]], with the numbers given only in an image.
  - AsyncReview reports no evaluation.
  - codestrike describes itself as a public preview not yet meant for production.
  - Open SWE describes itself as under active development.
- **Author and book accounts.**
  - The Sourcery and ast-grep pages rest on a book chapter summarising vendor write-ups.
  - AutoDev's review is described by its own author's blog.
  - The Compound Engineering Plugin page rests on a third party's blog post recommending it.
- **Engineering blogs by teams using the tool.**
  - Greptile's page rests on one such post, and Claude Code Action's on two. Their comparative ratings are that team's impressions rather than measurements. The team in the first post runs Greptile, Claude Code Action and Copilot in parallel rather than picking one.
  - Devin's review use comes from the Yayoi team's post. Devin's page also cites Cognition's own assessment of the agent.
- **A mining study of public GitHub.** Among the accounts of review use on these pages, CodeRabbit's is the only one built on a third-party study. There CodeRabbit was the one dedicated reviewer bot with enough volume and machine-parsable labels to study. The study found its label mix differed by which agent authored the pull request, and it declines to attribute why.

The broader concept these tools instantiate is [[DefinedTerm/agentic-code-review]].
