---
title: "subagents"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, configuration, agent-architecture, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/html/2602.14690v1'
    hash: sha256:a95102e253d7131ba8bf5f38f7f1e738784be17159af65fa612395d8ed4800b9
  - type: url
    url: 'https://arxiv.org/pdf/2603.05344'
    hash: sha256:29a5dfd46c7505affc599f6922ebba2f67d01e7f3a343df5347a42f435a08edc
  - type: url
    url: 'https://code.claude.com/docs/en/best-practices'
    hash: sha256:92807ef3d58f63fbea435ea928df49e2f3341e118eb8c40db08800c100a4c4c5
  - type: url
    url: 'https://ghuntley.com/ralph/'
    hash: sha256:9836ee3ee0773613f370a27796b1e456199be38681f73a47b974e210dd356317
  - type: url
    url: 'https://code.claude.com/docs/en/sub-agents'
    hash: sha256:12cc07fa94c1e50e47e202b2d565884e44401d3bce47e2e2c8dc5598cb57f87a
  - type: url
    url: 'https://resources.anthropic.com/hubfs/Claude%20Code%20Advanced%20Patterns_%20Subagents,%20MCP,%20and%20Scaling%20to%20Real%20Codebases.pdf'
    hash: sha256:143e1a9f91063648c6ee3a39d9db2b5f2b9c7d42efa9188abdc46b3e3b104a9d
  - type: url
    url: 'https://www.humanlayer.dev/blog/skill-issue-harness-engineering-for-coding-agents'
    hash: sha256:210c3b64f14464d0f411066d18a2164f9d8b5069812277a8a440cb571d86e3f1
  - type: url
    url: 'https://addyosmani.com/blog/code-agent-orchestra/'
    hash: sha256:399fcd256a0dea0d4dc0841558f7f17cf41a9b447bc6bbc5adfbaf8728e9c557
  - type: url
    url: 'https://www.anthropic.com/engineering/multi-agent-research-system'
    hash: sha256:f9af507dbe72a9650f1c11cf6ae2aa13e7f9c2f6c3a7436129197c31ddb3a3bc
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Specialized AI agents that an agentic AI coding tool, or another agent, can delegate tasks to. Their defining property is context isolation: a subagent operates in its own context window with a restricted tool set and returns only a distilled result to the parent agent."
---

Subagents are specialized AI agents that agentic AI coding tools, or other agents, can delegate tasks to. Their defining property across the sources that describe them is context isolation: a subagent operates within its own context window and returns its results to the parent agent, rather than executing within the calling agent's context.

As described in [[ScholarlyArticle/configuring-agentic-ai-coding-tools]], a subagent is technically a Markdown file sharing the same YAML frontmatter structure as an [[DefinedTerm/agent-skills]] definition. The functional difference between the two mechanisms is where the work happens: a subagent gets its own context window, whereas a Skill executes its instructions within the calling agent's context.

## Usage

**As a configuration mechanism.** Subagent support is less universal than Skills support. Among the five tools surveyed in that study, [[SoftwareApplication/claude-code]] (`.claude/agents/`), [[SoftwareApplication/github-copilot]] (`.github/agents/`), and [[SoftwareApplication/cursor]] (`.cursor/agents/`) offer the mechanism, while [[SoftwareApplication/codex-cli]] and [[SoftwareApplication/gemini-cli]] do not.

Adoption follows a pattern close to that of Skills. The study found 452 subagents across 131 repositories, averaging 3.45 per repository with a median of 2 (minimum 1, maximum 18); repositories that use them commonly define fewer than three. Subagents also show positive correlations with several other configuration mechanisms, including Settings, Skills, and MCP.

One capability the study looked for and did not find in use is persistent memory. Claude Code's subagents can have their own memory — a persistent directory that survives across interactions with the agent, usable for building up knowledge over time such as debugging insights — but the authors could not find any repositories in their sample storing such memory files.

**As an architectural mechanism.** [[ScholarlyArticle/building-effective-ai-coding-agents-for-the-terminal]] documents subagent orchestration from the implementing side, in the design of [[SoftwareApplication/opendev]]. There, each subagent type is restricted to a filtered tool set — the report names Code-Explorer, Planner, PR-Reviewer, Security-Reviewer, Web-Clone, Web-Generator, Project-Init, and Ask-User — and the restriction is enforced at the schema level rather than by runtime permission checks. The report presents this as a safety argument: because write tools are simply absent from a read-only subagent's schema, the agent cannot attempt to invoke them, argue for an exception, or probe for bypass conditions.

That report gives three reasons for restricting subagent capabilities: excluding task management tools so that only the main agent coordinates task lists, preventing race conditions; reducing context size and focusing each subagent on its specific role; and limiting the blast radius of errors, so that an exploration subagent cannot accidentally modify files.

It also describes two operational properties. Multiple subagents can run concurrently when the main agent emits several spawn calls in the same response, which the report frames as trading thread overhead for latency reduction on independent operations. And subagent prompts carry explicit termination conditions to prevent over-exploration — the report records that early prompts lacking clear stop conditions led to unbounded exploration, with an explorer subagent repeatedly reading the same files, and that adding stop conditions and an anti-loop instruction resolved it. A further recorded lesson is that early versions gave subagents the same tools as the main agent, which caused context pollution, role confusion, and conflicts when both agents attempted to update task lists simultaneously.

Context isolation is also what makes subagents useful for retrieval specifically: the report notes that when a subagent performs a multi-step search, intermediate results potentially spanning thousands of lines of code stay inside the subagent's window, and only the distilled summary returns to the main agent — preventing the retrieval process itself from consuming the context budget the main agent needs for reasoning and action.

A consequence both sources imply and the OpenDev report states explicitly is that subagent results are not visible to the user, so the parent agent must present their findings itself rather than assuming they have been seen.

**As an everyday working practice.** Anthropic's Claude Code documentation presents subagents as one of the most powerful tools available to a user, on the grounds that context is the fundamental constraint: researching a codebase means reading many files, all of which consume the main conversation's context, whereas subagents run in separate context windows and report back summaries. Its recommended invocations are explicit — *"use subagents to investigate X"* — and it names two uses in particular: scoping an investigation so exploration does not consume the main context, which it lists as the fix for a failure pattern it calls "the infinite exploration"; and reviewing completed work in a fresh context before treating a task as done, so the agent doing the work is not the one grading it (see [[DefinedTerm/llm-as-judge]]).

[[Person/geoffrey-huntley]] takes the same context argument further in [[BlogPosting/ralph-wiggum-as-a-software-engineer]], arguing the primary context window should not be allocated to at all but should operate as a scheduler that dispatches subagents for expensive allocation-type work — searching the filesystem, summarising whether a test suite passed. He also records a limit: fanning out to hundreds of subagents all running builds and tests produces "bad form back pressure," which is why his prompts permit many parallel subagents for search and file writing but only one for build and test. Controlling the degree of parallelism, in his account, is part of using the mechanism rather than an implementation detail.

The same vendor's [[PresentationDigitalDocument/claude-code-advanced-patterns]] deck states the choice as three conditions to check before delegating: that the subagent can be given a clear and relatively specialized role with defined tool access levels and criteria for success or completion; that inspecting or interacting with its work is not a priority, so a completed task and a few conclusions are all that is needed back; and that context management is served by the isolation. It places subagents between two neighbours on the same axis — separate terminals for unrelated tasks, agent teams for one large task split into coordinating workstreams — so that delegating a focused subtask from a single main session is what distinguishes a subagent from either.

### What isolation costs, in one vendor's implementation

Anthropic's dedicated Claude Code subagents documentation is specific about what a subagent does and does not inherit, which makes the trade-off behind context isolation legible. Each subagent runs in its own context window with its own system prompt, its own tool access, and independent permissions, and the documentation lists five reasons to use one: preserving context, enforcing constraints through tool restrictions, reusing configurations across projects, specialising behaviour with a focused system prompt, and controlling costs by routing work to faster, cheaper models.

The cost side is that a fresh subagent starts genuinely fresh. It does not see the conversation history, the skills already invoked, or the files the parent has already read; it receives a delegation message the parent composes plus its own system prompt and appended environment details, not the parent's full system prompt. The documentation also names state that never crosses the boundary at all: the session's output style does not shape a subagent's responses, the main conversation's auto memory is not loaded, and the subagent's context window is sized by its own model, so delegating to a smaller model gives that subagent a smaller window. Its stated guidance follows from this — prefer the main conversation when a task needs frequent back-and-forth, when several phases share significant context, or when latency matters, because a subagent that is not a fork starts fresh and may need time to gather context.

Two of the built-in subagents deliberately narrow what loads even further: Explore and Plan, both read-only agents with Write and Edit denied, skip the CLAUDE.md hierarchy and the parent session's git status to keep research fast and inexpensive, and the documentation notes there is no setting to change which agents skip them. Its stated mitigation is that the main conversation reads their results with full CLAUDE.md context anyway, so a rule only needs restating in the delegation prompt when it must reach the subagent itself — its example being "ignore the `vendor/` directory."

A **fork** is the documented escape hatch from that isolation. Started with `/subtask`, it inherits the entire conversation so far — the same system prompt, tools, model, and message history — which the documentation describes as deliberately dropping the input isolation subagents otherwise provide, while keeping the output isolation: the fork's own tool calls stay out of the parent conversation and only its final result comes back. It recommends a fork when any other subagent would need too much background to be useful, or to try several approaches in parallel from the same starting point.

The same documentation records the operational limits the mechanism runs into at scale, which is the concrete form of the parallelism concern practitioners describe. Nesting is capped — by default a subagent can spawn its own subagents up to three layers below the main conversation, after which the delegation tool is withheld and the subagent must do the work itself and return one summary. Concurrency is capped separately: by default, spawning a twenty-first running subagent fails with a `Concurrent subagent limit reached` error that instructs the model not to retry, with no limit on the total spawned over a session. Both caps are configurable through environment variables.

Configuration precedence runs by scope, from managed organisation settings, through subagents defined as JSON on the command line for a single session, to project and then user directories, with plugin-supplied subagents lowest; within the project scope, where nested `.claude/agents/` directories are scanned by walking up from the working directory, the definition closest to that directory wins. Plugin subagents are additionally restricted for security reasons: the `hooks`, `mcpServers`, and `permissionMode` frontmatter fields are ignored when an agent is loaded from a plugin. Where a subagent needs its own copy of the repository rather than just its own context, `isolation: worktree` supplies one, and the documentation describes Claude Code enforcing that boundary actively — checking each command's working directory, blocking commands that redirect git into the main checkout, and refusing commands whose shape it cannot verify stay inside the worktree.

### The context firewall, and what it is not for

[[BlogPosting/skill-issue-harness-engineering-for-coding-agents]] is unusually direct about a use of the mechanism that did not work for its authors: role-based sub-agents — a "frontend engineer" sub-agent, a "backend engineer" sub-agent, a "data analyst" sub-agent — which the post states plainly "doesn't work." What it reports working is the isolation property itself, which it calls a **context firewall**: an entire session's worth of work is encapsulated so the dispatching agent sees only the prompt it wrote and the sub-agent's final result, with none of the intermediate tool calls, tool results, or other messages entering the parent window. That team calls sub-agents a particularly powerful lever for hard problems, on the grounds that isolation is what maintains coherency across the many context windows such a problem takes.

Two operational conventions come with it in that account. Sub-agents should return highly condensed responses that themselves follow [[DefinedTerm/progressive-disclosure]] — their own agents cite sources in `filepath:line` format or as URLs, so the parent is not exposed to everything the sub-agent read but can go find it if needed. And the split is used for cost as well as context: an expensive model for the parent session where planning and orchestration happen, a cheaper and faster one for each sub-agent, on the reasoning that a discrete task needs a smaller instruction budget.

The post also records a workaround for harnesses without native support: an MCP server exposing a tool that launches a new agent session with a prompt from the parent and returns its final message. It warns that combining this with a harness that *does* support sub-agents lets native sub-agents dispatch further sub-agents through MCP, and that many harnesses impose an MCP tool-call timeout that may need raising.

### Hierarchical delegation

[[BlogPosting/the-code-agent-orchestra]] describes a second-order use of the same mechanism it calls *teams of teams*. Rather than an orchestrator spawning six subagents directly — which fragments the orchestrator's own context — it spawns two feature leads, each of which decomposes its brief into its own two or three specialists. A feature lead given "build the search feature" splits it into data, logic and API subagents on its own, and the parent never sees those details. Osmani's stated analogy is that real engineering organisations do not have a VP assigning tasks to individual engineers; the work goes through layers of tech leads.

That post also states plainly what a plain subagent arrangement still lacks, and treats it as the reason to graduate to [[DefinedTerm/agent-teams]]: the parent must manage the dependency graph manually, there is no peer messaging between subagents, there is no shared task list, and sloppy file scoping lets two subagents write to the same file. In its worked three-subagent example the coordination cost is entirely the parent's — two independent subagents run in parallel and write report files, and the third waits for both reports before starting.

### Subagents as compression

[[TechArticle/how-we-built-our-multi-agent-research-system]] gives a compact statement of why the mechanism suits search specifically: "the essence of search is compression: distilling insights from a vast corpus." Subagents facilitate that compression by operating in parallel with their own context windows, exploring different aspects of a question simultaneously before condensing the most important tokens for the lead agent. The second property it names is separation of concerns — distinct tools, prompts and exploration trajectories — which it argues reduces path dependency and enables thorough, independent investigations.

That post also documents what goes wrong when delegation is underspecified. Each subagent needs an objective, an output format, guidance on which tools and sources to use, and clear task boundaries; without detailed task descriptions "agents duplicate work, leave gaps, or fail to find necessary information." Its worked failure is a lead agent issuing instructions as short as "research the semiconductor shortage," after which one subagent explored the 2021 automotive chip crisis while two others duplicated each other on 2025 supply chains.

Effort scaling was pushed into the prompt for the same reason — agents struggle to judge appropriate effort, so explicit rules were embedded: one agent with 3-10 tool calls for simple fact-finding, 2-4 subagents with 10-15 calls each for direct comparisons, and more than 10 subagents with clearly divided responsibilities for complex research. Early versions without such rules over-invested in simple queries, in one case spawning 50 subagents for a simple request.

## Related Terms

Subagents are one of eight configuration mechanisms catalogued in the configuration study, alongside [[DefinedTerm/context-files]], [[DefinedTerm/agent-skills]], Commands, Rules, Settings, Hooks, and MCP servers. The authors note that usage patterns for subagents resemble those of Skills closely enough that differences in their content and use cases warrant dedicated future study. Architecturally, subagent orchestration is one of the subsystems coordinated by the [[DefinedTerm/agent-harness]], and the filtered agents themselves are compiled during [[DefinedTerm/agent-scaffolding]]. Splitting a problem across several of them is covered under [[DefinedTerm/multi-agent-orchestration]], and the specific discipline of dispatching a fresh one per task with a review between tasks under [[DefinedTerm/subagent-driven-development]]. Their context-isolation property makes them one of the three standard techniques for long-horizon work, alongside [[DefinedTerm/compaction]] and [[DefinedTerm/agentic-memory]].
