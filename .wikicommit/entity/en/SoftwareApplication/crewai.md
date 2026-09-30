---
title: "CrewAI"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, multi-agent, orchestration, agent-tooling]
sources:
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/agent/multi-agent/'
    hash: sha256:644e8c22de6fd778cefa3c3c44647eee3beb025a3fb81617e0411c473018e2c9
  - type: url
    url: 'https://aise.phodal.com/agent-for-aise.html'
    hash: sha256:25e468d7ba5ae035373a0284184294acc7158b0787c0e16b94a2c358beceec39
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A multi-agent framework built around role-based agent teams, in which each agent carries a role and a goal and a Flow defines whether tasks run in sequence or in parallel. It is characterised by a handbook chapter on multi-agent systems as the fastest route to a team with clear responsibilities, at the cost of limited control over what context each agent receives."
  applicationCategory: "Agent orchestration framework"
  featureList: "role and goal attributes per agent; Flows for sequential or parallel workflow definition with automatic task-dependency handling; States as per-step execution context; Tracing & Observability for agent and workflow metrics and logs; max_rpm as an API call-rate limit; max_execution_time and max_iter as execution-budget bounds; max_retry_limit as a retry cap; autonomous delegation and querying between agents; sequential and hierarchical processes; task output saved to a file or parsed into a Pydantic model or JSON"
---

CrewAI is a framework for building [[DefinedTerm/llm-based-multi-agent-system]]s around role-based
agent teams. In the account a handbook chapter on multi-agent systems gives, each agent is
configured with attributes including a `role` and a `goal`, so that a crew is assembled the way a team is — a researcher agent, a writer agent, an
editor agent — rather than wired as a graph of computation steps. That chapter characterises it as
offering centralised orchestration with minimal configuration and consistent persona behaviour, and
names limited context control as the corresponding weakness. A survey of coding agents in an online
book on AI-assisted software engineering lists its features in similar terms — role-based agent
design, autonomous delegation between agents, and process-driven task execution.

## Capabilities

Workflow structure is expressed through **Flows**, which support defining tasks in sequence or in
parallel and which handle dependencies between them automatically. Flows also carry an execution
context the handbook chapter calls **States**, holding environment data and intermediate results at each step,
which is what makes a run traceable as it moves between states. Alongside that, the framework
provides a **Tracing & Observability** facility for monitoring agent and workflow metrics and logs in
real time.

For containing the cost of a multi-agent run, the handbook chapter names settings in the agent configuration
under three of its four headings. Under call quotas, `max_rpm` limits the rate of API calls (its
worked figure is `max_rpm=10`), with `max_execution_time` and `max_iter` named among parameters that
bound the execution budget — the list is written as open-ended rather than complete. Under budget
monitoring it notes that a CrewAI Enterprise plan offers unified budget and alerting policies. Under
retry and circuit-breaking, `max_retry_limit` caps retries so that a failing agent does not spin in
an unbounded loop. Its fourth heading, malicious-input filtering, names no framework at all: it says
that validating user input for format and length, and using content review or allow/deny lists, has to
be implemented oneself in open-source frameworks, and that a cockpit layer can insert validation tools
before and after the call chain. The chapter does not say which of the frameworks it compares are open
source, so nothing there settles whether this applies to CrewAI.

The AI-assisted software engineering survey gives a separate feature list. Agents are designed around
roles, each customisable with its own role, goal and tools. Agents can delegate tasks to one another
autonomously and query each other, which the survey presents as improving problem-solving efficiency.
Tasks are defined with customisable tools and assigned to agents dynamically. Execution is
process-driven: sequential task execution and hierarchical processes are supported, with more complex
processes such as consensus-based and autonomous ones described as under development. The output of
an individual task can be saved to a file, or parsed into a Pydantic model or JSON, and a crew can run
on OpenAI models or on open-source models, including locally run ones.

## Adoption & Ecosystem

The handbook chapter places CrewAI against four architecture patterns and matches it to the **centralised**
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
- [[SoftwareApplication/langgraph]] — the graph-structured alternative the handbook chapter contrasts it with
- [[DefinedTerm/manager-pattern]] — a coordination shape of the kind the handbook chapter's 集中式
  (centralised) pattern describes; the chapter itself does not use this name
