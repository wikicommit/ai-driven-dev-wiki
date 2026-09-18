---
title: "Deny-First Permission Evaluation"
type: "schema:DefinedTerm"
lang: en
tags: [agents, agent-safety, human-oversight]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.14228'
    hash: sha256:c6ebed0a2e24b61491efe18f003cf6d6c018a671a732b3d6e331a5fe195a0e9d
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A permission model in which deny rules always take precedence over allow rules regardless of specificity, and an action matching no rule is escalated to a human rather than allowed silently."
---

Deny-first permission evaluation is a safety posture for tool-using agents in which deny rules always win over allow rules — even when the allow rule is the more specific of the two — and any action matching no explicit rule is escalated to a human rather than permitted by default. A broad denial such as "deny all shell commands" therefore cannot be overridden by a narrow permission such as "allow npm test". [[ScholarlyArticle/dive-into-claude-code]] identifies it as the default safety posture of [[SoftwareApplication/claude-code]] and pairs it with a second principle, defense in depth, under which multiple independent mechanisms apply in parallel so that any one of them can block an action.

## Usage

In the system analysed by that paper the approach is realised as seven independent layers, a request having to pass every applicable one: blanket-denied tools are stripped from the model's view before it can attempt them; deny rules are evaluated ahead of allow rules; the active permission mode determines baseline handling for anything matching no explicit rule; an ML classifier may deny requests the rule system would allow; approved shell commands may still run inside a sandbox restricting filesystem and network access; session-scoped permissions are not restored on resume or fork; and hooks can intervene to modify or resolve a decision. Rules match at both tool level and content level, so a pattern can target a specific command prefix rather than a whole tool.

A denial is treated as a routing signal rather than a hard stop: the model receives the reason, revises its approach, and attempts a safer alternative on the next iteration, so enforcement shapes the agent's behaviour instead of simply halting it. The analysing paper presents the approach as the expression of a threat model in which the model is untrusted while the developer's machine is trusted. It is also motivated by evidence about people — see [[DefinedTerm/approval-fatigue]] — since a system that must remain safe when its supervisor is approving prompts habitually cannot rest on that supervisor's attention.

## When It Applies

The approach assumes a harness in which reasoning and enforcement occupy separate code paths, so that a compromised or adversarially manipulated model cannot override the checks; in the analysed system the model's only interface to the outside world is a structured tool-use protocol the harness validates before execution. It is one of several positions available: the same paper contrasts it with container-based isolation, which sandboxes the agent's whole execution environment rather than evaluating individual invocations, and with version-control-based rollback, which makes changes reversible instead of gating them. The trade is fine-grained control over individual actions at the cost of simplicity.

Its central weakness is named by the authors themselves. Defense in depth rests on an assumption that the layers fail independently, and layers that share performance or economic constraints can degrade together: they cite security research finding that commands with more than 50 subcommands fell back to a single generic approval prompt instead of per-subcommand deny-rule checks, because the per-subcommand parsing caused interface freezes. They also report a temporal gap the layered picture does not capture — code executing during project initialization, before the interactive trust dialog appears, falls outside the evaluation pipeline entirely. The authors argue the relevant question is therefore not whether any single layer can be bypassed, but how many independent layers must fail at once and whether they share failure modes. The account here rests on one source-level study of a single system at one version, not on a measured comparison across agents.

## Related Terms

[[DefinedTerm/approval-fatigue]], [[DefinedTerm/guardrails]], [[DefinedTerm/sandboxing]], [[DefinedTerm/human-in-the-loop]], [[SoftwareApplication/claude-code]]
