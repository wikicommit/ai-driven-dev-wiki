---
title: "Multi-agent orchestration patterns compared"
lang: en
kind: comparison
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
derived_from:
  - path: .wikicommit/entity/en/DefinedTerm/manager-pattern.md
    source_commit: 7b07912e0ef7183c203dba9eea44e8052dcec715
  - path: .wikicommit/entity/en/DefinedTerm/decentralized-pattern.md
    source_commit: 7b07912e0ef7183c203dba9eea44e8052dcec715
  - path: .wikicommit/entity/en/DefinedTerm/planner-worker-model.md
    source_commit: b0cc6ca63c7e8c23683ba90cc3b5cf0b4690d315
  - path: .wikicommit/entity/en/DefinedTerm/planner-executor-reviewer.md
    source_commit: c6b8c68a8b3e34ab51b855aeb44d0daa53497505
  - path: .wikicommit/entity/en/DefinedTerm/sub-agent-architecture.md
    source_commit: 86e16a2d50882353cc91ba7116891cec9c627c63
  - path: .wikicommit/entity/en/DefinedTerm/agent-teams.md
    source_commit: b5ca703338b47ee427f9fd85de1f456b7453f357
  - path: .wikicommit/entity/en/DefinedTerm/three-layer-agent-orchestration.md
    source_commit: 2d31d66aac2a2bd64ef42b2343e0c9c19e1f422d
  - path: .wikicommit/entity/en/DefinedTerm/llm-based-multi-agent-system.md
    source_commit: 4b83a0390f0437f8f63f9399a1db3e12e1ace784
  - path: .wikicommit/entity/en/BlogPosting/code-agent-orchestra.md
    source_commit: 09b655594ff0cebcc127385c76c7c935da284a27
---

This wiki records several ways of dividing work among more than one LLM agent, each written up from a different source: a vendor guide, a vendor's engineering posts, a practitioner's talk, one team's production system, and a review of the research literature. They overlap in vocabulary — "orchestrator", "planner", "worker", "reviewer" recur — but they differ in where control sits, what passes between agents, why the work is split at all, and what evidence stands behind each account. This page sets them side by side so those differences are visible. It does not rank the patterns or recommend one.

## The patterns side by side

| Pattern | Where this wiki's account comes from | Roles | How work passes between agents |
|---|---|---|---|
| [[DefinedTerm/manager-pattern]] | OpenAI's guide to building agents | A central manager and specialist agents | The manager calls each specialist as a tool; the result comes back to the manager, which keeps talking to the user |
| [[DefinedTerm/decentralized-pattern]] | The same OpenAI guide | Peer agents, often starting from a triage agent | A one-way handoff transfers execution and conversation state; the receiving agent takes over the interaction |
| [[DefinedTerm/sub-agent-architecture]] | Anthropic's engineering posts and documentation, plus adopting teams and a handbook chapter | A main or lead agent and sub-agents | Each sub-agent works in a fresh context and returns a condensed summary to the lead |
| [[DefinedTerm/agent-teams]] | Claude Code's experimental feature, as described in two posts | A team lead, a shared task list, and teammates | Teammates self-claim tasks from the shared list and message each other directly |
| [[DefinedTerm/planner-worker-model]] | A Cursor engineering experiment, as reported in two posts | Planners, Workers and a Judge | Planners spawn tasks (recursively, as sub-planners); Workers implement them; a Judge assesses whether the goal is met |
| [[DefinedTerm/planner-executor-reviewer]] | A review of the agentic AI literature, and one teaching implementation | Planner, Executor and Reviewer, commonly under an Orchestrator | A sequential or graph-based pipeline, frequently with typed state transitions rather than free text |
| [[DefinedTerm/three-layer-agent-orchestration]] | One engineer's code review system at OpenWork | A parent agent, collection and scrutiny agents, and per-perspective review agents | The parent launches sub-agents in parallel; a scrutiny agent keeps only findings two or more reviewers raise independently |

Two further pages frame the list rather than adding to it. [[DefinedTerm/llm-based-multi-agent-system]] gives the general term and a survey's axes for describing any such system — coordination models (cooperative, competitive, hierarchical or mixed) and communication channels (central, decentral or hierarchical). [[BlogPosting/code-agent-orchestra]] sets out three escalating patterns for coding: subagents, agent teams, and orchestration platforms at scale.

## Where they differ

### Where control sits

The OpenAI guide draws its two patterns apart on exactly this point. In the manager pattern the manager never hands off control, and the guide gives that as the reason it does not lose context; its edges are tool calls that return. In the decentralized pattern the edges are handoffs that do not return: the receiving agent takes over execution and deals with the user itself, and the guide presents this as optimal where no single agent needs to keep central control or synthesize results.

The sub-agent architecture keeps control with the lead in the same way the manager pattern does, but its accounts describe the arrangement in terms of context isolation rather than tool calls. Agent Teams keeps a Team Lead that decomposes work and synthesizes results, but moves the coordination between tasks off the lead: when a teammate marks a task complete, dependent tasks unblock without the lead acting as an intermediary. The Planner-Worker model spreads control across a hierarchy, with Planners able to spawn sub-planners and a Judge deciding when an iteration is finished and when to restart. Three-layer orchestration keeps a parent agent at the top but decides which reviewers run mechanically, from the extensions of the changed files.

### Whether workers talk to each other

The accounts that describe sub-agents say the workers do not talk to each other. [[DefinedTerm/agent-teams]] draws that line explicitly: subagents report back to a single parent and cannot talk to each other, while teammates share findings, challenge each other's approaches and coordinate through a mailbox. The sub-agent page records the same limit from Anthropic's research system, where the lead waits for each set of subagents to finish, cannot steer them mid-flight, and a single slow subagent blocks the system.

Where workers do not talk, something else carries what they need. One adopting team on the sub-agent page writes each task file to be self-contained, so that the file rather than a conversation is the interface between agents. The Planner–Executor–Reviewer review reports typed JSON payloads or LangGraph state graphs replacing free-text handoffs. The multi-agent code-generation review on [[DefinedTerm/llm-based-multi-agent-system]] reports structured, schema-based protocols as a remedy for orchestration failure. The decentralized pattern moves conversation state with the handoff itself.

### Why the work is split at all

The accounts give different reasons for having more than one agent.

- **Context.** The sub-agent architecture is presented by Anthropic as a way around context window limits on long-horizon tasks: sub-agents may explore tens of thousands of tokens and return a summary of often 1,000 to 2,000. [[BlogPosting/code-agent-orchestra]] lists context overload as the first of three single-agent constraints.
- **Narrower scope.** Planner–Executor–Reviewer gives cognitive load as its rationale — a narrowed scope is intended to be more predictable than one generalist agent planning, synthesizing and verifying at once. Three-layer orchestration makes the same argument for review perspectives: a smaller, bounded task yields more accurate output.
- **Coordination.** The Planner-Worker model is reported as the answer to a flatter design in which equal-status agents coordinating through shared file locks got stuck waiting on each other or became risk-averse. Agent Teams is credited in [[BlogPosting/code-agent-orchestra]] with solving the coordination problem subagents leave unsolved.
- **Capacity.** Anthropic's research-system post reads token usage explaining 80% of performance variance on BrowseComp as validating an architecture that distributes work across separate context windows.
- **Prompt and tool sprawl.** The OpenAI guide names prompts that have accumulated many conditional branches, and tools that overlap enough to confuse selection, as its triggers for splitting.
- **Recovery.** One adopting team on the sub-agent page adds that a failed phase can be redone on its own rather than the whole run.

### Where review sits

Most of the patterns place a checking role somewhere, and they place it differently.

- In Planner–Executor–Reviewer the Reviewer is described as the pattern's verifiability mechanism rather than just a third stage. The page makes the pattern's fit depend on the Reviewer having something objective to review against: a Reviewer in a phase with no ground-truth signal has only its own judgement to apply.
- The Planner-Worker model ends each iteration with a Judge assessing whether the overall goal has been met.
- Agent Teams has a reported practice of a read-only "@reviewer" teammate, restricted to lint, test and security-scan tools and triggered on every task completion.
- The sub-agent architecture's second use, in Claude Code's documentation, is adversarial review from a fresh context that sees only the diff and the criteria. The same documentation warns that such a reviewer usually reports some gaps even when the work is sound, and recommends limiting it to correctness and stated requirements.
- Three-layer orchestration replaces a judging reviewer with agreement: four agents from two model families review each perspective, and a finding raised by only one is discarded.

### What it costs and when it does not fit

Every account that discusses cost treats the split as something to justify.

- The OpenAI guide recommends maximizing a single agent's capabilities before introducing multiple agents at all.
- Anthropic's research-system post reports multi-agent systems using about 15× the tokens of a chat interaction, and names most coding tasks as a poor fit today. An adopting team on the same page runs the pattern across a coding pipeline; the page reads the two together as showing that the limit depends on how tasks are cut, with neither side measured.
- Agent Teams costs more tokens because each teammate is a separate Claude instance, and [[BlogPosting/code-agent-orchestra]] reports three to five teammates as the sweet spot.
- The Planner-Worker source notes that this scale is not yet common and that, for most users, one capable long-running agent is often more practical than a large swarm.
- Three-layer orchestration assumes a billing arrangement under which launching many sub-agents is not separately charged, and so does not transfer unchanged to per-invocation billing.
- The handbook chapter on [[DefinedTerm/llm-based-multi-agent-system]] warns that coordination overhead can cancel out the gains from specialization, and that a sequential, tightly coupled task does not need a complex framework.

## What stands behind each account

The patterns rest on different kinds of evidence, and the pages say so.

- **Manager and decentralized patterns** — one vendor's characterization of its own customer experience, with code examples in that vendor's SDK, rather than an independently established taxonomy.
- **Sub-agent architecture** — vendor-reported results, including a lead-plus-subagents system outperforming a single agent by 90.2% on an internal research eval whose design is not described, alongside adopting teams' unmeasured reports.
- **Agent Teams** — an experimental feature, with listed limitations such as teammates not being restored on session resumption and task status that can lag.
- **Planner-Worker model** — one company's reported experiment and its production design, as relayed in two posts.
- **Planner–Executor–Reviewer** — reported as the predominant architecture across a review's 92 primary studies, of which 13 were evaluated in an industrial context; the teaching implementation is evidence of how the pattern is taught, not of how it performs.
- **Three-layer agent orchestration** — one engineer's system in production with qualitative feedback; the evaluation criteria its author sets out are not reported as met.
