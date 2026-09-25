---
title: "Agent Harness"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, agent-tooling, verification, agent-state, benchmarking]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.18747'
    hash: sha256:b1035aaed7f12c5fa8504dac7f47c2e10dda381065834be2cea784c2f758fb1f
  - type: url
    url: 'https://arxiv.org/pdf/2606.17799'
    hash: sha256:98d0e3aebf3d1c5ab551f46a6c1f719389e820d2be1490bfefd669d87c107e69
  - type: url
    url: 'https://blog.langchain.com/agent-frameworks-runtimes-and-harnesses-oh-my/'
    hash: sha256:dbbb531bd6a1b614e8c6537f3fe67ea744c2f9b7a8532abd9bfc3cd413ce1729
  - type: url
    url: 'https://blog.langchain.com/the-anatomy-of-an-agent-harness/'
    hash: sha256:71cffd4adc7b81b7dd5f981d26af2bebcee592b2751a882ea95bb833fa2d022e
  - type: url
    url: 'https://code.claude.com/docs/en/how-claude-code-works'
    hash: sha256:bd22d00c3d6884ed8323b1d1a90abe77a12c9df0272a5a855041afec603c6196
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The policy-governed system around a language model that grounds its outputs in external execution, persistent state and verifiable feedback, turning a stateless model into a functional agent. In the vocabulary of Gorinova et al., it is the inner of two orchestration levels — one model working with tools towards a single task — as distinguished from the system harness that decomposes goals and dispatches tasks to it."
---

An agent harness is what turns a stateless language model into a functional agent, by grounding its outputs in external execution, persistent state and verifiable feedback. [[ScholarlyArticle/code-as-agent-harness]] frames the central design question for any harness as a question about medium — what connects the model to its task environment — and argues that code is the answer, because code is executable, inspectable and stateful in ways natural language is not. On that account these are not properties of code as a notation but the properties that make it function as a harness interface: executability means the harness can verify what the model intended, inspectability means failures can be diagnosed and fed back, and statefulness means the agent's interaction history is not lost between steps.

[[ScholarlyArticle/coding-benchmarks-are-misaligned-with-agentic-software-engineering]] uses the term more narrowly, as one of two levels of orchestration. There, an agent harness is a language model interacting with tools, working towards a single task, with some system prompt and context to draw on; the [[DefinedTerm/system-harness]] is the outer layer that turns higher-level goals into concrete tasks, dispatches each to one or more agent harnesses, manages the environment they act on and routes their outputs through feedback. On that reading most artefacts described as "coding agents" — the paper names Claude Code, Codex, Cursor Agent, SWE-Agent and OpenHands among them — are agent harnesses in this sense. The same paper treats an agent harness as a configurable executor composed of model, prompt, tools and loop, which the surrounding system harness may tune or treat as a black box.

## Usage

The survey distinguishes the harness from the code running inside it. Code is an executable medium *within* the harness; the harness is the larger policy-governed system deciding what code may be executed, trusted, persisted, reused or promoted into future workflows. Reliability, on this framing, depends not only on the model's judgement and on agent-authored artefacts but on human-designed policies, sandbox boundaries, permission tiers, verification oracles, audit logs and human-review gates.

Three roles are identified for code at the harness interface. **Code for reasoning** externalises internal logic into verifiable computation that interpreters, symbolic solvers or execution traces can check and refine. **Code for acting** translates high-level intent into executable operations grounded in embodied, GUI, software or tool-use environments — with the survey emphasising that executable action code is an interface to perception, affordance estimation, controllers and safety layers, not a replacement for them. **Code for environment modelling** represents world state, transition dynamics and feedback signals through program states, repositories, simulators, tests and logs the agent can execute, edit and query.

Above that interface sit the harness mechanisms the survey groups into five interacting categories: planning, which organises long-horizon execution; memory and context engineering, described as a state-management layer deciding what stays in active context, what is compacted into summaries and what is offloaded to durable external storage; tool use, treated as a governed interface between model intent and external systems rather than an auxiliary capability; control through the [[DefinedTerm/plan-execute-verify-loop]]; and [[DefinedTerm/harness-engineering]], which studies how the harness itself can be measured and improved.

The survey also treats the harness as a safety governor rather than only a context manager or tool executor — a layer that classifies proposed actions by risk, enforces permission tiers, denies actions violating hard constraints and requires human approval for irreversible or externally consequential transitions. Its proposed structure is a multi-tier permission model: a read-only tier for browsing, retrieval, static inspection and log analysis; a sandbox-edit tier for local patching, test execution and temporary dependency installation inside an isolated workspace; and a full-access tier covering network access, credentials, deployment commands, package publishing, destructive filesystem operations and Git history mutation. The authors argue permissions should depend not only on tool identity but also on arguments, environment state, data sensitivity and expected side effects, since the same command may be safe in a disposable sandbox and unsafe in a production repository.

A further argument the survey makes about safety is that human-in-the-loop control should become durable harness state rather than an occasional prompt interruption: each approval, rejection, policy exception or reviewer correction should update the harness's permission rules, escalation policy, verification criteria and future memory retrieval, and high-stakes approvals should be auditable state transitions recording what was proposed, what evidence was shown, what risks were surfaced, who decided and what responsibility boundary changed. The authors call this executable accountability.

Gorinova et al. use the agent harness as an argument about measurement: because the harness is part of what a benchmark actually scores, a leaderboard entry naming only a model is under-specified. They reproduce Terminal-Bench entries for a single fixed model across several agent harnesses in which accuracy ranges from roughly 58% to roughly 80%, and argue that since the model is fixed the spread cannot be explained as a difference in model capability — it shows that prompt, tool interface, action loop, environment handling, retry behaviour and terminal conventions are part of the measured object. They add that a model may have been trained or tuned under particular tool-use conventions, so a harness can be well or poorly matched to a model before any task-specific reasoning begins.

LangChain's Harrison Chase uses the term for a position in a layering of agent-building software
rather than for the system around a model in general. In
[[BlogPosting/agent-frameworks-runtimes-and-harnesses]] he places an agent harness above an
[[DefinedTerm/agent-framework]]: where a framework's value is its abstractions and an
[[DefinedTerm/agent-runtime]] beneath it supplies production infrastructure, a harness adds default
prompts, opinionated handling of tool calls, planning tools and filesystem access — "batteries
included". His example is LangChain's own [[SoftwareApplication/deep-agents]], built on LangChain and
described as a "general purpose version of Claude Code"; he reads the Claude Agent SDK as Claude
Code's step in the same direction and allows that all coding CLIs could be argued to be agent harnesses
of a kind. He states that he did not come up with the term and that its definition, like the
boundaries between the three layers, was not yet clear.

A later LangChain post by Vivek Trivedy, [[BlogPosting/the-anatomy-of-an-agent-harness]], proposes a much
broader definition than Chase's layering: "Agent = Model + Harness", and "if you're not the model, you're
the harness". On this account a harness is every piece of code, configuration and execution logic that is
not the model itself — system prompts; tools, skills and MCP servers with their descriptions; bundled
infrastructure such as a filesystem, sandbox and browser; orchestration logic such as subagent spawning,
handoffs and model routing; and hooks or middleware for deterministic execution such as compaction,
continuation and lint checks. A raw model is not an agent, the post argues, until a harness gives it state,
tool execution, feedback loops and enforceable constraints. Trivedy offers this as, in his opinion, the
cleanest of many possible ways to draw the boundary, and derives each component by working backwards from
something a model cannot do on its own: the filesystem for durable state, bash and code execution as a
general-purpose tool, sandboxes for safe execution and self-verification, memory files and search for
knowledge beyond the weights, [[DefinedTerm/compaction]] and [[DefinedTerm/tool-call-offloading]] against
[[DefinedTerm/context-rot]], and the [[DefinedTerm/ralph-loop]] and planning for long-horizon work. The
post also argues that because products such as Claude Code and Codex are post-trained with their harness
in the loop, a model can overfit to that harness — yet the best harness for a given task is not
necessarily the one the model was trained with.

Anthropic's own documentation uses the term in the same broad sense for its product. Describing how
[[SoftwareApplication/claude-code]] works, it says the agentic loop is powered by two components —
models that reason and tools that act — and that Claude Code is the layer around the model that
provides the tools and manages the context the model sees, which it identifies as what the term
agentic harness refers to. The loop that harness runs is described as three blended phases: gathering
context, taking action and verifying results.

## Related Terms

- [[DefinedTerm/system-harness]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/plan-execute-verify-loop]]
- [[DefinedTerm/agent-scaffold]]
- [[DefinedTerm/harness-as-a-service]]
- [[DefinedTerm/ai-coding-agent]]
- [[DefinedTerm/agent-framework]]
- [[DefinedTerm/agent-runtime]]
- [[SoftwareApplication/deep-agents]]
- [[DefinedTerm/tool-call-offloading]]
- [[BlogPosting/the-anatomy-of-an-agent-harness]]
