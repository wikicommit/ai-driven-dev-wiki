---
title: "multi-agent orchestration"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, context-engineering, agentic-coding]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
    hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be
  - type: url
    url: 'https://www.langchain.com/blog/context-engineering-for-agents'
    hash: sha256:07e9475327ca11aeabb710cea3b419188e2ca4380d3cf4fd055291761f52fb8f
  - type: url
    url: 'https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf'
    hash: sha256:c63d41952636629543bbc11004c9be52b96f346284383c32bcd91f9130d25932
  - type: url
    url: 'https://ghuntley.com/ralph/'
    hash: sha256:9836ee3ee0773613f370a27796b1e456199be38681f73a47b974e210dd356317
  - type: url
    url: 'https://addyosmani.com/blog/code-agent-orchestra/'
    hash: sha256:399fcd256a0dea0d4dc0841558f7f17cf41a9b447bc6bbc5adfbaf8728e9c557
  - type: url
    url: 'https://www.anthropic.com/engineering/building-c-compiler'
    hash: sha256:76ec31b147cb595b08d33f9b46ece5a385276d3165f3c8ca4ab62600055ab111
  - type: url
    url: 'https://www.anthropic.com/engineering/building-effective-agents'
    hash: sha256:89d6d2e67b90631137ed1aba80dbebb0264d98646e0db9850e22d6a6c80c67cf
  - type: url
    url: 'https://www.anthropic.com/engineering/multi-agent-research-system'
    hash: sha256:f9af507dbe72a9650f1c11cf6ae2aa13e7f9c2f6c3a7436129197c31ddb3a3bc
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Splitting work across several agents that each hold their own context window, with a lead agent coordinating them — used both to isolate context so no single window fills up and to explore several parts of a problem in parallel."
  termCode: ""
  inDefinedTermSet: ""
---

Multi-agent orchestration is the practice of splitting work across several agents that each hold their own context window, coordinated by a lead agent or orchestrator. Its two stated motivations are context isolation — no single window accumulates everything — and parallelism, since separate agents can explore different parts of a problem simultaneously. It is one of the standard answers to the context window being a finite resource, alongside [[DefinedTerm/compaction]] and [[DefinedTerm/agentic-memory]].

## Usage

[[TechArticle/effective-context-engineering-for-ai-agents]] describes the architecture concretely: rather than one agent maintaining state across an entire project, specialised sub-agents handle focused tasks with clean context windows while the main agent coordinates with a high-level plan. Each sub-agent might explore extensively, using tens of thousands of tokens or more, but returns only a condensed summary — the post gives a figure of roughly 1,000–2,000 tokens. Its stated benefit is a clear separation of concerns, with detailed search context isolated inside sub-agents while the lead agent synthesises and analyses results. That post also matches the approach to a task shape, recommending it for complex research and analysis where parallel exploration pays dividends, over compaction for conversational back-and-forth and note-taking for iterative development with clear milestones.

[[BlogPosting/context-engineering]] treats the same architecture as the most popular way to *isolate* context in its four-bucket taxonomy, noting that each agent has its own tools, instructions, and context window, and citing separation of concerns as the motivation behind OpenAI's Swarm library. It also states the costs plainly: up to 15× more tokens than chat as reported by Anthropic, the need for careful prompt engineering to plan sub-agent work, and coordination overhead.

[[Report/2026-agentic-coding-trends-report]] treats the shift from single agents to coordinated teams as one of its eight predicted 2026 trends, and describes what adopting it demands: new skills in task decomposition, agent specialisation, and coordination protocols, along with development environments that show the status of multiple concurrent agent sessions and version control workflows that handle simultaneous agent-generated contributions. Its customer example is Fountain's hierarchical orchestration, with a central orchestration agent coordinating specialised sub-agents for candidate screening, document generation, and sentiment analysis.

Not every practitioner reaches for it. [[Person/geoffrey-huntley]] argues in [[BlogPosting/ralph-wiggum-as-a-software-engineer]] that agent-to-agent communication and multiplexing were not needed at the time, comparing non-deterministic agents-as-microservices unfavourably to a single monolithic process — while still using [[DefinedTerm/subagents]] heavily within that single process, dispatched by the primary context window acting as a scheduler.

### The 2026 tool landscape, in three tiers

[[BlogPosting/the-code-agent-orchestra]] frames the same architecture as a shift in the developer's own role — from *conductor*, guiding one agent synchronously with the context window as a hard ceiling, to *orchestrator*, coordinating an ensemble of agents that each hold their own context window and work asynchronously while the developer plans and checks in. Its stated consequence is that the codebase, not the conversation thread, becomes the workspace, and that the skills required change accordingly: clear specifications, work decomposition, and output verification rather than writing code.

That post sorts the tooling into three tiers. **Tier 1** is in-process — Claude Code [[DefinedTerm/subagents]] and [[DefinedTerm/agent-teams]] — needing a single terminal session and no extra tooling. **Tier 2** is local orchestrators, where the developer's machine spawns agents in isolated git worktrees and the developer keeps dashboards, diff review and merge control; it names [[SoftwareApplication/conductor]], [[SoftwareApplication/vibe-kanban]], Gastown, OpenClaw with Antfarm, Claude Squad, [[SoftwareApplication/google-antigravity]] and Cursor Background Agents, and gives 3–10 agents on a known codebase as the range it suits. **Tier 3** is cloud async agents running in cloud VMs and returning a pull request — Claude Code Web, the [[SoftwareApplication/github-copilot]] coding agent, [[SoftwareApplication/jules]], and Codex Web. The post's expectation is that most developers in 2026 use all three: Tier 1 for interactive work, Tier 2 for parallel sprints, Tier 3 to drain the backlog overnight.

Its operational guidance is more conservative than the tier list suggests. It gives 3–5 agents as the sweet spot on the grounds that you should not run more agents than you can meaningfully review, sets "one file, one owner" as a hard rule, recommends checking progress every 5–10 minutes rather than hovering, and defines kill criteria — an agent stuck three or more iterations on the same error is stopped and reassigned. It also names multi-model routing as a cost lever, with planning, implementation and review each routed to a different model through a `MODEL_ROUTING.md` file.

### Coordination through the repository, and the one-big-task ceiling

[[BlogPosting/building-a-c-compiler-with-parallel-claudes]] describes a deliberately minimal alternative to an orchestrator. Each of 16 agents runs in its own Docker container with a bare git repo mounted, clones a local copy, and pushes back when done. Collisions are prevented by a lock: an agent claims a task by writing a text file into a `current_tasks/` directory, and if two agents claim the same one, git's own synchronisation forces the second to choose differently. There is no inter-agent messaging, no enforced process for managing high-level goals, and no orchestration agent — each agent decides what to do, usually taking the "next most obvious" problem, and maintains a running document of failed approaches when stuck. Merge conflicts are described as frequent but handled by the agents themselves.

The failure mode that account documents is about task shape rather than coordination machinery. Parallelism is trivial when there are many distinct failing tests, since each agent takes a different one. When the work became a single giant task — compiling the Linux kernel — every agent hit the same bug, fixed it, and overwrote the others' changes, and having 16 agents running did not help. The fix was to manufacture independence: using a known-good compiler as an oracle, a harness compiled most of the kernel with GCC and only a subset with the agents' compiler, so a failure localised the bug to that subset and different agents could work on different files. Delta debugging was still needed afterwards to find pairs of files that failed together but worked independently.

That report also treats specialisation as a distinct payoff from throughput: alongside the agents solving the problem, individual agents were assigned to coalescing duplicated code (LLM-written code frequently re-implements existing functionality), to the tool's own performance, to the efficiency of its output, to critiquing the project's design from a Rust developer's perspective, and to documentation.

### Orchestrator-workers, and what separates it from parallelization

[[TechArticle/building-effective-agents]] names the pattern **orchestrator-workers**: a central LLM dynamically breaks down a task, delegates the pieces to worker LLMs, and synthesises their results. Its stated distinction from simple parallelization is the one that matters for choosing between them — the two are topographically similar, but in parallelization the subtasks are pre-defined, while in orchestrator-workers they are determined by the orchestrator from the specific input. That is why the post recommends it for work where the subtasks cannot be predicted in advance, giving as its example coding changes where the number of files to change and the nature of each change depend on the task, and search tasks gathering information from multiple sources.

That post also situates the pattern within a deliberately conservative selection rule: agentic systems trade latency and cost for task performance, so the recommendation is the simplest solution that works, with orchestrator-workers sitting near the complex end of five workflow patterns rather than being a default.

### What the architecture buys, and what it costs

[[TechArticle/how-we-built-our-multi-agent-research-system]] gives the clearest cost-benefit statement of the pattern from a vendor running it in production. On the benefit side, its internal evaluation found a multi-agent system with Claude Opus 4 as lead agent and Claude Sonnet 4 subagents outperformed single-agent Claude Opus 4 by 90.2% on its internal research eval — the worked example being identifying all board members of the Information Technology companies in the S&P 500, which the multi-agent system decomposed into subagent tasks while the single agent failed with slow sequential searches.

Its explanation for *why* is deflationary rather than architectural: "multi-agent systems work mainly because they help spend enough tokens to solve the problem." In its analysis of one browsing benchmark, three factors explained 95% of performance variance, with token usage alone accounting for 80%, followed by number of tool calls and model choice. It also notes that model upgrades act as efficiency multipliers, with one generational upgrade producing a larger gain than doubling the token budget on the prior model.

The cost side is stated in the same terms: agents typically use about 4× more tokens than chat interactions, and multi-agent systems about 15× more, so the architecture "require[s] tasks where the value of the task is high enough to pay for the increased performance."

Its stated *non*-fit is notable given this wiki's subject: domains where all agents must share the same context or many dependencies exist between agents are called a poor fit today, and **most coding tasks are named specifically** — on the grounds that they involve fewer truly parallelisable subtasks than research, and that LLM agents are not yet good at coordinating and delegating to each other in real time. Where it does excel, on that account, is valuable tasks involving heavy parallelisation, information exceeding a single context window, and interfacing with numerous complex tools.

That post also records a limitation of its own implementation: lead agents execute subagents synchronously, which simplifies coordination but prevents the lead from steering subagents mid-flight, prevents subagents from coordinating with each other, and can block the whole system on one slow subagent.

## Related Terms

The mechanism it is built from is covered under [[DefinedTerm/subagents]], and one specific discipline for applying it under [[DefinedTerm/subagent-driven-development]]. It is one of the strategies of [[DefinedTerm/context-engineering]], and the evaluation step it usually pairs with is [[DefinedTerm/llm-as-judge]]. Frameworks providing building blocks for it include [[SoftwareApplication/langgraph]] and [[SoftwareApplication/context-engineering-kit]]. A concrete practice built on it is [[custom/Practice/parallel-coding-agents]].
