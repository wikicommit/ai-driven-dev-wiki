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
  - type: url
    url: 'https://arxiv.org/pdf/2604.16520'
    hash: sha256:2601c1408563f747b2ac732af43342b6d4d14231aace9b4a2e0aa4d33ba3f674
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A design in which a human is deliberately kept part of an otherwise-automated agent workflow — used by Addy Osmani both for a developer actively pairing with an agent in real time, and, in a later post, for an asynchronous approval gate that pauses a long-running agent mid-task until a human responds; a third line of work argues that how proposals are surfaced for review determines how effective that involvement actually is."
---

Human-in-the-loop describes a design in which a human is deliberately kept part of an otherwise-automated agent workflow, rather than letting the agent run entirely unsupervised. The term is used for three distinct patterns across the sources: a developer pairing with an agent in real time, an asynchronous approval gate inside a longer autonomous run, and a structured review surface through which a person inspects and edits what the agent proposes.

## Usage

In the real-time sense, Osmani places human-in-the-loop sessions on one side of a two-mode mental model for working with coding agents: local, high-touch sessions where a developer stays engaged, course-correcting as the agent works and making calls that require context the agent lacks — architecture decisions, tricky refactors, product nuance, ambiguous requirements — as opposed to cloud or background sessions that run asynchronously on bounded, well-specified tasks such as straightforward features, migrations with clear patterns, test generation, documentation updates, dependency bumps, and targeted refactors.

A later post on long-running agents uses the same term for a different pattern: delegated approval inside an agent that otherwise runs unsupervised for hours or days. It contrasts this with what it calls the common but weak implementation of "human-in-the-loop" — serialize state to JSON, fire a webhook, and hope someone responds, after which the state goes stale, the notification gets buried, and the agent re-deserializes into a slightly different world. Long-running runtimes are described as instead letting the agent pause in place with its full execution state intact (reasoning chain, working memory, tool history, pending action), consuming zero compute while hours of human time pass, and resuming with sub-second latency once a decision is made. Google's Mission Control is named as one vendor's implementation of this pattern, with the post stating the underlying pattern works regardless of vendor.

[[ScholarlyArticle/agentclick]] adds a third emphasis: that whether a human is nominally in the loop matters less than what the interface lets them actually do. Its authors argue that terminal output interleaves reasoning traces, tool logs and proposed actions in a single stream, so it is hard to identify what requires review; that feedback is cumbersome because users must type free-form corrections even for small local edits; and that consequential actions are presented as opaque events or binary prompts, leaving little room for targeted inspection or modification. Their response, [[SoftwareApplication/agentclick]], is a review layer whose stated aim is to improve collaboration rather than merely gate execution: the user can approve, edit directly, delete content, adjust constraints or request a targeted rewrite at the level of the artifact under review, which those authors argue matters most when an agent's output is largely correct but needs a localized change. They also describe review as a channel for preference capture, with reason-tagged edits written to a memory file the agent reads in later runs, so a correction shapes future behaviour rather than serving as a one-off override.

## When It Applies

The real-time sense applies to work where taste and judgment dominate and the agent lacks context a person must supply as it goes — architecture decisions, tricky refactors, ambiguous requirements, nuanced product calls — and assumes a developer is available to actively pair with the agent rather than fire off a task and return to it later.

The delegated-approval sense applies to a long-running, otherwise-autonomous agent that reaches a decision point requiring a human sign-off, and assumes a runtime that can hold the agent paused in place with its full execution state intact — reasoning chain, working memory, tool history, pending action — rather than one that serializes state out, fires a notification and hopes for a reply. Its failure mode without that runtime is state going stale or a webhook notification getting buried before a human ever acts on it.

The artifact-review sense assumes an agent that can be made to submit proposals and wait for an outcome before acting, and a surface other than the terminal on which to render them. The AgentClick authors argue the barriers they identify fall hardest on non-expert users, and become sharper when agents run on remote or headless infrastructure where the terminal is not merely a poor collaboration medium but often an inaccessible one. That work is a demo paper whose three walkthroughs its own authors present as capability illustrations rather than a controlled user study, so the claimed benefits are demonstrated rather than measured.

## Related Terms

[[DefinedTerm/sandboxing]], [[DefinedTerm/checkpoint-and-resume]], [[DefinedTerm/long-running-agent]], [[DefinedTerm/approval-fatigue]]
