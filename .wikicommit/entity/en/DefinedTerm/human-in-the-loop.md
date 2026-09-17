---
title: "Human-in-the-loop"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/coding-agents-manager/'
    hash: sha256:fc697c3fcc830075a1a6b6751a1f242d4b6ff4ea9a385c1ec60a0c6f8a6e50a1
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A design in which a human is deliberately kept part of an otherwise-automated agent workflow — used by Addy Osmani both for a developer actively pairing with an agent in real time, and, in a later post, for an asynchronous approval gate that pauses a long-running agent mid-task until a human responds."
---

Human-in-the-loop describes a design in which a human is deliberately kept part of an otherwise-automated agent workflow, rather than letting the agent run entirely unsupervised. The term is used for two distinct patterns across the sources: a developer pairing with an agent in real time, and an asynchronous approval gate inside a longer autonomous run.

## Usage

In the real-time sense, Osmani places human-in-the-loop sessions on one side of a two-mode mental model for working with coding agents: local, high-touch sessions where a developer stays engaged, course-correcting as the agent works and making calls that require context the agent lacks — architecture decisions, tricky refactors, product nuance, ambiguous requirements — as opposed to cloud or background sessions that run asynchronously on bounded, well-specified tasks such as straightforward features, migrations with clear patterns, test generation, documentation updates, dependency bumps, and targeted refactors.

A later post on long-running agents uses the same term for a different pattern: delegated approval inside an agent that otherwise runs unsupervised for hours or days. It contrasts this with what it calls the common but weak implementation of "human-in-the-loop" — serialize state to JSON, fire a webhook, and hope someone responds, after which the state goes stale, the notification gets buried, and the agent re-deserializes into a slightly different world. Long-running runtimes are described as instead letting the agent pause in place with its full execution state intact (reasoning chain, working memory, tool history, pending action), consuming zero compute while hours of human time pass, and resuming with sub-second latency once a decision is made. Google's Mission Control is named as one vendor's implementation of this pattern, with the post stating the underlying pattern works regardless of vendor.

## When It Applies

The real-time sense applies to work where taste and judgment dominate and the agent lacks context a person must supply as it goes — architecture decisions, tricky refactors, ambiguous requirements, nuanced product calls — and assumes a developer is available to actively pair with the agent rather than fire off a task and return to it later.

The delegated-approval sense applies to a long-running, otherwise-autonomous agent that reaches a decision point requiring a human sign-off, and assumes a runtime that can serialize and later restore full execution state rather than only a coarse task description. Its failure mode without that runtime is state going stale or a webhook notification getting buried before a human ever acts on it.

## Related Terms

[[DefinedTerm/sandboxing]], [[DefinedTerm/checkpoint-and-resume]], [[DefinedTerm/long-running-agent]]
