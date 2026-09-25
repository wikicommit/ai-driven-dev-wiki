---
title: "Agent Development Kit (ADK)"
type: "schema:SoftwareApplication"
lang: en
sources:
  - type: url
    url: 'https://developers.googleblog.com/build-better-ai-agents-5-developer-tips-from-the-agent-bake-off/'
    hash: sha256:1531476aa716dcaf43b35914743fee4765992073720af2d19e509b1086ea47f4
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/agent/multi-agent/'
    hash: sha256:644e8c22de6fd778cefa3c3c44647eee3beb025a3fb81617e0411c473018e2c9
  - type: url
    url: 'https://codelabs.developers.google.com/devsite/codelabs/build-agents-with-adk-empowering-with-tools'
    hash: sha256:2152382ceca36b4b1abbac67cb7be849b6e50ea99799ce35758a70efb4f2d20b
  - type: url
    url: 'https://codelabs.developers.google.com/sdlc/instructions'
    hash: sha256:ed5d01ab1f229b1c0f5543df1541841ed81d141c60c442f41d9ad008c38881ee
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"
tags: [agents, multi-agent-systems, agent-tooling, tool-use]

properties:
  description: "A framework for building AI agents, distributed at adk.dev and presented by Google as one of its quickstart resources for building agent applications. A second source places it as a coordination framework designed for hierarchical composition of specialised agents."
  applicationCategory: "Agent development framework"
  author: "[[Organization/google]]"
  featureList: "flexible orchestration patterns; hierarchical agent composition; a built-in evaluation framework; native Vertex AI integration; an Agent Starter Pack for production deployment; function, built-in and third-party tools; AgentTool for using an agent as a tool; adk web development UI"
---

The Agent Development Kit (ADK) is a framework for building AI agents, distributed at
adk.dev. Google presents it on its own developer blog as a quickstart resource for
building agent applications rather than assembling them from custom integration code,
and publishes documentation for using it to build multi-agent systems.

## Capabilities

Google's developer writing suggests ADK as the vehicle for building a multi-step agent
that layers in open agent protocols one at a time — the worked suggestion is a supply
chain agent for a restaurant that, as protocols are added, can check real inventory
databases, communicate with remote supplier agents, execute secure transactions and
render interactive, streaming dashboards. The framework is presented as something to
combine with open standards such as [[DefinedTerm/model-context-protocol]], and Google's
argument for it is that doing so avoids writing and maintaining brittle integration code
for every tool an agent touches.

### Tools

A Google Codelabs tutorial in its "Building AI Agents with ADK" series describes a tool in ADK as a
modular piece of code that lets an agent perform specific actions, such as looking up real-time data
or calling an external API, and divides ADK's tools into three categories: **function tools**, custom
tools a developer writes; **built-in tools** the framework provides for common operations, such as
Google Search and code execution; and **third-party tools** from external libraries, including tools
from [[SoftwareApplication/langchain]] and [[SoftwareApplication/crewai]]. In the tutorial a Python
function is wrapped as a `FunctionTool`, and the tutorial stresses that the function's name and
docstring are what the agent's model reads to decide what the tool does and when to use it, calling a
clear docstring the single most important factor in the agent using the tool correctly.

The same tutorial shows a pattern it presents as fundamental: using a specialised agent as a tool. A
search agent whose only tool is Google Search is wrapped with `AgentTool`, which packages an entire
agent to look and act like a standard tool, and handed to a root agent alongside other tools; the root
agent then acts as an orchestrator or router that passes each request to the right tool. The tutorial
runs and inspects the agent through the `adk web` development UI, whose event inspector shows which
tool the agent called.

### Agent types and evaluation

Google's "AI Agent End to End" workshop builds two ADK agents that illustrate a distinction between
agent classes. A story-writing agent uses `LlmAgent`, which the workshop calls declarative: the model
generates the output from instructions. An image-generating agent instead uses `BaseAgent`, which the
workshop calls imperative: the developer writes the exact step-by-step logic in its `_run_async_impl`
method and calls the image tool directly rather than letting the model decide whether to. The workshop
recommends `BaseAgent` where an agent must follow a fixed sequence of steps, call a tool without model
intervention, or run logic too complex for a model to infer reliably from a prompt.

The same workshop describes ADK's evaluation framework as an automated way to test whether an agent's
behaviour meets expectations, rather than only whether its code runs. An `evalset.json` file holds eval
cases, each a sample conversation with the ideal "golden" response, and a `test_config.json` file sets
the criteria for success, such as a `response_match_score` threshold and custom evaluators; results are
viewed in the eval tab of the `adk web` UI. The workshop has [[SoftwareApplication/gemini-cli]] generate
these files from a prompt.

Google distributes an accompanying Agent Starter Pack alongside it, described as a route
to deploying production-grade agents.

A chapter of Jimmy Song's online handbook 智能体构建指南, comparing six agent coordination
frameworks, names four strengths for ADK: flexible orchestration, support for hierarchical agent
composition, a built-in evaluation framework, and native Vertex AI integration. That chapter matches ADK
to the **hierarchical** architecture pattern — multiple layers of supervision in which upper layers
abstract complexity and lower ones carry out detail — naming it there alongside
[[SoftwareApplication/langgraph]], and saying ADK is particularly suited to it because it is designed
for composing specialised agents into modular, scalable applications. Its stated best use
there is building [[DefinedTerm/llm-based-multi-agent-system]]s on Google Cloud Platform. That
chapter gives no figure or measurement in support of its account of ADK.
