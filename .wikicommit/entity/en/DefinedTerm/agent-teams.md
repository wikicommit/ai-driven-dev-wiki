---
title: "Agent Teams"
type: "schema:DefinedTerm"
lang: en
tags: [multi-agent, agentic-coding, agent-architecture, orchestration]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/code-agent-orchestra/'
    hash: sha256:399fcd256a0dea0d4dc0841558f7f17cf41a9b447bc6bbc5adfbaf8728e9c557
  - type: url
    url: 'https://www.anthropic.com/engineering/building-c-compiler'
    hash: sha256:76ec31b147cb595b08d33f9b46ece5a385276d3165f3c8ca4ab62600055ab111
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An experimental Claude Code feature for true parallel agent execution, adding the coordination primitives plain subagents lack: a shared task list with dependency tracking and file locking, and peer-to-peer messaging between teammates."
  termCode: ""
  inDefinedTermSet: ""
---

Agent Teams is an experimental [[SoftwareApplication/claude-code]] feature for running several coding agents in true parallel, described in [[BlogPosting/the-code-agent-orchestra]]. What distinguishes it from plain [[DefinedTerm/subagents]] is coordination: where a subagent arrangement leaves the parent to manage the dependency graph by hand and gives the children no way to talk to each other, Agent Teams supplies a shared task list with dependency tracking, peer-to-peer messaging between teammates, and file locking. It is enabled by setting the environment variable `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`.

## Usage

The architecture as described has three layers. A **team lead** decomposes the work, creates the task list, and synthesises results. A **shared task list** sits in the middle, holding tasks with statuses — pending, in_progress, completed, blocked — along with dependency tracking and file locking. **Teammates** at the bottom are independent Claude Code instances, each with its own context window, running in tmux split panes.

Two mechanisms do the coordinating. Teammates self-claim tasks from the shared list, and when one marks a task complete, any task blocked on it flips automatically to pending for another teammate to pick up; file locking prevents two teammates editing the same file at once. Separately, teammates message each other directly rather than through the lead — the worked example is a backend agent sending a frontend agent the API contract it just settled — which the account argues is what keeps the lead from becoming a coordination bottleneck. The lead is notified automatically when a teammate goes idle, and `Ctrl+T` toggles a visual overlay of the task list.

Osmani's stated operating guidance is that three to five teammates is the sweet spot, with token costs scaling linearly with team size, and that three focused teammates outperform five scattered ones. He describes two reliability additions on top: a hard `MAX_ITERATIONS=8` per teammate with a forced reflection prompt before each retry ("What failed? What specific change would fix it? Am I repeating the same approach?"), which he reports substantially cuts stuck agents; and a dedicated read-only `@reviewer` teammate at a ratio of roughly one per three or four builders, restricted to lint, test and security-scan tools and triggered automatically on every task completion, so that the lead only ever sees reviewed code. Requiring teammates to write a plan the lead approves before implementing is presented as the gate for risky tasks, on the reasoning that fixing a bad plan is cheaper than fixing bad code.

### A second, differently-built thing under the same name

The name is also used for a research prototype that shares the goal but almost none of the mechanism. In [[BlogPosting/building-a-c-compiler-with-parallel-claudes]], [[Person/nicholas-carlini]] describes "a new approach to supervising language models that we're calling 'agent teams'," in which multiple Claude instances work in parallel on a shared codebase without active human intervention. The two arrangements should not be read as descriptions of one system.

Where the Claude Code feature supplies a team lead, a shared task list with dependency tracking, peer-to-peer messaging and file locking, that prototype deliberately supplies none of them. Each agent runs in its own Docker container against a bare git repository; a task is claimed by writing a lock file into a `current_tasks/` directory, and git's own synchronisation resolves a collision by forcing the second claimant elsewhere. The report states plainly that no other method of inter-agent communication was implemented, that no process for managing high-level goals is enforced, and that no orchestration agent is used — each agent decides for itself what to work on, generally taking the next most obvious problem. Its author calls it a very early research prototype.

The two also differ in what the human is expected to do. The feature-level arrangement assumes an operator present at plan-approval and review gates; the prototype exists specifically to remove the operator, on the observation that existing scaffolds stop and wait for input on a long problem. That report's own conclusion about the trade is not that coordination machinery is unnecessary, but that the environment — tests, feedback, logs — is what has to carry the coordination burden instead.

## Related Terms

Agent Teams is the coordinated end of the same axis as [[DefinedTerm/subagents]], which provide context isolation and parallel execution but no shared state or peer communication, and it is one concrete implementation of [[DefinedTerm/multi-agent-orchestration]]. The quality gates it is paired with — hooks and an [[DefinedTerm/agents-md]] file for compound learning — are the same ones that answer the [[DefinedTerm/verification-bottleneck]].
