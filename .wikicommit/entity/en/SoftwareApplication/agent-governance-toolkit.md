---
title: "Agent Governance Toolkit"
type: "schema:SoftwareApplication"
lang: en
aliases: ["AGT"]
tags: [agents, governance, security, agent-safety, mcp]
sources:
  - type: url
    url: 'https://github.com/microsoft/agent-governance-toolkit'
    hash: sha256:e60d3eb7cbdc877fd12d392ceaef384f6963142b75d3719e319c020d7d0b0e3d
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An open-source toolkit from Microsoft that enforces policy on autonomous AI agents in deterministic application code rather than in the prompt — intercepting every tool call, message and delegation before it reaches the model's wire, and adding identity, sandboxing and audit layers around it."
  applicationCategory: "AI agent governance and policy enforcement"
  featureList: "Policy engine, zero-trust agent identity, execution sandboxing, tamper-evident audit logging, MCP security gateway, compliance verification CLI"
  author: "Microsoft"
---

The Agent Governance Toolkit (AGT) is an open-source toolkit published by Microsoft for governing
autonomous AI agents in production. Its stated scope is policy enforcement, identity, sandboxing
and site-reliability engineering for agents, installed through a single package and usable with any
agent framework. At the time the repository was read it was marked **Public Preview** —
production-quality releases that may still carry breaking changes before general availability — and
was licensed under the MIT License.

The project frames its purpose around three questions an operator cannot answer once agents act
autonomously: whether a given action is allowed, which agent in a multi-agent system performed it,
and whether what happened can be proved afterwards. It argues that OAuth scopes and IAM roles
control only which services an agent can reach, not what it does once connected, and that five
agents sharing one API key make "an agent did it" useless as incident response.

AGT's central design claim is that prompt-level safety is not a control surface. The repository
argues this is a polite request to a stochastic system, and points to published industry guidance on
prompt injection, to published adaptive-attack results, and to Microsoft's own red-teaming work as
evidence that model-layer defences remain probabilistic by construction. Rather than contest that inside the prompt, AGT
intercepts every tool call, message send and delegation in deterministic application code before
the model's intent reaches the wire — so that actions its kernel denies are, in the project's
phrasing, structurally impossible rather than merely unlikely.

## Capabilities

The smallest unit of use is a single wrapper: `govern()` takes a tool function and a YAML policy
file and returns a governed callable that evaluates the policy on every call, writes the decision
to an audit trail, and raises `GovernanceDenied` when the policy blocks the action. Policies are
YAML documents of named rules, each with a condition and an action — `deny` and `require_approval`
(with a named approver group) are both shown. A fuller `AgentControl` API loads a manifest and
evaluates intervention points programmatically, returning a verdict.

The repository describes a layered architecture — policy engine, then identity, then audit log —
in which every layer is optional, and states that most teams run policy enforcement plus audit
logging without adopting the full stack. The policy engine accepts YAML, OPA or Cedar; identity is
handled through SPIFFE, DID or mTLS; the audit log is described as tamper-evident, producing a
decision record per evaluation.

Functionality is grouped into named packages: **Agent OS** (policy engine, agent lifecycle,
governance gate), **Agent Control Specification** (a stateless, deterministic, fail-closed policy
decision runtime with a Rust core), **Agent Mesh** (discovery, routing, trust mesh), **Agent
Runtime** (execution sandboxing across four privilege rings), **Agent SRE** (kill switch, SLO
monitoring, chaos testing), **Agent Compliance**, **Agent Marketplace**, **Agent Lightning**
(reinforcement-learning training governance) and **Agent Hypervisor**. Additional capabilities
named separately include an MCP Security Gateway covering [[DefinedTerm/tool-poisoning]], drift monitoring,
typosquatting and hidden-instruction scanning; Shadow AI Discovery for finding unregistered agents
across processes, configs and repositories; a governance dashboard; a twelve-vector prompt
injection evaluator; and a contributor-reputation GitHub Action for screening pull-request authors.

A command-line tool, `agt`, exposes installation checks (`agt doctor`), OWASP compliance
verification (`agt verify`, with a `--strict` mode that fails CI on weak evidence), a prompt
injection audit (`agt red-team scan`, with a minimum-grade threshold) and policy linting.

## Adoption & Ecosystem

AGT ships SDKs for Python, TypeScript, .NET, Rust and Go. The repository states that all five
implement core governance — policy, identity, trust and audit — while Python carries the full
stack, and that the Copilot CLI and Claude Code packages are first-party developer surfaces built
on the TypeScript SDK. For [[SoftwareApplication/claude-code]] specifically, AGT is installed by
adding the repository as a plugin marketplace and installing its governance plugin. As of v4.1.0
the Python side was consolidated from 45 packages into five top-level distributions, with the
previous package names left installable as redirecting stubs.

Framework integration is listed as native for [[SoftwareApplication/microsoft-agent-framework]]
(middleware) and for Semantic Kernel (.NET and Python), adapters for AutoGen, LangGraph/LangChain, CrewAI, Google ADK and Mastra, middleware for
the OpenAI Agents SDK and LlamaIndex, and further integrations for Haystack, Dify and Azure AI
Foundry.

The project puts unusual weight on written specifications: it states that every major component
has a formal RFC 2119 specification with conformance tests defining what implementations MUST,
SHOULD and MAY do, listing ten such specifications backed by 992 conformance tests, alongside 29
architecture decision records. It also publishes compliance mappings against the OWASP Agentic AI
Top 10, NIST AI RMF 1.0, the EU AI Act and SOC 2.

The repository is candid about one boundary: AGT enforces governance at the application middleware
layer, not the OS kernel, so the policy engine and the agents it governs share a process. Its own
production recommendation is therefore to run each agent in a separate container for OS-level
isolation, and it maintains a documented list of known limitations.
