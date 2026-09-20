---
title: "Model AI Governance Framework for Agentic AI"
type: "schema:TechArticle"
lang: en
tags: [agents, governance, human-oversight, agent-safety, multi-agent]
sources:
  - type: url
    url: 'https://www.imda.gov.sg/-/media/imda/files/about/emerging-tech-and-research/artificial-intelligence/mgf-for-agentic-ai.pdf'
    hash: sha256:ade20c2fa2aedf4f9ea3efe129e8b2ed3cc7823b414e766050586231d956645e
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An IMDA framework setting out the risks of agentic AI and emerging best practices for managing them, organised into four dimensions: bounding risk upfront, human accountability, technical controls, and end-user responsibility."
  publisher: "IMDA"
  datePublished: "2026-05-20"
---

The Model AI Governance Framework for Agentic AI, abbreviated MGF for Agentic AI, is a governance
document at version 1.5, published 20 May 2026 and updated 5 June 2026. IMDA is named in it as the
body that released a case study applying the framework, and the document describes itself as
building on its authors' previous model governance frameworks, specifically MGF (2020). It is
addressed to organisations looking to deploy agentic AI, and states its purpose as giving them a
structured overview of the risks of agentic AI and of emerging best practices for managing them,
so that agentic AI can be adopted with greater confidence. Its stated position is that existing
principles for trusted AI such as transparency, accountability and fairness continue to apply, but
need translating into practice for agents.

The framework opens with a component-level account of what an agent is. A simple agent is described
as a model acting as the reasoning engine, instructions that define its role and behavioural
constraints, and memory; to these are added planning and reasoning, tools, and protocols, and then
a safety and reliability layer of controls (access controls, guardrails, human approvals) and
logging and monitoring. Risks are then traced back to those components — a plan that contradicts
the user's intent, a hallucinated or wrongly-called tool, an untrusted MCP server that exfiltrates
data — on the stated view that the risks themselves are familiar (agents inherit traditional
software vulnerabilities and LLM-specific ones such as prompt injection) but manifest differently
through each new part.

The document is explicit that it is a living document, compiled with government agencies and
companies and intended to be updated as the field moves; version 1.5 records incorporating feedback
from more than 60 companies since v1.0, including the addition of systemic and multi-agent risks
and of new risk factors such as system complexity and use of third-party solutions.

## Details

The framework's central structure is four dimensions, presented as an iterative process rather than
a sequence — an anomaly found during monitoring is meant to send an organisation back to reassess
the earlier dimensions.

**Assess and bound the risks upfront.** Suitability is judged as a function of likelihood and
impact, against named factors: the domain's tolerance of error, the agent's access to sensitive data
and to external systems, the scope and reversibility of its actions, its level of autonomy, task
complexity, whether the agent is provided or operated by an external
party, and overall system complexity. Autonomy is one half of a distinction the framework draws
earlier between what an agent may do and how far it decides for itself; see
[[DefinedTerm/action-space]]. Bounding then happens through design — least-privilege access
to tools and data, SOPs constraining autonomy for process-driven tasks, and mechanisms to take
agents offline and limit their blast radius. The framework's general preference is stated plainly:
prefer deterministic rather than non-deterministic limits, and bound by design, so that an agent is
prevented from calling a tool by access control rather than instructed not to by a prompt. Agent
identity is treated as the other half of bounding: identities should be unique and cryptographically
verifiable, tied to a supervising agent, human or department, differentiated by the capacity in
which the agent acts, and catalogued centrally — the stated defence against
[[DefinedTerm/agent-sprawl]] — with authorisations scoped, time- or session-bound and
non-transferable. The framework offers as a rule of thumb that a human user should not be able to
set permissions for an agent greater than what that user is themselves authorised to do.

**Make humans meaningfully accountable.** The framework's difficulty here is that agent actions
emerge dynamically rather than from fixed logic, and that a value chain spanning model developers,
platform providers, system providers or app developers, tooling providers, deployers and end users
diffuses accountability. Its answer is explicit allocation, both inside the organisation (key
decision makers, product teams, cybersecurity teams, users) and in contracts with external parties,
combined with designing for meaningful oversight: defining significant checkpoints that require
human approval — high-stakes actions, irreversible actions, outlier behaviour, and user-defined
thresholds — and keeping approval requests contextual and digestible rather than dumping raw logs.
It treats the continued effectiveness of that oversight as something to be measured rather than
assumed; see [[DefinedTerm/automation-bias]].

**Implement technical controls and processes.** Controls are recommended for the new agentic
components specifically — prompting an agent to reflect on whether its plan adheres to instructions
and logging that plan; strict input formats and least-privilege tools; whitelisting trusted MCP
servers and sandboxing code execution; requiring agents to communicate through typed function calls
rather than free text and limiting shared memory between them. The document also floats MCP itself
as a governance layer, since it sits between the agent and the systems it reaches. Testing is
treated as needing new dimensions beyond output correctness: overall task execution, policy
compliance, tool calling, and robustness, tested across whole workflows, at the multi-agent system
level, in realistic environments, and repeatedly across varied datasets. Deployment is expected to
be gradual and continuously monitored, with alert thresholds, anomaly detection, agents monitoring
other agents, immutable logs, and denial by default when approval infrastructure fails.

**Enable end-user responsibility.** Users are split into those who interact with agents, for whom
the emphasis is transparency, and those who integrate agents into their work processes, for whom
education and training are layered on top. The framework specifically raises loss of tradecraft as a
business continuity risk: as agents take over entry-level tasks that normally serve as training,
users may lose the operational knowledge needed when agents malfunction or become unavailable.

Several case studies bear directly on agentic coding. GovTech's phased rollout of agentic coding
assistants — Windsurf and GitHub Copilot in Agent Mode from October 2025, [[SoftwareApplication/claude-code]]
from April 2026 — is described as deliberately contained in its first phase to internal employees,
no MCP, and low-risk systems, while central logging and an MCP Governance Framework were built for
the second; its recorded learnings include reducing approver cognitive load by allowing OS-native
sandboxes. Tencent's [[SoftwareApplication/codebuddy]] is used to illustrate approval requirements
calibrated to action risk. An IMDA case study applies all four dimensions to deployments of
[[SoftwareApplication/openclaw]]. The framework also notes, in its discussion of human oversight,
that users who use agents to "vibe code" may not have the software engineering expertise to review
the robustness of the generated code.
