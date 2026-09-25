---
title: "Safe Outputs"
type: "schema:DefinedTerm"
lang: en
tags: [agent-safety, ci-cd, agentic-engineering]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/generative-ai/continuous-ai-in-practice-what-developers-can-automate-today-with-agentic-ci/'
    hash: sha256:994d27bdd399c24187602b4764046df3b5e7b67fb9de1d565cff3b8821304ac3
  - type: url
    url: 'https://docs.github.com/en/copilot/how-tos/github-agentic-workflows/creating-github-agentic-workflows'
    hash: sha256:a8e56bd50a0890f7f307b8d7987d63165acf3552883dc367b139df6ca784eb6f
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

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

## Usage

The model is described as assuming agents can fail or behave unexpectedly. Its stated properties
are that outputs are sanitized, permissions are explicit, all activity is logged and auditable, and the resulting blast radius is described as
deterministic. The source characterizes the arrangement as AI operating within guardrails developers
explicitly define, and distinguishes it from AI taking over software development.

In the same design, agentic workflows do not make autonomous commits. They create the same kinds of
artifacts a developer would, with pull requests reported as the most common output because they
align with how developers already review changes. The stated consequences are that agents do not
merge code, developers retain full control, and everything is visible and reviewable.

In [[SoftwareApplication/github-agentic-workflows]] the contract is a field of the workflow file
itself. GitHub's documentation lists `safe-outputs` among the key frontmatter fields, defining it
as the write operations the agent is allowed to perform — for example `create-issue`,
`add-comment` or `create-pull-request` — alongside `permissions`, the repository permissions
granted to the agent, which default to `read-all`. Its example weekly issue-activity report
declares only `create-issue`, so the report is delivered as a new issue.

## When It Applies

It applies when a developer defines an agentic workflow: the developer declares which artifacts
the agent may produce and under what constraints, anything outside those boundaries is forbidden,
and the artifacts that result are reviewed by developers, whose judgment the source describes as
remaining the final authority.

How well-established it is: both accounts available here come from a single vendor, GitHub — a
design principle described in a GitHub Next blog post, and a configuration field documented for
GitHub Agentic Workflows, a product in public preview. Neither presents a measured result.

## Related Terms

- [[DefinedTerm/continuous-ai]] — the pattern this permission model underpins
- [[DefinedTerm/guardrails]] — the broader family of controls placed around an agent
- [[DefinedTerm/human-in-the-loop]] — the review step the model preserves by producing artifacts
- [[DefinedTerm/deny-first-permission-evaluation]] — default-deny permission evaluation for agent tools
- [[BlogPosting/continuous-ai-in-practice]] — the blog source of this account
