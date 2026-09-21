---
title: "Attribution Gap"
type: "schema:DefinedTerm"
lang: en
tags: [agents, requirements-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2601.04556'
    hash: sha256:47686611cd9c576575a542851a7df72a328d486ff7ae3ce584ed719df20ad9f9
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The gap between the outcome question a decision-maker asks and the causal explanation they actually want. An agent that answers the literal question with correct figures, and stops there, has left the gap open — the named failure that motivates specifying at design time what an agent should reason about."
---

The attribution gap is the distance between what a decision-maker asks and what they are after: they ask about an outcome, but what they want is attribution — a causal chain connecting that outcome to something they can act on. The term is introduced in [[ScholarlyArticle/4d-are-bridging-the-attribution-gap]], whose formulation is that when a manager asks "why is completion rate 80%?", they are not requesting a data lookup; they want to know which process failed, what resource was missing, what strategic factor is in play.

## Usage

The paper's illustrating case is an agent that answered the literal question correctly and delivered nothing. Its abstract states this as an agent the authors deployed; the section that tells the story introduces it as a deployment scenario to consider. Asked why a region's deposit completion rate was 80%, it reported the rate, the visit frequency and the product-penetration figure, and closed with the advice that the team should improve these metrics. The retrieval was accurate and the reasoning steps were valid; the manager still had only numbers. Contrast an answer that traces "completion rate is 80% ← low product penetration in the high-value segment ← insufficient visit coverage ← competitive pressure from three new market entrants", which gives her something to act on.

What makes it a useful diagnosis rather than a complaint is where it locates the fault. The gap is not a failure of the agent's reasoning machinery: in that example the reasoning-action loop executed exactly as designed. It is an absence upstream, in what the agent was told to reason about. On this account runtime reasoning frameworks assume a well-specified agent, and the assumption is rarely met in practice.

## When It Applies

It is framed as a problem for attribution-driven decision-support agents in particular — those that answer "why" questions, trace causal chains, and ground recommendations in causal explanation, such as business analytics assistants, diagnostic aids and advisory systems. Its proposers explicitly place three kinds of agent outside that scope: recommendation agents, where users accept suggestions without requiring an explanation; predictive agents, where the goal is forecasting rather than attribution; and autonomous agents, which act without a human decision-maker in the loop. They add elsewhere that coding, creative, recommendation and autonomous agents likely need specification approaches of their own.

Its proposers name the organizational consequence of leaving the gap open the "promptware crisis": agent development degenerating into trial-and-error prompt engineering, implicit knowledge that lives in developers' heads, and agents that fail in predictable ways — incomplete explanations, boundary violations, missed causal connections. Their proposed remedy is [[DefinedTerm/4d-are]], a design-time methodology for specifying attribution logic explicitly.

The term comes from a single preprint that introduces it to motivate its own methodology, and is illustrated by one deployment; it is not at this point an established or independently corroborated framing.

## Related Terms

[[DefinedTerm/4d-are]], [[DefinedTerm/prompt-debt]], [[DefinedTerm/prompt-engineering]], [[DefinedTerm/context-engineering]]
