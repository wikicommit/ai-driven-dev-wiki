---
title: "Approval Fatigue"
type: "schema:DefinedTerm"
lang: en
tags: [agents, human-oversight, agent-safety]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.14228'
    hash: sha256:c6ebed0a2e24b61491efe18f003cf6d6c018a671a732b3d6e331a5fe195a0e9d
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The pattern in which users habitually approve an agent's permission prompts without careful review, making interactive confirmation behaviorally unreliable as a sole safety mechanism."
---

Approval fatigue is the pattern in which the people supervising an AI agent come to approve its permission prompts habitually rather than deliberately, so that interactive confirmation stops functioning as the safety check it was designed to be. [[ScholarlyArticle/dive-into-claude-code]] treats it as a documented behavioral pattern rather than a hypothesis, relaying Anthropic's own analysis that users approve approximately 93% of permission prompts in [[SoftwareApplication/claude-code]] and reading that figure as indicating that approval fatigue renders interactive confirmation behaviorally unreliable as a sole safety mechanism.

## Usage

The term is used to argue for a particular architectural conclusion: that a system must maintain safety independently of human vigilance, because users approve without careful review. In the analysis of Claude Code it is given as the motivation for deny-first evaluation, blanket-deny pre-filtering and [[DefinedTerm/sandboxing]] as layers that operate regardless of user attentiveness, and for the choice to restructure the problem rather than add more warnings — defining boundaries within which the agent can work freely instead of asking for per-action approvals that users stop reviewing once habituated.

The same source relays two further measurements from other publications it cites. Longitudinal usage data shows auto-approve rates rising from roughly 20% at fewer than 50 sessions to over 40% by 750 sessions, alongside substantial increases in session duration; the paper quotes that study's description of the result as autonomy that is “co-constructed by the model, the user, and the product”, and adds its own reading that the gradient is navigated not by deliberate mode selection but by gradual habituation. Separately it reports that sandboxing reduced the frequency of permission prompts by an estimated 84%, which it characterizes as reframing the problem as a human-factors concern: the architectural response to unreliable human approval is to reduce the number of decisions humans must make.

## Related Terms

[[DefinedTerm/deny-first-permission-evaluation]], [[DefinedTerm/human-in-the-loop]], [[DefinedTerm/sandboxing]], [[DefinedTerm/guardrails]], [[ScholarlyArticle/dive-into-claude-code]]
