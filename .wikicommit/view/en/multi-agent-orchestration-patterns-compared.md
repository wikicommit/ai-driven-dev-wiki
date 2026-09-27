---
title: "Multi-agent orchestration patterns compared"
lang: en
kind: comparison
review_status: pending
generated_at: "2026-09-27"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"
derived_from:
  - path: .wikicommit/entity/en/DefinedTerm/manager-pattern.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/DefinedTerm/decentralized-pattern.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/DefinedTerm/planner-worker-model.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/DefinedTerm/planner-executor-reviewer.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/DefinedTerm/sub-agent-architecture.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/DefinedTerm/agent-teams.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/DefinedTerm/three-layer-agent-orchestration.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/DefinedTerm/llm-based-multi-agent-system.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/BlogPosting/code-agent-orchestra.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/DefinedTerm/subagent-driven-development.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/DefinedTerm/forked-subagent.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/DefinedTerm/llm-map-reduce-pattern.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/DefinedTerm/dual-llm-pattern.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/DefinedTerm/critical-dialogue-review.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/DefinedTerm/multi-model-orchestration.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/BlogPosting/building-effective-agents.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/BlogPosting/dont-build-multi-agents.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/BlogPosting/how-and-when-to-build-multi-agent-systems.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/BlogPosting/building-a-c-compiler-with-a-team-of-parallel-claudes.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/BlogPosting/harness-design-for-long-running-application-development.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/SoftwareApplication/microsoft-agent-framework.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/SoftwareApplication/spring-ai-alibaba.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/SoftwareApplication/agent-development-kit.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
  - path: .wikicommit/entity/en/SoftwareApplication/bmad.md
    source_commit: 1525bfe84e79d069cabbac746d309196d749b23d
---

This wiki records many ways of dividing work among more than one LLM agent, each written up from a different source: vendor guides and engineering posts, framework documentation, practitioners' talks and team write-ups, security design patterns, and reviews of the research literature. They share a vocabulary — "orchestrator", "planner", "worker", "reviewer", "handoff" recur — but they differ in where control sits, what passes between agents, whether the workers talk to each other, why the work is split at all, and what evidence stands behind each account. Several sources also argue against splitting. This page sets them side by side so those differences are visible. It does not rank the patterns or recommend one.

## The patterns side by side

### A coordinator that delegates and collects

| Pattern | Where this wiki's account comes from | Roles | How work passes between agents |
|---|---|---|---|
| [[DefinedTerm/manager-pattern]] | OpenAI's guide to building agents | A central manager and specialist agents | The manager calls each specialist as a tool; the result comes back and the manager keeps talking to the user |
| Orchestrator-workers, in [[BlogPosting/building-effective-agents]] | Anthropic's inventory of patterns seen across customer teams | A central LLM and worker LLMs | The orchestrator breaks the task down from the input, delegates, and synthesizes the results |
| [[DefinedTerm/sub-agent-architecture]] | Anthropic's engineering posts and documentation, adopting teams, and a handbook chapter | A main or lead agent and sub-agents | Each sub-agent works in a fresh context and returns a condensed summary to the lead |
| [[DefinedTerm/forked-subagent]] | Claude Code's documentation | The main session and a fork | The fork inherits the whole conversation; only its final result comes back |
| [[DefinedTerm/subagent-driven-development]] | Two toolkits, the Context Engineering Kit and Superpowers | An orchestrating main agent and one fresh sub-agent per task | Each task goes to a newly dispatched sub-agent, with review between tasks |
| [[DefinedTerm/three-layer-agent-orchestration]] | One engineer's code review system at OpenWork | A parent agent, collection and scrutiny agents, and per-perspective review agents | The parent launches sub-agents in parallel; a scrutiny agent keeps only findings two or more reviewers raise independently |
| [[DefinedTerm/multi-model-orchestration]] | One engineer's post on one project | Claude Code as main agent, Codex as sub-agent | Claude writes the prompt for Codex from the spec; Codex returns JSON; Claude reviews the result and takes the work over if Codex keeps failing |

### Control that moves between peers

| Pattern | Where this wiki's account comes from | Roles | How work passes between agents |
|---|---|---|---|
| [[DefinedTerm/decentralized-pattern]] | OpenAI's guide to building agents | Peer agents, often starting from a triage agent | A one-way handoff transfers execution and conversation state; the receiving agent takes over the interaction |
| [[DefinedTerm/agent-teams]] | Claude Code's experimental feature, as described in two posts | A team lead, a shared task list, and teammates | Teammates self-claim tasks from the shared list and message each other directly |
| The parallel-Claudes harness in [[BlogPosting/building-a-c-compiler-with-a-team-of-parallel-claudes]] | One Anthropic researcher's experiment | Sixteen agents, some given specialized roles | No orchestration agent and no inter-agent communication; each agent claims a task by writing a lock file to a shared git repository |

The last row's author also calls the approach "agent teams", but it is a separate harness, not the Claude Code feature in the row above it.

### A pipeline of specialized roles

| Pattern | Where this wiki's account comes from | Roles | How work passes between agents |
|---|---|---|---|
| [[DefinedTerm/planner-worker-model]] | A Cursor engineering experiment, as reported in two posts | Planners, Workers and a Judge | Planners spawn tasks (recursively, as sub-planners); Workers implement them; a Judge assesses whether the goal is met |
| [[DefinedTerm/planner-executor-reviewer]] | A review of the agentic AI literature, and one teaching implementation | Planner, Executor and Reviewer, commonly under an Orchestrator | A sequential or graph-based pipeline, frequently with typed state transitions rather than free text |
| Planner–generator–evaluator, in [[BlogPosting/harness-design-for-long-running-application-development]] | One Anthropic Labs engineer's experiments | A planner, a generator and an evaluator | The planner expands a short prompt into a product spec; generator and evaluator negotiate a sprint contract and communicate by writing and reading files |
| [[SoftwareApplication/bmad]] | The project's repository, a paper that cites it, and a study of its documentation | Analyst, product manager, architect, developer, UX designer, technical writer | Planning produces PRDs and designs; a sharding step creates story files holding focused context; each role's workflow produces documents for the next phase |

### A split made for trust rather than for work

| Pattern | Where this wiki's account comes from | Roles | How work passes between agents |
|---|---|---|---|
| [[DefinedTerm/dual-llm-pattern]] | Simon Willison's proposal, later restated alongside a paper that includes it | A privileged LLM with tools, and a quarantined LLM that reads untrusted content | The privileged model sees only symbolic variables standing for what the quarantined model read or produced |
| [[DefinedTerm/llm-map-reduce-pattern]] | A post reviewing a paper on securing LLM agents | A coordinating agent and per-item sub-agents | Each sub-agent reads one untrusted item and returns only a constrained answer, such as a boolean |

### Shapes that frameworks package

Three framework pages record orchestration shapes as built-in options rather than as patterns to assemble.

- [[SoftwareApplication/microsoft-agent-framework]] names prebuilt sequential, concurrent, group-chat and handoff orchestrations. Its documentation separates them on interactivity: the first three do not stop for free-form user input on their own, while handoff is interactive by default, returning control to the user when an agent answers without handing off.
- [[SoftwareApplication/spring-ai-alibaba]] separates a workflow, in which sub-agents run along a predefined flow (`SequentialAgent`, `ParallelAgent`, `LoopAgent`), from a multi-agent system in which the model decides where the flow goes next (`LlmRoutingAgent`). Its own table places the multi-agent type's determinism between a single ReAct agent's and a predefined flow's.
- [[SoftwareApplication/agent-development-kit]] wraps a whole agent as a tool with `AgentTool`, so a root agent acts as an orchestrator or router — the same shape as the manager pattern — and a handbook chapter matches ADK to a hierarchical pattern with layers of supervision.

### Pages that frame the list

Three pages frame the list rather than adding to it. [[DefinedTerm/llm-based-multi-agent-system]] gives the general term and a survey's axes for describing any such system — coordination models (cooperative, competitive, hierarchical or mixed) and communication channels (central, decentral or hierarchical). [[BlogPosting/code-agent-orchestra]] sets out three escalating patterns for coding: subagents, agent teams, and orchestration platforms at scale. [[BlogPosting/building-effective-agents]] draws its line between workflows, where LLMs and tools are orchestrated through predefined code paths, and agents, where the LLM directs its own process.

## Where they differ

### Where control sits

The OpenAI guide draws its two patterns apart on exactly this point. In the manager pattern the manager never hands off control, and the guide gives that as the reason it does not lose context; its edges are tool calls that return. In the decentralized pattern the edges are handoffs that do not return: the receiving agent takes over execution and deals with the user itself, and the guide presents this as optimal where no single agent needs to keep central control or synthesize results.

A second line runs through who decides the route. [[BlogPosting/building-effective-agents]] distinguishes orchestrator-workers from parallelization by flexibility rather than topology: in orchestrator-workers the subtasks are not predefined but decided by the orchestrator from the input. Spring AI Alibaba makes the same cut in its types, between a predefined flow and a flow the model decides.

The sub-agent architecture keeps control with the lead in the same way the manager pattern does, but its accounts describe the arrangement in terms of context isolation rather than tool calls. Subagent-driven development keeps the orchestrator in charge of every task: it launches each sub-agent, passes it what it needs, and controls its work. Agent Teams keeps a Team Lead that decomposes work and synthesizes results, but moves the coordination between tasks off the lead: when a teammate marks a task complete, dependent tasks unblock without the lead acting as an intermediary. The parallel-Claudes harness has no coordinator at all: each agent decides for itself what to do, in most cases the "next most obvious" problem. The Planner-Worker model spreads control across a hierarchy, with Planners able to spawn sub-planners and a Judge deciding when an iteration is finished and when to restart. Three-layer orchestration keeps a parent agent at the top but decides which reviewers run mechanically, from the extensions of the changed files.

In the trust-driven patterns, control sits with the component that never reads untrusted text. The dual LLM pattern's privileged model holds the tools and is only ever exposed to trusted input; the map-reduce pattern's coordinator never needs the underlying text.

### What passes between agents

The patterns differ widely in what one agent hands another.

- **A condensed summary.** Sub-agents may explore tens of thousands of tokens and return a summary of often 1,000 to 2,000 tokens.
- **The whole conversation.** A forked subagent inherits the main session's system prompt, tools, model and message history, which the documentation describes as dropping the input isolation other subagents provide; it keeps the output side, returning only its final result.
- **Conversation state with control.** The decentralized pattern moves conversation state with the handoff itself.
- **Files.** One adopting team on the sub-agent page writes each task file to be self-contained, so that the file rather than a conversation is the interface between agents. BMAD's story files hold focused context for one task. In the planner–generator–evaluator harness, generator and evaluator communicate by writing and reading files. The parallel-Claudes agents coordinate only through lock files in a shared repository and are instructed to maintain READMEs and progress files, because each starts in a fresh container with no context.
- **Typed messages.** The Planner–Executor–Reviewer review reports JSON payloads or LangGraph state graphs replacing free-text handoffs. The code-generation review on [[DefinedTerm/llm-based-multi-agent-system]] reports structured, schema-based protocols as a remedy for orchestration failure. In multi-model orchestration Codex returns JSON: task output, tokens used and a log directory on success, and a suggested fix on failure.
- **Deliberately narrow channels.** The dual LLM pattern's privileged model sees only symbolic variables such as `$var1`. The map-reduce pattern's sub-agents return a constrained answer; a boolean, on that page's account, can express at worst a wrong answer about one file, not a new instruction.

The accounts disagree about how much to pass. [[BlogPosting/dont-build-multi-agents]] states as its first principle that full agent traces should be shared, not just individual messages, because copying the original task to each subagent leaves out earlier turns and tool calls that bear on how it should be read. The handbook chapter on [[DefinedTerm/llm-based-multi-agent-system]] names efficient context transfer between agents as a limit none of the frameworks it compares resolves: sharing everything is slow and expensive, and sharing summaries loses detail. Multi-model orchestration reports the same fragmentation across models, bridged by having Claude write the prompt for Codex from the spec.

### Whether workers talk to each other

The accounts that describe sub-agents say the workers do not talk to each other. [[DefinedTerm/agent-teams]] draws that line explicitly: subagents report back to a single parent and cannot talk to each other, while teammates share findings, challenge each other's approaches and coordinate through a mailbox. The sub-agent page records the same limit from Anthropic's research system, where the lead waits for each set of subagents to finish, cannot steer them mid-flight, and a single slow subagent blocks the system.

Two accounts treat workers that cannot see each other as the problem itself. [[BlogPosting/dont-build-multi-agents]] states as its second principle that actions carry implicit decisions and conflicting decisions carry bad results: even with shared context, parallel subagents that cannot see each other's work make choices on conflicting assumptions. Its example is a Flappy Bird clone split into a background subtask and a bird subtask, which come back in mismatched styles. The parallel-Claudes harness has no inter-agent communication either, and reports parallelism breaking down on the Linux kernel, a single giant task on which every agent hit and fixed the same bug; the fix was to use GCC as a known-good oracle so that different agents chased different bugs in different files.

Where workers do not talk, something else carries what they need: the self-contained task file, the typed payload, or lock files in a shared repository.

### Why the work is split at all

The accounts give different reasons for having more than one agent.

- **Context.** Anthropic presents the sub-agent architecture as a way around context window limits on long-horizon tasks. Subagent-driven development gives [[DefinedTerm/context-rot]] as its reason for launching a fresh sub-agent per task. [[BlogPosting/code-agent-orchestra]] lists context overload as the first of three single-agent constraints.
- **Narrower scope.** Planner–Executor–Reviewer gives cognitive load as its rationale — a narrowed scope is intended to be more predictable than one generalist agent planning, synthesizing and verifying at once. Three-layer orchestration makes the same argument for review perspectives: a smaller, bounded task yields more accurate output.
- **Coordination.** The Planner-Worker model is reported as the answer to a flatter design in which equal-status agents coordinating through shared file locks got stuck waiting on each other or became risk-averse. Agent Teams is credited in [[BlogPosting/code-agent-orchestra]] with solving the coordination problem subagents leave unsolved.
- **Capacity.** Anthropic's research-system post reads token usage explaining 80% of performance variance on BrowseComp as validating an architecture that distributes work across separate context windows.
- **Throughput across providers.** Multi-model orchestration was adopted because one provider's token-consumption limits capped how many work lines could run in parallel.
- **Independent judgement.** The planner–generator–evaluator post argues that agents asked to judge their own work tend to praise it, and that tuning a separate evaluator to be skeptical is more tractable than making a generator critical of its own output. Critical dialogue review argues that a single model reviewing its own output gives weak independence of perspective.
- **Trust.** The dual LLM and map-reduce patterns split by privilege: the component holding dangerous capabilities never reads attacker-controllable text.
- **Prompt and tool sprawl.** The OpenAI guide names prompts that have accumulated many conditional branches, and tools that overlap enough to confuse selection, as its triggers for splitting.
- **Recovery.** One adopting team on the sub-agent page adds that a failed phase can be redone on its own rather than the whole run.

### Reading versus writing

[[BlogPosting/how-and-when-to-build-multi-agent-systems]] draws a distinction the other accounts approach from different sides: read actions are more parallelizable than write actions, because parallel writing requires both communicating context between agents and merging their outputs, and conflicting writes produce far worse results than conflicting reads. It points to Anthropic's research system, where multiple agents handle the research while the final report is written by a single main agent in one call. Anthropic's research-system post names most coding tasks as a poor fit today. The adopting team on the sub-agent page runs the pattern across a coding pipeline by making each task file self-contained and isolating each run in its own git worktree, and the page reads the two together as showing that the limit depends on how tasks are cut, with neither side measured.

### Where review sits

Most of the patterns place a checking role somewhere, and they place it differently.

- In Planner–Executor–Reviewer the Reviewer is described as the pattern's verifiability mechanism rather than just a third stage. The page makes the pattern's fit depend on the Reviewer having something objective to review against.
- The Planner-Worker model ends each iteration with a Judge assessing whether the overall goal has been met.
- The planner–generator–evaluator harness gives its evaluator the Playwright MCP so it can navigate the live page before scoring. Its author reports the evaluator's value as conditional: worth its cost when the task sits beyond what the current model does reliably alone, and moved from per-sprint grading to a single pass at the end once the model improved.
- Subagent-driven development puts review between every task. In Superpowers it is two-stage, checking spec compliance first and code quality second; the Context Engineering Kit offers executing a task with an independent judge and an automatic retry loop until it passes.
- Agent Teams has a reported practice of a read-only "@reviewer" teammate, restricted to lint, test and security-scan tools and triggered on every task completion.
- The sub-agent architecture's second use, in Claude Code's documentation, is adversarial review from a fresh context that sees only the diff and the criteria. The same documentation warns that such a reviewer usually reports some gaps even when the work is sound.
- Critical dialogue review pairs agents on different models: Codex criticizes, Claude Code accepts, rejects or holds each finding with a reason, and Codex re-criticizes the rejections. Neither agent is the final judge; after a cap on cycles the decision returns to a person.
- Three-layer orchestration replaces a judging reviewer with agreement: four agents from two model families review each perspective, and a finding raised by only one is discarded. The handbook chapter on [[DefinedTerm/llm-based-multi-agent-system]] lists voting, confidence-weighted voting and trust-value routing as ways to settle disagreement.
- In multi-model orchestration, the main agent reviews the sub-agent's work for conformance to the spec.
- The parallel-Claudes harness puts its check outside the agents: its author reports that the task verifier must be nearly perfect, and added a stricter continuous integration pipeline when new features began breaking existing functionality.

### What it costs and when it does not fit

Every account that discusses cost treats the split as something to justify.

- [[BlogPosting/building-effective-agents]] states its general rule as finding the simplest solution possible and increasing complexity only when needed, which may mean not building an agentic system at all. The OpenAI guide recommends maximizing a single agent's capabilities before introducing multiple agents.
- [[BlogPosting/dont-build-multi-agents]] recommends a single-threaded linear agent whose context is continuous, optionally with a separate model that compresses history for very long tasks, and judges that in 2025 agents cannot yet resolve disagreements with each other much more reliably than a single agent.
- Anthropic's research-system post reports multi-agent systems using about 15× the tokens of a chat interaction. Early versions spawned 50 subagents for simple queries when task descriptions were vague.
- The planner–generator–evaluator post reports one prompt costing $9 over 20 minutes solo and $200 over 6 hours with the full harness; the solo result's game did not respond to input, and the harness produced a playable one.
- The parallel-Claudes experiment ran nearly 2,000 sessions at about $20,000 in API costs; its author judges that a fraction of what producing the compiler himself, let alone with a team, would have cost.
- Subagent-driven development reports token overhead of 1.5x–3x and 3x–5x for two of its variants, and Superpowers offers inline execution as the cheaper alternative.
- Agent Teams costs more tokens because each teammate is a separate Claude instance, and [[BlogPosting/code-agent-orchestra]] reports three to five teammates as the sweet spot.
- Critical dialogue review is reported to take more time and money than running Claude Code alone, and is kept for important features and high-risk changes.
- The Planner-Worker source notes that this scale is not yet common and that, for most users, one capable long-running agent is often more practical than a large swarm.
- Three-layer orchestration assumes a billing arrangement under which launching many sub-agents is not separately charged, and so does not transfer unchanged to per-invocation billing.
- The dual LLM pattern's author calls building such systems fiddly, with things that cannot be done with them. The map-reduce pattern is misapplied where a sub-agent's result must be rich enough to carry attacker-controlled prose back.
- Multi-model orchestration reports the main agent sometimes giving reasons to avoid delegating to Codex, which its author has not been able to suppress fully.
- The handbook chapter on [[DefinedTerm/llm-based-multi-agent-system]] warns that coordination overhead can cancel out the gains from specialization, and that a sequential, tightly coupled task does not need a complex framework.
- [[BlogPosting/how-and-when-to-build-multi-agent-systems]] concludes that there is no one-size-fits-all answer and that the right point between single and multiple agents depends on the problem.

## What stands behind each account

The patterns rest on different kinds of evidence, and the pages say so.

- **Manager and decentralized patterns** — one vendor's characterization of its own customer experience, with code examples in that vendor's SDK, rather than an independently established taxonomy.
- **Orchestrator-workers and the other building blocks** — Anthropic's consulting experience, reported qualitatively, with no measurements for any pattern.
- **Sub-agent architecture** — vendor-reported results, including a lead-plus-subagents system outperforming a single agent by 90.2% on an internal research eval whose design is not described, alongside adopting teams' unmeasured reports.
- **Forked subagent** — one tool's documentation of its own feature.
- **Subagent-driven development** — two toolkits' descriptions of their own tooling; the token-overhead figures are the project's own, not an independent benchmark.
- **Agent Teams** — an experimental feature, with listed limitations such as teammates not being restored on session resumption and task status that can lag.
- **Parallel-Claudes harness** — one researcher's first-hand account of one experiment, which its author calls a very early research prototype.
- **Planner-Worker model** — one company's reported experiment and its production design, as relayed in two posts.
- **Planner–Executor–Reviewer** — reported as the predominant architecture across a review's 92 primary studies, of which 13 were evaluated in an industrial context; the teaching implementation is evidence of how the pattern is taught, not of how it performs.
- **Planner–generator–evaluator** — one engineer's experiments, with a single solo-versus-harness comparison on one prompt, no repetition, and quality judgements calibrated to the author's own taste.
- **BMAD** — the project's own documentation and a study scoring it from that documentation; the study records it as without independent empirical evaluation.
- **Three-layer agent orchestration** — one engineer's system in production with qualitative feedback; the evaluation criteria its author sets out are not reported as met.
- **Multi-model orchestration** and **critical dialogue review** — each one team's or one engineer's report of its own deployment, with no measured comparison against a single model.
- **Dual LLM and map-reduce patterns** — a researcher's proposal, which its author calls a terrible solution that may nonetheless be the best available, and a paper's pattern known here through a reviewer's account; uptake in the literature rather than evidence of deployment.
- **Framework-packaged shapes** — each framework's documentation, a course, or a handbook chapter; the chapter gives no measurement for its account of ADK.
- **The case against splitting** — [[BlogPosting/dont-build-multi-agents]] reports no measurements and is written by a company building its own agent product; [[BlogPosting/how-and-when-to-build-multi-agent-systems]] is a commentary on the Anthropic and Cognition posts by the maker of LangGraph.
