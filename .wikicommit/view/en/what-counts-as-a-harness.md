---
title: "What Counts as a Harness"
lang: en
kind: debate
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"
derived_from:
  - path: .wikicommit/entity/en/DefinedTerm/agent-harness.md
    source_commit: abe7dbaa9cb573068b927bda52cc565d6ba058e6
  - path: .wikicommit/entity/en/DefinedTerm/harness-engineering.md
    source_commit: c6b8c68a8b3e34ab51b855aeb44d0daa53497505
  - path: .wikicommit/entity/en/DefinedTerm/execution-harness.md
    source_commit: 23acf239019dbf782b4365d4b7b30b659e3d60c1
  - path: .wikicommit/entity/en/DefinedTerm/system-harness.md
    source_commit: 23acf239019dbf782b4365d4b7b30b659e3d60c1
  - path: .wikicommit/entity/en/DefinedTerm/agent-scaffold.md
    source_commit: 2b5f014fc7cc03f207d83ea499c4a231c110d0fe
  - path: .wikicommit/entity/en/DefinedTerm/harness-as-a-service.md
    source_commit: 908ab492691e9fcd622bfa73c6c2fd839716bea1
  - path: .wikicommit/entity/en/DefinedTerm/methodological-harness.md
    source_commit: 35d96aaa33f4f9b2ab6d25c70a59d6ec1d1c503a
  - path: .wikicommit/entity/en/DefinedTerm/agent-framework.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/BlogPosting/agent-frameworks-runtimes-and-harnesses.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/BlogPosting/the-anatomy-of-an-agent-harness.md
    source_commit: 136844949634913857d6d1eb26ef9cb9cfaf8876
---

The pages in this wiki that use the word "harness" do not agree on what it covers. The question they answer differently is simple to state: what, exactly, is a harness? Is it everything around a model, one layer in a stack of agent-building software, one of several components of an agent, or a level of orchestration that has another level above it? This page sets the answers side by side, together with what each one rests on. It does not pick one.

## The broad answer: everything that is not the model

The most expansive definition is compressed into "Agent = Model + Harness" and "if you're not the model, you're the harness". [[BlogPosting/the-anatomy-of-an-agent-harness]], a LangChain post by Vivek Trivedy, counts as harness every piece of code, configuration and execution logic that is not the model itself: system prompts; tools, skills and MCP servers with their descriptions; bundled infrastructure such as a filesystem, sandbox and browser; orchestration logic such as subagent spawning, handoffs and model routing; and hooks or middleware for deterministic execution. On this account a raw model is not an agent until a harness gives it state, tool execution, feedback loops and enforceable constraints. Trivedy presents this as, in his opinion, the cleanest of many possible ways to draw the boundary.

Several other sources on [[DefinedTerm/agent-harness]] use the word in this broad sense. Anthropic's documentation describes [[SoftwareApplication/claude-code]] as the layer around the model that provides the tools and manages the context the model sees, and identifies that layer as what "agentic harness" refers to. The [[SoftwareApplication/openharness]] README calls a harness the complete infrastructure that wraps an LLM to make it a functional agent, and closes on "The model is the agent. The code is the harness." [[DefinedTerm/harness-engineering]] records Addy Osmani's post attributing the "agent = model + harness" formulation to Trivedy, and a chapter of [[CreativeWorkSeries/agentic-engineering-patterns]] stating that a coding agent *is* a harness for a language model: software that extends the model with prompts the user never sees and with callable tools.

The Trivedy post adds an observation about training: because products such as Claude Code and Codex are post-trained with their harness in the loop, a model can overfit to that harness, and the post notes that on the Terminal Bench 2.0 leaderboard Opus 4.6 in Claude Code scores far below Opus 4.6 in other harnesses. It argues from this that the best harness for a task is not necessarily the one the model was trained with.

## A formalised version of the broad answer

Three research reviews keep the broad scope but give it internal structure instead of a list.

[[DefinedTerm/execution-harness]] records [[ScholarlyArticle/survey-on-agent-system-and-harness-design]] writing an agent as a model layer coupled with an execution harness, formalised as a six-part tuple: observation interface, context manager, control loop, action interface, state and artifact store, and verification and governance. The survey states that this is broader than any individual tool, memory module, prompt template or workflow script, and treats the six parts as coupled rather than independently optimisable.

[[DefinedTerm/agent-harness]] records a second survey, [[ScholarlyArticle/code-as-agent-harness]], which frames the harness as a policy-governed system around the model. It separates the harness from the code running inside it: code is an executable medium *within* the harness, and the harness decides what code may be executed, trusted, persisted, reused or promoted. That survey also treats the harness as a safety governor that classifies proposed actions by risk and enforces permission tiers.

[[DefinedTerm/harness-engineering]] records a review, [[ScholarlyArticle/externalization-in-llm-agents]], that pushes the concept further still: a harness as the **designed cognitive environment** within which externalised modules become jointly effective, with agency emerging from the coupling of model and environment rather than sitting in the model alone. That review says the concept is still consolidating, and presents its characterisation as a synthesis of recurring patterns rather than a closed definition. It offers six analytical dimensions of harness design as a framework for comparing harness architectures rather than as an implementation checklist.

## A narrower answer: a layer above the framework

Harrison Chase's post [[BlogPosting/agent-frameworks-runtimes-and-harnesses]] uses "harness" not for the system around a model in general but for one position in a layering of agent-building packages. An [[DefinedTerm/agent-framework]] provides abstractions; an agent runtime beneath it supplies production infrastructure such as durable execution; and an agent harness sits above the framework, adding default prompts, opinionated handling of tool calls, planning tools and filesystem access — "batteries included". His example is LangChain's own [[SoftwareApplication/deep-agents]], built on LangChain.

Read this way, a harness is a kind of package, one of three categories, rather than the complement of the model. Chase allows that all coding CLIs could be argued to be agent harnesses of a kind. He states that he did not coin the term, that its definition was not yet clear, and that the boundaries between the three layers are blurry: LangGraph, for instance, is "probably best described as both a runtime and a framework". The classification is illustrated throughout with the author's own company's packages, and the post calls itself a first attempt rather than a settled taxonomy.

The two LangChain posts therefore disagree with each other. [[DefinedTerm/agent-harness]] notes that Trivedy's later definition is much broader than Chase's layering.

## A partitioned answer: one component among four

An Anthropic post on agent governance, recorded on [[DefinedTerm/harness-engineering]], splits an agent four ways: **the model**; **a harness**, defined as the instructions and guardrails the model operates under; **tools**, the services and applications the model can use; and **an environment**, where the agent runs and what it can reach. Each is described as both a source of capability and a potential point of oversight.

On this reading tools and environment are *not* part of the harness. Under the "not the model, so harness" definition they are. [[DefinedTerm/harness-engineering]] presents the four-way split as a decomposition of the second term of "agent = model + harness" rather than a rival to it. The boundary question is still visible, though: what one account calls part of the harness, the other names as a separate component beside it.

## A levelled answer: agent harness and system harness

[[ScholarlyArticle/coding-benchmarks-are-misaligned-with-agentic-software-engineering]], a paper by Gorinova et al., uses "agent harness" for one of two levels of orchestration. As recorded on [[DefinedTerm/system-harness]], an agent harness is a language model interacting with tools towards a single task, treated as a configurable executor of model, prompt, tools and loop. Most artefacts called "coding agents", naming Claude Code, Codex, Cursor Agent, SWE-Agent and OpenHands among them, are agent harnesses in this sense. The **system harness** sits outside them: it turns higher-level goals into tasks, dispatches each to one or more agent harnesses, manages the environment, and routes outputs through feedback in three tiers by scope, latency and trust.

Here "harness" names something that can be nested. The inner level is not the same object as the broad answer's harness — Gorinova et al.'s agent harness includes the model, whereas Trivedy's harness is everything except it — and the paper argues that practical agentic coding at scale operates at the outer one, while benchmarks measure the inner. [[DefinedTerm/agent-harness]] records the same authors reproducing Terminal-Bench entries for a single fixed model across several agent harnesses, with accuracy ranging from roughly 58% to roughly 80%, and arguing that a leaderboard entry naming only a model is under-specified.

## Beyond one agent: the methodological harness

[[DefinedTerm/methodological-harness]] records a proposal from [[ScholarlyArticle/spec-driven-development-for-agentic-software-engineering]] that extends the word past software altogether. That paper calls the software around a model — orchestration loop, tools, context management, memory, guardrails and verification loops — the *technical* harness, which governs one agent in one session. It argues that team-level properties such as reproducibility, auditability, transferability, review capacity and coordination need a second, *methodological* harness: team-owned practices and artifacts centred on the specification.

This answer also disagrees about how long a harness lasts. The paper describes the technical harness as transient, depreciating as models improve and as capabilities become native to them, and the methodological harness as appreciating over time. The authors describe their framework as falsifiable hypotheses rather than a validated model.

## Neighbouring words

Two other terms in the wiki cover much of the same ground without being defined in terms of "harness".

[[DefinedTerm/agent-scaffold]] records [[ScholarlyArticle/inside-the-scaffold]], a source-code taxonomy of 13 open-source coding agents, which calls the code surrounding the model in a coding agent — control loop, tool definitions, state management and context strategy — its **scaffold**, and organises it into control architecture, tool and environment interface, and resource management. The scaffold and harness pages link to each other, but none of them states whether "scaffold" and "harness" name the same thing.

[[DefinedTerm/harness-as-a-service]] uses the word for something you build *on*: a framing, attributed to Viv Trivedy, of a shift from building on LLM APIs that return a completion to building on harness APIs that return a runtime. The Claude Agent SDK, the Codex SDK and the OpenAI Agents SDK are named as pointing this way. Like Chase, this treats a harness as something a builder obtains rather than writes, but the examples do not line up: the harness-as-a-service page names the OpenAI Agents SDK as pointing towards harness APIs, while [[DefinedTerm/agent-framework]] records Chase classifying the OpenAI Agents SDK as an agent framework. The same page attributes the framing to Viv Trivedy, the name [[DefinedTerm/harness-engineering]] also gives for the originator of "agent = model + harness".

## Where the answers diverge

Laid side by side, the accounts differ along a few distinct lines:

- **Boundary.** Whether tools and the execution environment are part of the harness or separate components beside it. Trivedy's inventory includes both, listing tools alongside bundled infrastructure such as a filesystem, sandbox and browser; Anthropic's Claude Code documentation and the OpenHarness README place tools inside the harness; Anthropic's four-way governance split names tools and environment as components of their own.
- **Kind of thing.** Whether a harness is the complement of the model in any agent (the broad answer), a category of package with frameworks and runtimes beside it (Chase), or something a builder obtains as a service (harness-as-a-service).
- **Scope.** Whether "harness" names a single agent working on a single task, a system above that dispatching to many (Gorinova et al.), or a team's practices around both (the methodological-harness proposal).
- **Durability.** [[DefinedTerm/harness-engineering]] records Anthropic reporting harness components dropped as models improved, and records that post closing on the position that the space of interesting harness combinations does not shrink as models improve but moves. The Trivedy post expects some harness functions to be absorbed into models while harness engineering stays useful. The methodological-harness proposal describes the technical harness as depreciating and the methodological harness as appreciating.

Several of the sources flag their own definitions as provisional. Chase says no clear definition exists yet, Trivedy calls his boundary the cleanest in his opinion, and the externalization review calls the concept still consolidating.
