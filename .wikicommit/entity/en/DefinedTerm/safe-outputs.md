---
title: "Safe Outputs"
type: "schema:DefinedTerm"
lang: en
tags: [agent-safety, ci-cd, agentic-engineering]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/generative-ai/continuous-ai-in-practice-what-developers-can-automate-today-with-agentic-ci/'
    hash: sha256:994d27bdd399c24187602b4764046df3b5e7b67fb9de1d565cff3b8821304ac3
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "GitHub's name for a deterministic contract governing what an agentic workflow is permitted to produce. Agents are read-only by default, a workflow declares exactly which artifacts its agent may create and under what constraints, and anything outside those boundaries is forbidden."
---

Safe Outputs is GitHub's name for the permission model underpinning
[[DefinedTerm/continuous-ai]]: a deterministic contract for what an agent is allowed to do. As
described in [[BlogPosting/continuous-ai-in-practice]], agents operate by default with read-only
access to repositories and cannot create issues, open pull requests or modify content unless
explicitly permitted. When defining a workflow, developers specify exactly which artifacts the agent
may produce — opening a pull request, filing an issue — and under what constraints, with anything
outside those boundaries forbidden.

What the name emphasizes is the direction of the control. The constraint is placed on the agent's
*outputs* rather than on its reasoning or its inputs, which is what makes the contract deterministic
even though the process producing those outputs is not.

## Usage

The model is described as assuming agents can fail or behave unexpectedly, and its properties follow
from that premise rather than from confidence in the agent: outputs are sanitized, permissions are
explicit, all activity is logged and auditable, and the resulting blast radius is described as
deterministic. The source characterizes the arrangement as AI operating within guardrails developers
explicitly define, and distinguishes it from AI taking over software development.

In the same design, agentic workflows do not make autonomous commits. They create the same kinds of
artifacts a developer would, with pull requests reported as the most common output because they
align with how developers already review changes. The stated consequences are that agents do not
merge code, developers retain full control, and everything is visible and reviewable.

## When It Applies

The model applies wherever an agent runs unattended against a shared repository, and it assumes the
useful results of that work can be expressed as a declarable set of artifacts. Its protection is
bounded by that declaration: a capability someone grants is granted, so the contract constrains an
agent's reach without judging whether any particular permitted artifact is a good one — which is
what the human review step is for.

How well-established it is: the account available here is a single vendor's description of the
safety model in its own research prototype, presented as a design principle rather than as a
measured result.

## Related Terms

- [[DefinedTerm/continuous-ai]] — the pattern this permission model underpins
- [[DefinedTerm/guardrails]] — the broader family of controls placed around an agent
- [[DefinedTerm/human-in-the-loop]] — the review step the model preserves by producing artifacts
- [[DefinedTerm/deny-first-permission-evaluation]] — a comparable default-deny posture at tool level
- [[BlogPosting/continuous-ai-in-practice]] — the source of this account
