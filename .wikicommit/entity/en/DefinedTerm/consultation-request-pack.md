---
title: "Consultation Request Pack"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, human-ai-collaboration, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "In the Structured Agentic Software Engineering framework, a structured artifact an agent generates mid-task to request human expertise, documenting the specific uncertainty or decision point together with options, trade-offs, and a recommendation."
  termCode: "CRP"
---

A Consultation Request Pack (CRP) is the artifact proposed in [[DefinedTerm/structured-agentic-software-engineering]] for agent-initiated human consultation. It is generated when an agent requires human input to proceed, and it documents the specific uncertainty or decision point in a structured form rather than as an open-ended question in a chat log. [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] presents it as the mechanism that makes the human-agent partnership bi-directional: agents are not only issued instructions, they can call on humans.

## Usage

A CRP is contextualized by the active [[DefinedTerm/briefing-script]] and may be triggered by LoopScript or MentorScript rules. The paper's worked example structures it around a decision point with an issue summary and details, a set of labelled options each carrying pros, cons, and an estimated effort, an explicit agent recommendation with reasoning, the specific decision being requested, and an escalation target naming the role that should decide.

Routing is handled by the [[DefinedTerm/agent-command-environment]], which presents and records the request; the paper describes this as the ACE treating humans as callable expertise endpoints while preserving the context needed for accountability. The example given is an agent routing a database schema issue to the designated database architect, who provides feedback through the ACE — and the authors note that in more advanced settings that "architect" role may itself be filled by another specialized agent.

The human response is not an informal reply. In the framework, reviewing and answering a CRP falls under an activity called Agentic Guidance Engineering (AGE), which produces a Version-Controlled Resolution (VCR) explicitly linked to the artifact it addresses, preserving traceability and enabling downstream auditing and learning. The ACE is specified to provide an inbox-like interface for triaging CRPs.

The paper argues the CRP is what elevates the human from a passive approver of outputs to an active, on-demand consultant who intervenes precisely where their expertise adds the greatest value, and that without explicit, durable artifacts of this kind, multi-actor workflows would be ephemeral, untraceable, and ultimately unmanageable. The authors list "consultability as a first-class artifact" among the points differentiating their framework from adjacent efforts, describing the CRP as enabling traceable cross-role handovers and shifting the paradigm from solo agentic coding to team-based agentic software engineering.

## Related Terms

The CRP is one of two agent-generated artifacts in the framework; the other is the [[DefinedTerm/merge-readiness-pack]], submitted when the agent has finished rather than when it is stuck. Agents raise CRPs from within the [[DefinedTerm/agent-execution-environment]], and humans triage them in the [[DefinedTerm/agent-command-environment]].
