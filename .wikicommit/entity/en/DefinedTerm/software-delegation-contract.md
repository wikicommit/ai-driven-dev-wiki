---
title: "Software delegation contract"
type: "schema:DefinedTerm"
lang: en
tags: [coding-agents, code-review, agentic-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2606.17099'
    hash: sha256:287a1f7f2965de4360676a41fe7236b0036d0a2d603c9d92125d58e53a5d3612
review_status: pending
generated_at: "2026-10-16"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.10.0"

properties:
  description: "A unit of analysis for delegated coding work, covering the task, the authority granted, the returned work package and the acceptance context under which an AI coding agent's work is assigned and reviewed."
---

A software delegation contract is a proposed unit of analysis for coding work that is delegated to
an AI coding agent: it covers the task being assigned, the authority the agent is given to modify
the repository, the work package the agent returns, and the acceptance context in which that work is
reviewed. It frames the agent as accepting an assigned task, modifying a repository under bounded
authority and returning work for review.

## Usage

The term comes from research on AI coding agents. According to
[[ScholarlyArticle/software-delegation-contracts-measuring-reviewability-in-ai-coding-agent-work]],
the concept was proposed in prior work without its effects being measured; that paper uses it to
write explicit contracts for coding agents and compares them against a realistic issue-style prompt,
both with and without a required evidence bundle.

## When It Applies

The concept applies when a coding agent is assigned a bounded task and returns work for someone to
accept or reject. Its evidence so far is one controlled pilot study of 64 agent runs on ten small
TypeScript API tasks, reviewed by model-based reviewers. In that study, making the contract explicit
did not improve correctness — every run passed the hidden acceptance checks — but improved
reviewability: evidence sufficiency rose, reviewer ambiguity fell, and changed-file lists,
known-limitations and residual-risk sections, and reviewer checklists appeared mostly or only when
the contract demanded them. The cost was 13% more agent tokens and 38% more wall-clock time, larger
for the weaker model tier.

## Related Terms

- [[DefinedTerm/ai-coding-agent]]
- [[DefinedTerm/pr-contract]]
