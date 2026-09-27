---
title: "What Counts as a Harness"
lang: en
kind: debate
review_status: pending
generated_at: "2026-09-27"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"
derived_from:
  - path: .wikicommit/entity/en/DefinedTerm/agent-harness.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/DefinedTerm/harness-engineering.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/DefinedTerm/execution-harness.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/DefinedTerm/system-harness.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/DefinedTerm/meta-harness.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/DefinedTerm/methodological-harness.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/DefinedTerm/agent-scaffold.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/DefinedTerm/harness-as-a-service.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/DefinedTerm/agent-framework.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/DefinedTerm/agent-runtime.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/DefinedTerm/brain-hands-session-split.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/BlogPosting/the-anatomy-of-an-agent-harness.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/BlogPosting/agent-frameworks-runtimes-and-harnesses.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/BlogPosting/agent-harness-engineering.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/BlogPosting/skill-issue-harness-engineering-for-coding-agents.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/BlogPosting/harness-engineering-for-coding-agent-users.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/BlogPosting/what-is-harness-engineering.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/BlogPosting/your-agent-needs-a-harness-not-a-framework.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/BlogPosting/scaling-managed-agents-decoupling-the-brain-from-the-hands.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/BlogPosting/codex-as-a-platform.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/ScholarlyArticle/harness-engineering-anatomy-architecture-and-evolution-of-coding-agents.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/ScholarlyArticle/survey-on-agent-system-and-harness-design.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/ScholarlyArticle/code-as-agent-harness.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/ScholarlyArticle/externalization-in-llm-agents.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/ScholarlyArticle/coding-benchmarks-are-misaligned-with-agentic-software-engineering.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/ScholarlyArticle/spec-driven-development-for-agentic-software-engineering.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/ScholarlyArticle/inside-the-scaffold.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
  - path: .wikicommit/entity/en/ScholarlyArticle/harness-engineering-for-agentic-ai-coding-tools.md
    source_commit: a2ba4711503633df3c1b0613b4c6e0a04b2a0e27
---

The pages in this wiki that use the word "harness" do not agree on what it covers. The question they answer differently is simple to state: what, exactly, is a harness? Is it everything around a model, the configuration surface a user customises, one layer in a stack of agent-building software, the infrastructure that keeps an agent loop alive, one of several components of an agent, or a level of orchestration with other levels above and beside it? This page sets the answers side by side, together with what each one rests on. It does not pick one.

## The broad answer: everything that is not the model

The most expansive definition is compressed into "Agent = Model + Harness" and "if you're not the model, you're the harness". [[BlogPosting/the-anatomy-of-an-agent-harness]], a LangChain post by Vivek (Viv) Trivedy, counts as harness every piece of code, configuration and execution logic that is not the model itself: system prompts; tools, skills and MCP servers with their descriptions; bundled infrastructure such as a filesystem, sandbox and browser; orchestration logic such as subagent spawning, handoffs and model routing; and hooks or middleware for deterministic execution. On this account a raw model is not an agent until a harness gives it state, tool execution, feedback loops and enforceable constraints. Trivedy presents this as, in his opinion, the cleanest way to draw the boundary.

The formulation travels. Addy Osmani's [[BlogPosting/agent-harness-engineering]] repeats it, attributing it to Viv Trivedy, and lists prompts, tools, context policies, hooks, sandboxes, subagents, feedback loops and recovery paths as the harness. [[BlogPosting/what-is-harness-engineering]] quotes the same formula, with the harness as constraint mechanisms, feedback loops, automated tests, workflow control and documentation standards, and calls it, in its author's phrase, an operating system designed for the agent. [[ScholarlyArticle/harness-engineering-anatomy-architecture-and-evolution-of-coding-agents]], a source-code study of eleven production coding agents, takes "an agent is a model plus a harness" as its starting definition, with the harness as the runtime that couples a model to the world through its loop, tools, context, safety controls, orchestration and extension surfaces.

Vendor and project documentation uses the word in the same broad sense. [[DefinedTerm/agent-harness]] records Anthropic's documentation describing [[SoftwareApplication/claude-code]] as the layer around the model that provides the tools and manages the context the model sees, and identifying that layer as what "agentic harness" refers to. The [[SoftwareApplication/openharness]] README calls a harness the complete infrastructure that wraps an LLM to make it a functional agent, and closes on "The model is the agent. The code is the harness." OpenAI's [[BlogPosting/codex-as-a-platform]] argues that a capable agent needs more than a prompt and a model response, and names the surrounding execution system — understanding a task, maintaining context, calling tools, handling failures, requesting approval — as the agent harness. [[DefinedTerm/harness-engineering]] records a chapter of [[CreativeWorkSeries/agentic-engineering-patterns]] stating that a coding agent *is* a harness for a language model.

Two variations narrow the emphasis without narrowing the formula. HumanLayer's [[BlogPosting/skill-issue-harness-engineering-for-coding-agents]] writes "coding agent = AI model(s) + harness", but describes the harness as the agent's *configuration surface* — skills, MCP servers, sub-agents, memory, AGENTS.md files and the like. [[BlogPosting/harness-engineering-for-coding-agent-users]] takes the "everything except the model" shorthand and narrows it to the bounded context of using a coding agent: part of the harness is built into the agent by its builders, and users add an **outer harness** of their own, which it models as a system of [[DefinedTerm/guides-and-sensors]].

## Formalised versions of the broad answer

Several research papers keep the broad scope but give it internal structure instead of a list.

[[ScholarlyArticle/survey-on-agent-system-and-harness-design]] writes an agent at the implementation level as a foundation model coupled with an [[DefinedTerm/execution-harness]], formalised as six coupled runtime responsibilities: observation interface, context manager, control loop, action interface, state and artifact store, and verification and governance. It states that this is broader than any individual tool, memory module, prompt template or workflow script.

[[ScholarlyArticle/code-as-agent-harness]] frames the harness as a policy-governed system around the model and separates it from the code running inside it: code is an executable medium *within* the harness, and the harness decides what code may be executed, trusted, persisted, reused or promoted. That survey also observes that production harnesses are becoming a source of training data, which it describes as making the boundary between "the agent" and "the harness around the agent" a learnable surface in its own right.

[[ScholarlyArticle/externalization-in-llm-agents]] pushes the concept furthest: a harness is the **designed cognitive environment** within which externalised memory, skills and protocols become jointly effective, with agency emerging from the coupling of model and environment rather than sitting in the model alone. It says the concept is still consolidating, and presents its characterisation as a synthesis of recurring patterns rather than a closed definition.

[[ScholarlyArticle/harness-engineering-for-agentic-ai-coding-tools]] draws the line by layering vocabulary rather than listing parts: *context* is the complete input to a single model call, and the agent harness is the software around the model that drives the agent loop, assembles that context for each call, exposes tool schemas and manages turn-by-turn state. On that reading, designing the context is context engineering, and customising the harness itself is harness engineering.

## What a harness is not

[[ScholarlyArticle/harness-engineering-anatomy-architecture-and-evolution-of-coding-agents]] is the one source here that defines the harness by exclusion. It names four things a harness is often confused with:

- a **scaffold**, which it treats as a near-synonym, reserving "scaffold" where a distinction helps for the structural code — the loop and the registries — and "harness" for the shipped runtime artifact that embeds it;
- an **agentic framework**, a library imported to build an agent, as opposed to a runtime worked inside;
- an **evaluation harness** such as SWE-bench's, which wraps an agent rather than a model;
- an **orchestrator or [[DefinedTerm/meta-harness]]**, which coordinates harnesses from above and implements no editing loop of its own.

The paper says scoring a meta-harness on the same subsystems as a harness would be a category error. Its exclusions put it at odds with some of the accounts below: the framework it contrasts with a harness is the layer Harrison Chase builds a harness on top of, and its meta-harness uses the same word Anthropic uses for something different.

## A layer in a stack: framework, runtime, harness

Harrison Chase's [[BlogPosting/agent-frameworks-runtimes-and-harnesses]] uses "harness" not for the system around a model in general but for one position in a layering of agent-building packages. An [[DefinedTerm/agent-framework]] provides abstractions; an [[DefinedTerm/agent-runtime]] beneath it supplies production infrastructure, chiefly durable execution; and an agent harness sits above the framework, adding default prompts, opinionated handling of tool calls, planning tools and filesystem access — "batteries included". His example is LangChain's own [[SoftwareApplication/deep-agents]], built on LangChain.

Read this way, a harness is a kind of package, one of three categories, rather than the complement of the model. Chase allows that all coding CLIs could be argued to be agent harnesses of a kind. He states that he did not coin the term, that its definition was not yet clear, and that the boundaries between the three layers are blurry. [[DefinedTerm/agent-harness]] notes that Trivedy's later definition, from the same company's blog, is much broader than Chase's layering.

The layering does not line up with the source-code study above. Chase's harness is built on a framework; that study distinguishes a harness from a framework as a runtime worked inside rather than a library imported, and reports that none of the eleven agent runtimes it examined imports a general-purpose agentic framework such as LangChain, LangGraph or AutoGen.

## Infrastructure that connects: the harness as a durable runtime

[[BlogPosting/your-agent-needs-a-harness-not-a-framework]], a post on the Inngest blog, starts from the engineering meaning of the word — a wiring harness, a test harness, a safety harness: the layer that connects, protects and orchestrates components without doing the work itself. In its framing the LLM is the engine, tools are the peripherals and memory is storage, and the harness is what connects them, catches failures, prevents collisions and routes events. The problems a harness solves — retries, state, concurrency, observability, scheduling — are framed as infrastructure problems rather than AI problems.

What this post calls a harness sits close to what Chase calls a runtime. Chase names durable execution as the main concern of an agent runtime and names Temporal, Inngest and other durable execution engines as the projects closest to LangGraph there; the Inngest post argues that durable, event-driven infrastructure already solves what it calls the harness problem. The post is written by the vendor of the infrastructure it recommends.

## One component among several

Two Anthropic accounts split an agent into more parts than two, and in both the harness is one of them rather than everything besides the model.

An Anthropic post on agent governance, recorded on [[DefinedTerm/harness-engineering]], splits an agent four ways: **the model**; **a harness**, defined as the instructions and guardrails the model operates under; **tools**, the services and applications the model can use; and **an environment**, where the agent runs and what it can reach. [[DefinedTerm/harness-engineering]] presents this as a decomposition of the second term of "agent = model + harness" rather than a rival to it.

[[BlogPosting/scaling-managed-agents-decoupling-the-brain-from-the-hands]] draws a different three-way line for [[SoftwareApplication/claude-managed-agents]]: a **session** (an append-only log of everything that happened), a **harness** (the loop that calls Claude and routes its tool calls) and a **sandbox** (where Claude runs code and edits files), each behind its own interface — the [[DefinedTerm/brain-hands-session-split]]. The harness calls the sandbox like any other tool, and because the session log sits outside it, a failed harness can be rebooted and resume from the last event. Anthropic describes keeping credentials out of the sandbox so that the harness is never made aware of any credentials.

On both readings, things the broad answer places inside the harness sit outside it. Trivedy's inventory includes tools, a filesystem and a sandbox; the governance split names tools and environment as components of their own, and the Managed Agents design places the sandbox and the durable session log beside the harness rather than in it.

## Levels of harness

Several sources use "harness" for something that can be nested, with more than one harness in the same system.

[[ScholarlyArticle/coding-benchmarks-are-misaligned-with-agentic-software-engineering]], by Gorinova et al., uses "agent harness" for a language model interacting with tools towards a single task, treated as a configurable executor of model, prompt, tools and loop. Most artefacts called "coding agents" are agent harnesses in this sense. The [[DefinedTerm/system-harness]] sits outside them: it turns higher-level goals into tasks, dispatches each to one or more agent harnesses, manages the environment, and routes outputs through feedback. The inner level here is not the same object as the broad answer's harness — Gorinova et al.'s agent harness includes the model, whereas Trivedy's harness is everything except it.

A [[DefinedTerm/meta-harness]] is a level above that again, and the word is used for two different designs. In the source-code study, it is an orchestration layer that wraps entire harnesses — Claude Code, Codex, Cursor and others — as interchangeable components and implements no editing loop of its own; its example is [[SoftwareApplication/omnigent]], and its authors read it as a bet that the harness is becoming a commodity component. Anthropic calls Claude Managed Agents "a meta-harness" in a different sense: a system unopinionated about which harness runs, offering durable-session and sandbox interfaces that many harnesses can run on. Neither source refers to the other's usage.

The outer harness of [[BlogPosting/harness-engineering-for-coding-agent-users]] is a third kind of outside layer: not an orchestrator but the guides and sensors a user adds around the part of the harness the agent's builders already supplied.

## Beyond the software: the methodological harness

[[DefinedTerm/methodological-harness]] records a proposal from [[ScholarlyArticle/spec-driven-development-for-agentic-software-engineering]] that extends the word past software altogether. That paper calls the software around a model — orchestration loop, tools, context management, memory, guardrails and verification loops — the *technical* harness, which governs one agent in one session. It argues that team-level properties such as reproducibility, auditability, transferability, review capacity and coordination need a second, *methodological* harness: team-owned practices and artifacts centred on the specification. The authors describe their framework as falsifiable hypotheses rather than a validated model.

[[BlogPosting/harness-engineering-for-coding-agent-users]] makes a smaller move in the same direction: it says human developers bring their skills and experience as an implicit harness, which a coding agent lacks, and that harnesses try to make that explicit but can only go so far.

## Neighbouring words

Two other terms in the wiki cover much of the same ground without being defined in terms of "harness".

[[DefinedTerm/agent-scaffold]] records [[ScholarlyArticle/inside-the-scaffold]], a source-code taxonomy of 13 open-source coding agents, which calls the code surrounding the model in a coding agent — control loop, tool definitions, state management and context strategy — its **scaffold**, organised into control architecture, tool and environment interface, and resource management. The later source-code study treats "scaffold" and "harness" as near-synonyms in practice, with the scaffold/runtime-artifact distinction described above; its example is that Mini-SWE-Agent's scaffold is 100 lines of Python, while Claude Code's harness is a product with a terminal UI, a permission system and a plugin ecosystem.

[[DefinedTerm/harness-as-a-service]] uses the word for something you build *on*: a framing, attributed to Viv Trivedy, of a shift from building on LLM APIs that return a completion to building on harness APIs that return a runtime. The Claude Agent SDK, the Codex SDK and the OpenAI Agents SDK are named as pointing this way. Like Chase, this treats a harness as something a builder obtains rather than writes, but the examples do not line up: the harness-as-a-service page names the OpenAI Agents SDK as pointing towards harness APIs, while [[DefinedTerm/agent-framework]] records Chase classifying the OpenAI Agents SDK as an agent framework.

## Where the answers diverge

Laid side by side, the accounts differ along a few distinct lines:

- **Boundary.** Whether tools, the sandbox, the execution environment and durable state are part of the harness or components beside it. Trivedy's inventory, the Claude Code documentation and the OpenHarness README place tools inside the harness; Anthropic's governance split names tools and environment as separate components; the Managed Agents design places the sandbox and the session log outside the harness, which it reduces to the loop that calls the model and routes its tool calls.
- **Kind of thing.** Whether a harness is the complement of the model in any agent (the broad answer), a configuration surface (HumanLayer), a category of package above a framework (Chase), connecting infrastructure of the kind Chase files under runtime (Inngest), or something a builder obtains as a service (harness-as-a-service). The source-code study adds that it is *not* a framework, a scaffold in the narrow sense, an evaluation harness or a meta-harness.
- **Scope.** Whether "harness" names a single agent working on a single task, a system above that dispatching to many (Gorinova et al.), a layer above whole harnesses (the meta-harness, in two senses), an outer layer a user adds (the outer harness), or a team's practices around all of it (the methodological harness).
- **Durability.** Anthropic's Managed Agents post starts from harnesses encoding assumptions about what Claude cannot do on its own, which go stale as models improve, and so makes its design opinionated about the interfaces around Claude rather than about the harness that runs on them. Osmani's post argues harnesses do not shrink as models improve but move. The Trivedy post expects some harness functions to be absorbed into models while harness engineering stays useful. The meta-harness authors read the harness as becoming a commodity. The methodological-harness proposal describes the technical harness as depreciating and the methodological harness as appreciating.

Several of the sources flag their own definitions as provisional. Chase says no clear definition exists yet, Trivedy calls his boundary the cleanest in his opinion, the externalization review calls the concept still consolidating, and the meta-harness authors call Omnigent the first such system they know of rather than a representative of an established category.
