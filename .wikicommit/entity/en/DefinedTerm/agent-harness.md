---
title: "agent harness"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, agent-architecture, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.05344'
    hash: sha256:29a5dfd46c7505affc599f6922ebba2f67d01e7f3a343df5347a42f435a08edc
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents'
    hash: sha256:2fa27ef4cd354e98bc9fd4d6cc5bec7f182d3b5a96745c6de6f694f18541f1a6
  - type: url
    url: 'https://www.humanlayer.dev/blog/skill-issue-harness-engineering-for-coding-agents'
    hash: sha256:210c3b64f14464d0f411066d18a2164f9d8b5069812277a8a440cb571d86e3f1
  - type: url
    url: 'https://arxiv.org/pdf/2607.03691'
    hash: sha256:2ca8495996618345fe8107bd0b9cf73cf84283dc0135c961a0fadc83ce891c49
  - type: url
    url: 'https://arxiv.org/pdf/2605.18747'
    hash: sha256:b1035aaed7f12c5fa8504dac7f47c2e10dda381065834be2cea784c2f758fb1f
  - type: url
    url: 'https://www.anthropic.com/engineering/building-c-compiler'
    hash: sha256:76ec31b147cb595b08d33f9b46ece5a385276d3165f3c8ca4ab62600055ab111
  - type: url
    url: 'https://www.anthropic.com/engineering/managed-agents'
    hash: sha256:0e4e8bf6d9cb724da07f95297d00f7077a224890c85346851d0d455eba93d529
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The runtime orchestration layer that wraps an agent's core reasoning loop and coordinates tool execution, context management, safety enforcement, and session persistence around it — everything that happens after the first prompt, as distinct from the scaffolding that assembles the agent before it."
---

An agent harness is the runtime orchestration layer that wraps an agent's core reasoning loop and coordinates tool execution, context management, safety enforcement, and session persistence around it. [[ScholarlyArticle/building-effective-ai-coding-agents-for-the-terminal]] defines it in explicit contrast to [[DefinedTerm/agent-scaffolding]]: where scaffolding is concerned with constructing the agent before the first prompt, the harness is concerned with everything that happens after — dispatching tools, compacting context, enforcing safety invariants, and persisting state across turns. The report credits the formalization of the term to Justin Young's writing on effective harnesses for long-running agents, describing it as the runtime framework that coordinates these concerns for agents operating over extended timeframes.

## Usage

In the architecture the report documents, the harness centres on a ReAct execution loop surrounded by supporting subsystems. Each iteration runs a fixed sequence of phases: draining any messages the UI thread injected since the last iteration, checking context pressure and applying reduction strategies, optionally producing a reasoning trace without tool access, calling the action model with the full tool schemas, dispatching any resulting tool calls through the registry, and deciding whether to iterate or return.

Seven subsystems sit around that loop, each addressing a distinct concern: a prompt composition engine that assembles the system prompt from modular, priority-ordered sections; a tool registry that dispatches to specialized handlers; a safety system providing defense in depth through multiple independent layers; a context engineering subsystem that treats the conversation as a finite resource; memory and session services that persist both the transcript and a playbook of learned strategies; and subagent orchestration that spawns isolated agent instances with filtered tool access.

The harness is also where several reliability mechanisms live that the reasoning model itself cannot provide. The report describes interrupt tokens polled at phase boundaries to propagate cancellation, a thread-safe injection queue so follow-up user messages are drained at iteration boundaries and checked before completion rather than being silently dropped, and cost tracking that records cumulative token usage after each model call. Termination is likewise a harness responsibility: the loop can end through explicit completion, implicit completion when the model returns text with no tool calls, exhaustion of an error-recovery budget, or an iteration safety cap — and before accepting termination the system checks for incomplete task items and pending messages.

The report presents the scaffolding/harness split itself as a transferable lesson, arguing that the separation prevents construction-time concerns from tangling with runtime concerns: the harness never checks whether the agent is fully initialized, because eager construction at scaffolding time guarantees it always is. The stated practical benefit is that each concern can evolve independently — adding a new tool requires only a registry change at construction time, while changing the compaction strategy requires only a harness change at runtime.

### The harness for work that outlasts one context window

That credited source is now available directly. [[TechArticle/effective-harnesses-for-long-running-agents]] frames the harness problem around a different axis than the runtime-subsystem account above: not what wraps a single reasoning loop, but what bridges consecutive sessions. Its stated core challenge is that agents must work in discrete sessions and each new session begins with no memory of what came before — the post's analogy being a project staffed by engineers working in shifts, each arriving with no memory of the previous one.

Its answer is a two-part harness rather than a subsystem inventory: an **initializer agent** whose specialized prompt builds the environment on the very first session, and a **coding agent** that runs every session afterwards to make incremental progress and leave structured updates. A footnote makes the split narrower than it sounds — the two differ only in their initial user prompt, sharing the same system prompt, tools, and harness. The environment the initializer leaves behind is what actually carries state across the boundary: a JSON feature list whose entries later agents may only flip from failing to passing, an `init.sh` script that starts the development server, and a progress file read alongside the git log at the start of each session.

The post is explicit that this is a harness-level answer to a problem the model cannot solve on its own: it reports that compaction alone is not sufficient, and that a frontier model looped across context windows on a high-level prompt still fails to produce a production-quality application. Each element of the environment is introduced as the fix for a specific observed failure — declaring victory too early, leaving the environment buggy or undocumented, marking features done prematurely, and re-deriving how to run the app each session.

### The harness as a configuration surface

A third framing treats the harness less as an architecture to be built than as a surface to be tuned. [[BlogPosting/skill-issue-harness-engineering-for-coding-agents]] states the decomposition as `coding agent = AI model(s) + harness`, and defines the harness as the agent's runtime, or its peripherals — what the model uses to interact with its environment. On that account skills, MCP servers, sub-agents, memory, hooks, and context files are technically separate concepts but form one configuration surface, and deliberately tuning it is [[DefinedTerm/harness-engineering]].

That post also records a coupling the subsystem accounts above do not address: frontier coding models are post-trained on their own harnesses, which can make a model perform better in the harness it was trained on — its example being OpenCode having to add an `apply_patch` tool specifically for GPT/Codex models, while Claude and other models continue using ordinary edit and write tools. Its counter-observation is that the coupling can also become over-fitting, citing Terminal Bench 2.0 results in which Opus 4.6 places 33rd in Claude Code but 5th in a harness not seen during post-training, with an error band of about four positions either way.

### The harness as a software system that evolves

The accounts above treat the harness as an architecture or a surface to configure. [[ScholarlyArticle/dont-blame-the-large-language-model]] treats it as a *codebase under active development*, and measures what that development does to agent quality. Its definition is compatible with the others — "a middleware layer in between a developer and a large language model that orchestrates system prompts, tool execution, context management, and iterative reasoning loops" — but its object of study is the release history rather than the design.

What it finds first is a development pattern it names **hyper-churn**: across five open-source harnesses it measures 1.5–18 releases per week and 2.8–34 merged commits per day, with median pull-request review times under four hours, making the most active of them 13–28× more release-intensive than VS Code or GitHub CLI over the same period. Bug-fix commits account for roughly 30% of development effort, and issue backlogs grow rather than close. The paper's conclusion from this is directly definitional: "the agent harness surrounding the LLM is not stable but is instead a continuously evolving software system."

Its controlled result is that this evolution does not reliably improve the agent. Holding the model fixed across 35 sequential Qwen Code CLI releases evaluated on 50 stratified SWE-bench Verified tasks, it finds no statistically significant improvement in resolve rate — with early versions sometimes outperforming later ones — while token usage and tool-call counts more than double in some cases. Mapping commits onto a reference harness architecture, it identifies the LLM Provider layer and Context Management as the components whose changes most often precede quality degradation, and Extensibility and Security as consistently safe. Its practical recommendation for anyone reasoning about a harness is to treat its version as a variable in its own right: developers should track resolve rate, token consumption, and tool-call overhead across releases, and researchers should "report and control for agent harness versions alongside the underlying LLM."

### Code as the harness's substrate

[[ScholarlyArticle/code-as-agent-harness]] proposes a different organising axis again: not what the harness is made of or how it is tuned, but what medium it operates in. Its claim is that "in emerging agentic systems, code is no longer only a target output. It increasingly serves as an operational substrate for agent reasoning, acting, environment modeling, and execution-based verification" — so the harness is best understood as code-centric infrastructure rather than as a set of services around a model.

That survey's three-layer organisation is a usable map of the concern space. A **harness interface** layer where code connects the agent to reasoning, action, and environment modeling; a **harness mechanisms** layer covering planning, memory, and tool use for long-horizon execution together with feedback-driven control and optimization; and a **scaling** layer where shared code artifacts support coordination, review, and verification across multiple agents. Its control section frames the mechanism as a plan–execute–verify loop, with planning treated as contract formation, execution sandboxed under permissioned state transition, and verification performed through deterministic sensors.

Its list of open problems doubles as a statement of what the concept still lacks: evaluation beyond final task success, verification under incomplete feedback, regression-free harness improvement, consistent shared state across multiple agents, human oversight for safety-critical actions, and extension to multimodal environments. The second and third of those are the ones the empirical work above has begun to address.

### Designing the harness for the model rather than for yourself

[[BlogPosting/building-a-c-compiler-with-parallel-claudes]] reports that most of the effort in a long-running autonomous project went into the environment around the agent — the tests, the environment, the feedback — rather than the loop itself, on the reasoning that the loop is only useful if the agent can tell how to make progress. Its author states the discipline as having to keep reminding himself that he was writing the test harness for Claude and not for himself, which meant rethinking assumptions about how tests should communicate results.

Three concrete rules come out of that. Because each agent starts in a fresh container with no context and spends real time orienting itself, the prompt instructs it to maintain extensive READMEs and progress files updated frequently with current status. Against **context window pollution**, the harness prints at most a few lines and logs everything important to a file, with log lines shaped for machine processing — writing `ERROR` and the reason on the same line so a grep finds it — and pre-computing aggregate summary statistics so the agent does not have to recompute them. Against **time blindness**, since the agent cannot tell time and will happily spend hours running tests instead of making progress, the harness prints incremental progress infrequently and defaults to a `--fast` option sampling 1% or 10% of tests, deterministic per agent but random across machines so that each agent can identify regressions perfectly while the fleet still covers every file.

The same account makes verifier quality the binding constraint on the whole arrangement: because the agent will autonomously solve whatever problem it is given, "it's important that the task verifier is nearly perfect, otherwise Claude will solve the wrong problem."

### Harness assumptions expire

[[TechArticle/scaling-managed-agents]] states the durability problem directly: a harness encodes assumptions about what the model cannot do on its own, and those assumptions need to be questioned frequently because they go stale as models improve. Its worked example is a behaviour it names **context anxiety** — Claude Sonnet 4.5 wrapping up tasks prematurely as it sensed its context limit approaching — which was answered by adding context resets to the harness. Running the same harness on Claude Opus 4.5 found the behaviour gone, and the resets had become dead weight.

That post's response is to stop treating the harness as the durable artefact. It virtualises an agent into three interfaces — a session holding the append-only log of everything that happened, a harness holding the loop that calls the model and routes its tool calls, and a sandbox providing an execution environment — each replaceable without disturbing the others, on the operating-system analogy that abstractions like process and file outlasted the hardware beneath them. What survives, in that arrangement, is the interface set rather than any particular loop; the result is described as a [[DefinedTerm/meta-harness]].

Two consequences fall out for harness design specifically. The harness becomes disposable: because the session log sits outside it, nothing in the harness needs to survive a crash, and a replacement can wake on the same session and resume from the last event. And the harness stops owning the environment: it calls a sandbox exactly as it calls any other tool, so a dead sandbox surfaces as a tool-call error handed back to the model rather than as a lost session, and the harness does not know whether the sandbox is a container, a phone, or a games emulator.

## Related Terms

The harness is one half of a pair with [[DefinedTerm/agent-scaffolding]]. Several of the mechanisms it coordinates have their own entries: [[DefinedTerm/adaptive-context-compaction]], [[DefinedTerm/system-reminders]], and [[DefinedTerm/subagents]]. The report positions the whole assembly as an instance of a compound AI system, in which state-of-the-art results come from composing multiple models, retrievers, and tools rather than relying on a single model call.
