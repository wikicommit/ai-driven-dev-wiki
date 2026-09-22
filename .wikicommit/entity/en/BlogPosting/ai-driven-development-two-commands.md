---
title: "AI駆動開発を2コマンドで組織標準に ── Claude Code × Codexで設計からテストまで"
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, agentic-code-review, ai-adoption]
sources:
  - type: url
    url: 'https://techblog.zozo.com/entry/ai-development-two-commands'
    hash: sha256:58353a3fded13879de422c6b7cc6aff4012808394657a717d42726f5f81140df
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An account from ZOZO's core-systems division of collapsing its AI-driven development process into two standard commands — one that builds a design document and progress table from a Jira ticket, and one that resumes work by reading that table against the Git state. It argues that what to delegate should be decided from the direction of information transformation rather than from current model capability, and pairs Claude Code with Codex in a three-round critical dialogue for quality-critical work."
  author: "田中秀明"
  datePublished: "2026-06-08"
  publisher: "[[Organization/zozo]]"
---

The post opens with a diagnosis the author is careful to distinguish from the obvious one: the problem at [[Organization/zozo]] was not that engineers were failing to use AI, but that each person's prompts, review criteria and sense of how much to delegate had diverged. Advanced users were changing how they worked, while newcomers could not tell at which stage, or how far, to hand work to an agent — so the organization's floor stayed where it was even as its ceiling rose. The author's stated aim is to avoid both delegating too much, where unverified output carries a misread requirement into the design, and delegating too little, where investigation, design write-up, task decomposition and review-point extraction stay manual.

The answer the division settled on is two commands rather than one per stage. Splitting by stage would make each command's responsibility clear at the cost of forcing the user to decide which one applies; collapsing everything into one command fails on the first run of a ticket, because no design document or progress table exists yet for the agent to locate itself in. So `/dev-init` exists only to create that initial state — parsing the Jira ticket, dispatching sub-agents to investigate the codebase and Confluence in parallel, and emitting a Confluence design document plus a local Markdown progress table that doubles as the detailed design — and `/dev-resume` carries everything after it, reading the table and reconciling it against `git status` and `git diff` to propose where to pick up.

Underneath both sits an argument about what to delegate, and a second about how to check it. The delegation argument takes the model as a converter that returns the most probable output given its input, training data and context, and sorts work by the direction of information transformation rather than by what a given model can do this month. The checking argument is that a single model reviewing its own output gives weak independence of perspective, so quality-critical runs route the design and the diff through Codex in the [[DefinedTerm/critical-dialogue-review]] loop the post describes.

## Key Points

- The stated failure mode of early AI adoption is not non-use but per-person divergence: prompts, judgment criteria, the information handed to the agent and the review criteria all differ, so design documents, progress tracking and verification criteria accumulate in inconsistent formats and the knowledge does not become reusable.
- What to delegate is decided from the direction of information transformation, not from current model performance, on the stated grounds that a capability-based line goes stale as models change. Concrete-to-abstract work (extracting issue patterns from incident reports, review points from a diff, gaps and contradictions from a specification) and same-level conversion (Jira ticket to design document, design document to task list, diff to review comments) go to the agent; abstract-to-concrete work (shaping requirements into a plan, choosing between implementation options, prioritizing under a deadline) stays with people, who hold final responsibility.
- The two-command split is presented as a concession to a technical constraint rather than a design principle — the author states the intent is to keep entry points as few as possible, and that `/dev-init` exists only because the agent cannot locate itself before a Git-managed progress table has been emitted.
- The progress table is deliberately detailed enough to resume from on its own, carrying the ticket background, acceptance criteria, task list, target files, implementation detail, test criteria, open issues and a work log. The author's stated point is that context for continuation belongs in a file rather than in conversation history, which is lost across an interruption, an overnight break or a handover to another member.
- Building a division-specific command rather than adopting a general-purpose orchestration tool is argued as a trade of generality against fit — the stated limit of a general tool is embedding ZOZO's Jira, Confluence, design-document granularity, progress tracking and front-end verification into the daily development path. The user-facing surface is held at two commands while the prompts, Skills and integrations behind them are updated.
- Front-end changes are routed to Playwright MCP for DOM, console-error and network-error checks, with automatic repair attempted at most twice; where Playwright MCP is not configured the step is skipped rather than blocking the flow, which the author gives as a requirement for anything used as an organizational standard.
- Prompts and diffs sent to Codex are constrained to be checked for secrets such as API keys, passwords and tokens — the author's stated conclusion being that standardizing a cross-vendor AI integration means building the security operating rules into the command, not only the quality ones.
- The author presents the standard command as an educational device as well as an efficiency one: running it exposes which judgments the process requires, and the stated expectation is that repeated use builds a feel for which stages to delegate that eventually works without the framework.
- Reported limits are that the Codex pairing costs more time and money than running Claude Code alone and is not worth using on every task; that unresolved findings after the cycle cap must return to a person, which the author frames as a boundary the standard command must not cross rather than a failure; that Playwright verification depends on a URL hint, authentication, test data and a stable environment being in place; and that effect measurement — design write-up time, lead time to implementation, review quality, rework counts — is still outstanding. These are the author's own account of one division's deployment, not measured results.

## Context

The post sits alongside other firsthand accounts in this wiki of organizations standardizing agent use rather than leaving it to individuals, and it takes an explicit position against one common alternative: letting each team build its own workflow, which the author argues raises local autonomy while leaving the organizational floor untouched. Its closest structural neighbour is the argument for cross-model review — the same reasoning that makes [[DefinedTerm/n-version-programming]] attractive, applied to criticism rather than generation, and distinct from the observational sense in which [[DefinedTerm/closed-loop-ai-review]] describes AI on both sides of a pull request.

The author is explicit that the boundary drawn here is not fixed. Planning, requirement shaping, prioritization and customer-value judgment are described as the author's own current view of what people should lead, with the expectation that model capability will move the line and the standard command's design will have to be revisited with it. An extension to upstream requirement-definition work is noted as under consideration, with the caveat that upstream work is more abstract-to-concrete and so cannot be delegated on the same terms.
