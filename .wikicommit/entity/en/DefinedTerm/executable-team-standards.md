---
title: "Executable team standards"
type: "schema:DefinedTerm"
lang: en
tags: [ai-assisted-programming, code-review, team-practices]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/reduce-friction-ai/encoding-team-standards.html'
    hash: sha256:fb880997f4c019405eb8c8eae89a22e3f74a4872b6df9553261f865be00c6e46
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A practice, proposed by Rahul Garg, of encoding a team's standards for AI-assisted generation, refactoring, security checking and review as versioned, repository-held instructions the AI executes, so the team's judgment is applied consistently regardless of who is prompting."
---

Executable team standards are the instructions that govern a team's interactions with an AI coding
assistant — for generating code, refactoring it, checking it for security problems and reviewing it —
written down as versioned, reviewed, shared artifacts in the team's repository rather than left to each
developer's own prompting. As proposed by Rahul Garg in
[[BlogPosting/encoding-team-standards]], they turn the tacit knowledge of a team's senior engineers
(what to generate, what to check, what to flag, what to reject) into instructions that execute, so the
standards are applied as a side effect of the workflow instead of as a separate step someone has to
remember.

## Usage

The term comes from the article's conclusion, which contrasts linting — catching syntax and style — with
"executable team standards" that can encode architectural judgment, security awareness, refactoring
philosophy and review rigor. The author compares the practice to linting rules, CI/CD pipeline
definitions and infrastructure-as-code: configuration that executes, not documentation that informs.

In his account, each such instruction has four parts — a role definition that sets the expertise level
and perspective, the context it requires before it can operate, standards grouped by priority (for a
security instruction: blockers, concerns to address before merge, and advisories), and an output format
that keeps results comparable across runs and developers. Instructions are kept small and
single-purpose, and are created by interviewing senior engineers about the decisions, corrections and
rejections they make instinctively. The author notes that tools implement the shared artifact
differently — custom commands, [[DefinedTerm/agent-skills]], rules files or project instructions such as
[[DefinedTerm/agents-md]] — while the property that matters is the same.

## When It Applies

- **Conditions**: the author presents it as most valuable once a team is too large to keep AI-assisted
  work consistent through conversation alone — when output visibly varies with who is prompting, or
  generation and review route through the few people who know how to prompt. By his heuristic, teams of
  five may not need it and teams of fifteen almost certainly do.
- **Assumptions**: the instructions live in the repository and change through the same pull request
  review as code, so drift from actual practice becomes visible in the normal course of work.
- **Failure modes**: overly prescriptive instructions become brittle, producing false positives on edge
  cases or fighting legitimate variation; instructions need maintenance as standards evolve; not every
  interaction with AI needs one; and the collection can decay into a documentation graveyard. Applied in
  CI, instructions must be fast and predictable enough not to become a noisy gate.
- **Establishment**: a single practitioner's proposal, grounded in the author's own observation and
  project experience rather than measurement. He recommends starting with one instruction, usually for
  generation or review, and adding more only as adoption follows.

## Related Terms

- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/agents-md]]
- [[DefinedTerm/agent-skills]]
- [[DefinedTerm/guardrails]]
