---
title: "Open SWE"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, agent-sandboxing, agentic-code-review]
sources:
  - type: url
    url: 'https://github.com/langchain-ai/open-swe'
    hash: sha256:b404a7534d6291d6cf852031e7a8d7ee3facfa37c0dfa55f5abe310cde60e19d
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "LangChain's open-source asynchronous coding agent, built on Deep Agents and run on LangGraph, that takes a code-change task from a dashboard, GitHub, Slack, Linear or a schedule and works in an isolated sandbox to deliver a pull request — and that also reviews pull requests, learns a repository's review style and monitors CI."
  applicationCategory: "Agentic coding platform"
  featureList: "Five LangGraph graph entrypoints (Agent, Reviewer, Analyzer, Chat, Scheduler); per-thread persistent sandboxes; read-only PR review and PR chat; CI monitoring with /baby-sit; dashboard, GitHub, Slack, Linear and experimental desktop surfaces; pluggable sandbox providers"
  author: "LangChain"
---

Open SWE is LangChain's open-source asynchronous coding agent, which the project describes as an
open-source **software factory** built on Deep Agents. A code-change task arrives from the
dashboard, GitHub, Slack or Linear — or on a schedule — and the agent works in an isolated
environment to understand the codebase, make changes, validate them and deliver a pull request.

The project states that it goes beyond code generation: it can review pull requests, learn a
repository's review style, monitor CI and respond to feedback. It is open source under an MIT
license, deployable in the operator's own infrastructure, and designed to be adapted to a team's
repositories, tools, policies and workflows. The repository carries a note that Open SWE is under
active development and that APIs, setup and product surfaces may continue to evolve.

## Capabilities

The project groups what it does into four areas. Under **build** it investigates repositories,
plans work, edits code, runs focused validation, commits and pushes, and opens or updates pull
requests, using subagents to parallelize research and independent work and supporting reusable
skills, repository instructions and custom workspaces. Under **review** it runs read-only pull
request reviews on demand or automatically, learns repository-specific review preferences from
historical feedback, supports read-only PR chat for investigating a change without modifying it, and
keeps findings grounded in the diff before publishing them back to GitHub. Under **operate** it
takes tasks from the dashboard, GitHub, Slack and Linear, schedules recurring work through
deterministic automations, monitors opted-in pull requests with a `/baby-sit` command that diagnoses
CI failures and reruns only evidence-backed flaky jobs, and routes follow-up messages to the
original thread and sandbox. Under **customize** the models and reasoning effort, integrations,
toolset, sandbox providers, middleware, skills, triggers and delivery policies can all be changed,
along with personal and repository coding instructions and organization-wide review guidelines.

The unit of work is a **thread**: a durable conversation and work context that can contain multiple
invocations, each an agent execution triggered by a message or automation. An initial request and a
follow-up belong to one thread and produce two invocations, each with its own usage; independent
threads run in parallel, and the same thread carries context from request through delivery and
follow-up. Read-only PR chat needs no sandbox, and desktop work can run directly against an
allowlisted local project.

## Architecture

The project is explicit about the separation between the agent harness and the runtime.
**Deep Agents is the harness** — it supplies the planning, file operations, shell access, skills,
state and subagent primitives, while Open SWE adds the software-engineering tools, prompts,
middleware, integrations, authorization and product surfaces needed for end-to-end engineering work.
The project's stated reason for composing it this way is that the system stays extensible and
inherits improvements from the underlying LangChain agent stack.

**LangGraph is the runtime**, providing durable execution and thread state; each invocation executes
as a LangGraph run within a thread. Open SWE ships five graph entrypoints, each with its own role:
Agent (plans, implements, validates and delivers changes), Reviewer (read-only pull request
reviews), Analyzer (learns repository-specific review style), Chat (answers questions about pull
requests without changing code), and Scheduler (dispatches recurring tasks and CI monitoring).

**Sandboxes contain the work.** Cloud work runs in isolated Linux sandboxes carrying the development
tooling that the workspace's setup scripts or snapshot supply, and each cloud coding thread is bound to its own persistent
sandbox so the agent can continue from prior work when a human replies. The project states a
deliberate failure policy here: an unreachable coding sandbox is not silently replaced — Open SWE
fails safely rather than risk discarding uncommitted work. LangSmith is the default sandbox and
tracing provider, with Modal, Daytona, Runloop, E2B and local execution also supported behind a
pluggable interface.

## Control and safety

The project frames the problem as needing both autonomy and boundaries, and lists what it provides:
per-thread sandbox isolation and persistent workspaces for cloud coding; GitHub App installation
boundaries with optional per-user OAuth; organization and repository allowlists with actor
authorization checks; credentials held in the server process or injected through a sandbox proxy;
human approval before pushing workflow-file changes; read-only reviewer and PR chat agents; a plan
mode for reviewing an approach before code changes; and opt-in automatic review and CI monitoring.

It also states the residual risk plainly rather than as a caveat: sandboxes can have network access
and powerful tools, so deployments should use least-privilege credentials, restrict which
repositories and integrations are enabled, and tailor approval rules to their environment.

## Adoption & Ecosystem

One deployment serves the API, the webhooks and the dashboard from a single URL. It runs on
LangGraph Platform or Docker; production self-hosting uses the standalone LangGraph Agent Server and
requires its license key. The repository publishes a generated OpenAPI 3.1 contract
(`swagger.json`) for its FastAPI backend, and notes that some request/response schemas and
authentication requirements are not yet documented there and that LangGraph runtime endpoints are
not included.

The desktop client is experimental: packaged releases target macOS, while source builds also support
Windows and Linux. The repository states that Open SWE is built in the open by LangChain and is
evolving quickly.
