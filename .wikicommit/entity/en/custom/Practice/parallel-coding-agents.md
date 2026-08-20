---
title: "Parallel Coding Agents"
type: "schema:custom/Practice"
lang: en
tags: [agentic-coding, agent-architecture, context-engineering, human-ai-collaboration]
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"
derived_from:
  - path: .wikicommit/entity/en/DefinedTerm/subagents.md
    source_commit: 1804b4f09d8e8e88510a78cca5839eb041febbe0
  - path: .wikicommit/entity/en/DefinedTerm/multi-agent-orchestration.md
    source_commit: 1804b4f09d8e8e88510a78cca5839eb041febbe0
  - path: .wikicommit/entity/en/DefinedTerm/subagent-driven-development.md
    source_commit: 1804b4f09d8e8e88510a78cca5839eb041febbe0
  - path: .wikicommit/entity/en/SoftwareApplication/claude-code.md
    source_commit: 1804b4f09d8e8e88510a78cca5839eb041febbe0
  - path: .wikicommit/entity/en/DefinedTerm/agent-execution-environment.md
    source_commit: 1804b4f09d8e8e88510a78cca5839eb041febbe0
  - path: .wikicommit/entity/en/ScholarlyArticle/agentic-software-engineering-foundational-pillars.md
    source_commit: 1804b4f09d8e8e88510a78cca5839eb041febbe0
  - path: .wikicommit/entity/en/DefinedTerm/spec-driven-development.md
    source_commit: 1804b4f09d8e8e88510a78cca5839eb041febbe0

properties:
  description: "Running several AI coding agents at the same time on parts of one problem, rather than driving a single agent serially. Its two stated payoffs are context isolation — no single context window accumulates everything — and latency reduction on independent work; its cost is token overhead, coordination effort, and the need to partition the work so the agents do not interfere with each other."
  appliesWhen: "Complex research, exploration and analysis where several parts of a problem can be examined independently; independent operations whose latency can be traded against thread overhead; work partitioned at the specification level so components can be implemented simultaneously. Not recommended for tasks needing frequent back-and-forth, for phases that share significant context, or where latency matters more than context isolation."
  precondition: "Work that can be decomposed into independent units; a coordinating agent or orchestrator holding the high-level plan; version control workflows able to absorb simultaneous agent-generated contributions, and, where agents write to the same repository, separate checkouts such as worktrees."
  failureMode: "Unbounded exploration when subagent prompts carry no explicit termination condition; context pollution, role confusion and task-list conflicts when parallel agents are given the same tools as the main agent; 'bad form back pressure' when fan-out is too wide for build and test work; results invisible to the user unless the parent agent presents them; token cost reported as high as 15x that of chat."
  evidenceOrigin: "Vendor engineering blog posts and product documentation (Anthropic, LangChain), one implementation report for a specific terminal agent, one practitioner's account of his own loop, one toolkit's maintainers reporting their own production figures, one industry trends report, and one vision paper that presents no empirical evaluation. No controlled study of parallel agent execution appears in the grounding material."
  tool:
    - "[[SoftwareApplication/claude-code]]"
    - "[[SoftwareApplication/context-engineering-kit]]"
    - "[[SoftwareApplication/opendev]]"
    - "[[SoftwareApplication/langgraph]]"
    - "[[SoftwareApplication/spec-kit]]"
---

Running coding agents in parallel means putting several agents to work at the same time on different parts of one problem, coordinated by a lead agent, instead of driving a single agent through the work serially. Two motivations are stated for it across the accounts that describe it, and they are separable: **context isolation**, so that no single context window accumulates everything, and **parallelism proper**, so that separate agents can explore different parts of a problem simultaneously. The practice is one of the standard answers to the context window being a finite resource, alongside [[DefinedTerm/compaction]] and [[DefinedTerm/agentic-memory]], and it is what [[DefinedTerm/multi-agent-orchestration]] does when the coordination is concurrent rather than sequential.

## When to Apply

The clearest matching of the practice to a task shape comes from the context-engineering account behind [[DefinedTerm/multi-agent-orchestration]]: parallel sub-agents suit **complex research and analysis where parallel exploration pays dividends**, as against compaction for conversational back-and-forth and note-taking for iterative development with clear milestones. On the implementation side, the argument in [[DefinedTerm/subagents]] is narrower and more operational — multiple subagents can run concurrently when the main agent emits several spawn calls in the same response, which is framed as **trading thread overhead for latency reduction on independent operations**. The qualifier is doing the work there: the operations have to be independent for the trade to pay.

The same material is explicit about when *not* to reach for it. Anthropic's subagent documentation recommends the main conversation instead when a task needs frequent back-and-forth, when several phases share significant context, or when latency matters — because a subagent that is not a fork starts genuinely fresh and may need time to gather context before it can do anything. A fresh agent does not see the conversation history, the skills already invoked, or the files the parent has already read.

Two accounts add a *partitioning* precondition rather than a task-shape one. The report behind [[DefinedTerm/spec-driven-development]] argues that specifications act as "super-prompts" that break complex problems into modular components aligned with agents' context windows, and that partitioning work at the spec level is what lets multiple agents implement different components simultaneously without interference — the interference being the thing the specification is there to prevent. [[SoftwareApplication/spec-kit]] treats parallel implementation exploration as a phase in its own right ("Creative Exploration": explore diverse solutions across multiple technology stacks and architectures), which is parallelism used for *variance* rather than for throughput.

Not every practitioner adopts it at the process level. [[Person/geoffrey-huntley]] argues in [[BlogPosting/ralph-wiggum-as-a-software-engineer]] that agent-to-agent communication and multiplexing were not needed at the time, comparing non-deterministic agents-as-microservices unfavourably to a single monolithic process — while still using [[DefinedTerm/subagents]] heavily *within* that single process. That is a useful boundary line: he rejects parallel agents as an architecture and keeps them as a dispatch mechanism.

## How It Works

**A lead agent holds the plan; the parallel agents hold the detail.** Rather than one agent maintaining state across an entire project, specialised sub-agents handle focused tasks with clean context windows while the main agent coordinates with a high-level plan. Each sub-agent may explore extensively — tens of thousands of tokens or more — and returns only a condensed summary, given as roughly 1,000–2,000 tokens. The separation of concerns is the point: detailed search context stays isolated inside the sub-agents while the lead agent synthesises and analyses.

**Fan-out is bounded deliberately, and the bound differs by work type.** Huntley's prompts permit many parallel subagents for search and file writing but only *one* for build and test, because fanning out to hundreds of subagents all running builds and tests produces what he calls "bad form back pressure." Controlling the degree of parallelism is, on his account, part of using the mechanism rather than an implementation detail. Claude Code encodes the same concern as hard limits: by default a subagent can spawn its own subagents up to three layers below the main conversation, after which the delegation tool is withheld and the subagent must do the work itself and return one summary; and spawning a twenty-first *running* subagent fails with a `Concurrent subagent limit reached` error that instructs the model not to retry, with no limit on the total spawned over a session. Both caps are configurable through environment variables.

**Tool sets are narrowed per agent, not shared.** In the OpenDev implementation described under [[DefinedTerm/subagents]], each subagent type is restricted to a filtered tool set enforced at the schema level rather than by runtime permission checks, so a read-only agent cannot attempt a write tool, argue for an exception, or probe for bypass conditions. Three reasons are given, and two of them are specifically about parallelism: excluding task-management tools so that only the main agent coordinates task lists, **preventing race conditions**; reducing context size and focusing each agent on its role; and limiting the blast radius of errors.

**Where agents write, they need separate ground.** [[SoftwareApplication/claude-code]]'s documentation lists worktrees, the desktop app, Claude Code on the web, and agent teams as its parallel-work options, and `isolation: worktree` gives a subagent its own copy of the repository rather than just its own context — with the boundary enforced actively, by checking each command's working directory, blocking commands that redirect git into the main checkout, and refusing commands whose shape it cannot verify stay inside the worktree.

**Parallelism is also used for competition, not only for division.** [[DefinedTerm/subagent-driven-development]] ships `/do-in-parallel` for running the same task across multiple independent targets with context isolation, and `/do-competitively` for competitive generation followed by multi-judge evaluation and evidence-based synthesis; its maintainers also describe generating specifications on the fly *in parallel with* implementation rather than writing a full specification up front. Claude Code's **fork** (`/subtask`) serves the same shape from the other direction: it inherits the entire conversation so far, deliberately dropping the input isolation subagents otherwise provide while keeping the output isolation, and is recommended for trying several approaches in parallel from the same starting point.

**Verification is usually a parallel agent too.** Adding an adversarial review step in a fresh subagent context before treating work as done is recommended practice, on the grounds that the agent doing the work should not be the one grading it — see [[DefinedTerm/llm-as-judge]].

## Failure Modes

- **Unbounded exploration.** Early OpenDev prompts lacking clear stop conditions led to an explorer subagent repeatedly reading the same files; adding explicit termination conditions and an anti-loop instruction resolved it. The same pattern is catalogued in Anthropic's best-practices guide as "the infinite exploration," where an unscoped investigation reads hundreds of files, with scoped delegation named as the fix.
- **Context pollution and role confusion.** Early versions of OpenDev gave subagents the same tools as the main agent, which caused context pollution, role confusion, and conflicts when both agents attempted to update task lists simultaneously — the concrete form of the race condition that motivates per-agent tool filtering.
- **Back pressure at wide fan-out.** Huntley's limit of one build-and-test subagent exists because wide fan-out on that class of work degrades rather than accelerates.
- **Invisible results.** Subagent results are not visible to the user, so the parent agent must present their findings itself rather than assuming they have been seen.
- **Rules that do not cross the boundary.** Claude Code's built-in Explore and Plan agents skip the CLAUDE.md hierarchy and the parent session's git status to stay fast and cheap, and there is no setting to change that; a rule that must reach the agent itself has to be restated in the delegation prompt.
- **Cost.** Up to 15× more tokens than chat is reported, alongside the need for careful prompt engineering to plan sub-agent work and the coordination overhead itself.

## Evidence

The material supporting this practice is almost entirely **vendor documentation, implementation reports and practitioner accounts** — no controlled study of parallel agent execution appears in it.

Anthropic's engineering post and its Claude Code documentation supply the architecture and the operational limits; both describe the vendor's own product. The OpenDev report is a single implementation account, valuable because it records what went wrong before it went right (the same-tools mistake, the missing stop conditions) rather than only the finished design. LangChain's context-engineering post supplies the cost figures — the 15× number is attributed to Anthropic — and the separation-of-concerns motivation behind OpenAI's Swarm library. Huntley's account is one practitioner's experience of his own loop; the parallelism limits in it are his, not measured.

The [[Report/2026-agentic-coding-trends-report]] treats the shift from single agents to coordinated teams as one of eight *predicted* 2026 trends, and states what adoption demands: new skills in task decomposition, agent specialisation and coordination protocols, development environments that show the status of multiple concurrent agent sessions, and version control workflows that handle simultaneous agent-generated contributions. Its Fountain example is a customer's hierarchical orchestration, reported by the vendor.

[[DefinedTerm/subagent-driven-development]]'s figures — `/do-and-judge` credited with a 90% chance of a fully accurate result for changes spanning 1–3 files at 1.5×–3× token overhead, `/do-in-steps` with 92% at 3×–5×, against 60–80% for a one-shot prompt at no overhead — are the maintainers' own numbers from their production usage, not published benchmark results. The spec-driven report's claim that human-refined specs improve LLM-generated code quality, with controlled studies showing error reductions of up to 50%, is about specification quality rather than about parallelism itself.

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] is a vision paper whose authors state explicitly that it offers no empirical evaluation of its framework.

## Notes

Across these accounts the two motivations for the practice — context isolation and parallel speed — are routinely stated together but pull in different directions, and the material only makes this visible when the sources are placed side by side. Anthropic's own guidance recommends *against* delegation when latency matters, on the grounds that a fresh agent must first gather context; the OpenDev report recommends *for* concurrency precisely as a latency reduction. Both can hold, but only if the isolation cost is paid on work independent enough that the gathering happens in parallel too — which is the condition the spec-driven account addresses from a different angle, by partitioning the work before any agent starts.

A second tension sits between the practitioner and framework ends of the material. [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] proposes an [[DefinedTerm/agent-execution-environment]] built for "massive parallelism" and argues SE curricula should train students to manage *fleets* of agents, while the operational accounts describe fan-out being deliberately capped in the single digits for build and test work and at twenty concurrent agents by default in one shipped product. The vision assumes the infrastructure that would make wide parallelism cheap; the shipped tools describe the back pressure that exists before it does.

No source in this grounding set describes how to merge or reconcile the output of agents that worked in parallel on the same codebase. The trends report names version control workflows that handle simultaneous agent-generated contributions as a requirement for adoption, and worktrees supply per-agent isolation while work is in progress — but what happens at the merge point is not covered by any of these accounts.
