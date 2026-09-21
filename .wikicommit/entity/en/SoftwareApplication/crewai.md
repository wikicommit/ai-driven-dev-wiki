---
title: "CrewAI"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, multi-agent, orchestration, agent-tooling]
sources:
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/agent/multi-agent/'
    hash: sha256:644e8c22de6fd778cefa3c3c44647eee3beb025a3fb81617e0411c473018e2c9
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A multi-agent framework built around role-based agent teams, in which each agent carries a role and a goal and a Flow defines whether tasks run in sequence or in parallel. It is characterised by its source as the fastest route to a team with clear responsibilities, at the cost of limited control over what context each agent receives."
  applicationCategory: "Agent orchestration framework"
  featureList: "role and goal attributes per agent; Flows for sequential or parallel workflow definition with automatic task-dependency handling; States as per-step execution context; Tracing & Observability for agent and workflow metrics and logs; max_rpm as an API call-rate limit; max_execution_time and max_iter as execution-budget bounds; max_retry_limit as a retry cap"
---

CrewAI is a framework for building [[DefinedTerm/llm-based-multi-agent-system]]s around role-based
agent teams. In the account given here, each agent is configured with attributes including a `role`
and a `goal`, so that a crew is assembled the way a team is — a researcher agent, a writer agent, an
editor agent — rather than wired as a graph of computation steps. Its source characterises it as
offering centralised orchestration with minimal configuration and consistent persona behaviour, and
names limited context control as the corresponding weakness.

## Capabilities

Workflow structure is expressed through **Flows**, which support defining tasks in sequence or in
parallel and which handle dependencies between them automatically. Flows also carry an execution
context the source calls **States**, holding environment data and intermediate results at each step,
which is what makes a run traceable as it moves between states. Alongside that, the framework
provides a **Tracing & Observability** facility for monitoring agent and workflow metrics and logs in
real time.

For containing the cost of a multi-agent run, the source names settings in the agent configuration
under three of its four headings. Under call quotas, `max_rpm` limits the rate of API calls (its
worked figure is `max_rpm=10`), with `max_execution_time` and `max_iter` named among parameters that
bound the execution budget — the list is written as open-ended rather than complete. Under budget
monitoring it notes that a CrewAI Enterprise plan offers unified budget and alerting policies. Under
retry and circuit-breaking, `max_retry_limit` caps retries so that a failing agent does not spin in
an unbounded loop. Its fourth heading, malicious-input filtering, names no framework at all: it says
that validating user input for format and length, and using content review or allow/deny lists, has to
be implemented oneself in open-source frameworks, and that a cockpit layer can insert validation tools
before and after the call chain. The source does not say which of the frameworks it compares are open
source, so nothing there settles whether this applies to CrewAI.

## Adoption & Ecosystem

The source places CrewAI against four architecture patterns and matches it to the **centralised**
one, where a single coordinating agent allocates tasks, monitors progress and synthesises results. Its
stated best use is role-based collaboration and rapid prototyping — the example given is content
automation for a marketing team — and its stated limitation is limited context control. Its own image
for the comparison is a traffic-control system: where [[SoftwareApplication/langgraph]] supplies
flexible interchanges for complex conditional routing and state persistence, CrewAI supplies a simple
organisational structure of clear job descriptions and a team leader.

In the same chapter's 2026 survey of the framework ecosystem, CrewAI is listed as under active
iteration and as the mainstream choice for centralised orchestration and rapid prototyping, alongside
[[SoftwareApplication/langgraph]], [[SoftwareApplication/microsoft-agent-framework]],
[[SoftwareApplication/openai-agents-sdk]] and [[SoftwareApplication/openhands]]. Nothing in that
chapter's account of CrewAI is backed by a figure or a measurement.

## Related Terms

- [[DefinedTerm/llm-based-multi-agent-system]] — the arrangement this framework coordinates
- [[SoftwareApplication/langgraph]] — the graph-structured alternative the same source contrasts it with
- [[DefinedTerm/manager-pattern]] — a coordination shape of the kind the source's 集中式
  (centralised) pattern describes; the source itself does not use this name
