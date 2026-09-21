---
title: "Schema Gating"
type: "schema:DefinedTerm"
lang: en
tags: [agent-safety, agent-tooling, agent-architecture]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.05344'
    hash: sha256:29a5dfd46c7505affc599f6922ebba2f67d01e7f3a343df5347a42f435a08edc
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Restricting what an agent can do by removing tools from the schema it is shown, rather than by checking permissions when a call is made — so that the model never learns the capability exists and has nothing to argue for or probe around."
---

Schema gating is the practice of constraining an agent by controlling which tools appear in the
schema handed to the model, rather than by intercepting calls to forbidden tools at runtime.
[[ScholarlyArticle/building-effective-ai-coding-agents-for-the-terminal]] states the contrast as the
difference between a guardrail and a missing road: a model that can see a dangerous tool in its
schema can reason about invoking it, argue for why it should be allowed, and probe for edge cases in
the permission logic, whereas a model cannot reason about a capability it does not know exists.

## Usage

The term describes a placement decision, not a new mechanism: the same restriction is expressed
either by omitting the tool from the schema or by rejecting the call, and the claim is that the
first placement is more robust. In [[SoftwareApplication/opendev]] it appears as one of five
independent safety layers, realised as a whitelist of read-only tools in the agent's planning mode,
a per-subagent list of allowed tools, and gating on which externally discovered tools may enter the
context at all. The same report describes the planning and execution roles as separate agents
precisely so that the planning agent's schema can exclude write tools.

## When It Applies

It applies wherever an agent has tools whose use must be prevented rather than merely reviewed, and
where the set to be withheld is known before the turn begins — a planning phase that should not
write, a subagent that should not shell out. It assumes the tool set is assembled per agent and per
mode rather than fixed globally, which is a property of the scaffolding stage rather than something
that can be retrofitted at call time.

It does not replace the other layers, and the report does not present it as doing so: an approval
system is still needed for operations a human should see, and validation inside a tool is still
needed for calls that are legitimate but dangerous in their particulars. It also has nothing to say
about a tool the agent is supposed to have and misuses. The report's argument for keeping the layers
independent is that a bug in one should not weaken another.

As evidence, this is the design rationale of a single system, reported by its author in a technical
report that explicitly presents architectural decisions rather than measured results. The claim that
schema gating is more robust than runtime permission checks is argued from the model's ability to
reason about what it can see, not from a comparative evaluation.

## Related Terms

[[DefinedTerm/guardrails]], [[DefinedTerm/permission-modes]], [[DefinedTerm/sandboxing]],
[[DefinedTerm/agent-scaffold]]
