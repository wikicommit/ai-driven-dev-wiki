---
title: "Encoding Team Standards"
type: "schema:BlogPosting"
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
  description: "A March 2026 article by Rahul Garg on martinfowler.com, part of the series \"Patterns for Reducing Friction in AI-Assisted Development\", proposing that the instructions a team uses to steer AI generation, refactoring, security checks and review be treated as versioned, reviewed, shared infrastructure that encodes the team's tacit knowledge."
  author: ["Rahul Garg"]
  datePublished: "2026-03-31"
  publisher: "martinfowler.com"
---

This article, published on martinfowler.com as part of the series "Patterns for Reducing Friction in
AI-Assisted Development", starts from an observation about AI coding assistants: they respond to
whoever is prompting, so the quality of what they produce depends on how well that person articulates
the team's standards. Two developers on the same team, using the same tool, codebase and project
context, can get materially different results, because the instructions each gives the AI differ —
across generation, refactoring, security checking and review alike.

The author proposes treating those instructions as infrastructure: versioned, reviewed, shared
artifacts kept in the repository that turn the team's tacit knowledge into instructions the AI executes,
so that quality stays consistent regardless of who is at the keyboard. The page for the concept itself
is [[DefinedTerm/executable-team-standards]].

## Key Points

- When AI-assisted development depends on who is prompting, senior engineers become bottlenecks — not
  because they write the code, but because they are the only ones who know what to ask the AI for. The
  author reports having observed this pattern repeatedly.
- The author frames the inconsistency as a systems problem rather than a skills problem: training,
  documentation and pairing help but are slow and do not scale, and the knowledge has no vehicle for
  consistent distribution.
- Earlier techniques in the same series address what the AI *knows* about the project; this one is
  about making the AI apply the team's *judgment* consistently.
- The author describes two moves: from tacit to explicit (writing down what seniors know instinctively,
  in a form an AI can execute) and from documentation to execution (instructions that live in the
  repository and are reviewed through pull requests, like linting rules or CI/CD pipeline definitions).
  When the standard is encoded as an instruction, "the governance is the workflow".
- A well-structured executable instruction, in the author's account, has four elements: a role
  definition, context requirements, categorized standards (a priority structure such as blockers /
  must-address / advisories), and an output format that keeps results comparable across runs and
  developers.
- The principle applies to generation, refactoring, security and review instructions alike; the author
  recommends keeping each instruction small and single-purpose.
- Creating instructions amounts to interviewing senior engineers with pointed questions (which
  decisions must never be left to individual judgment, which corrections are made most often, what
  triggers immediate rejection in review); the answers map directly onto instruction structures. In one
  project the author describes, this surfaced that two seniors had different thresholds for "critical"
  versus "important" security concerns, and a less experienced developer's first review with the
  resulting instructions flagged a missing authorization check.
- Instructions apply at generation time (where they have the most leverage, preventing misalignment),
  during development, at review time (the last opportunity to catch misalignment), and optionally in CI,
  where they must be fast and predictable enough not to become a noisy gate.
- A prompt on an individual machine is a personal productivity hack; the same prompt in the team's
  repository is infrastructure. Different tools implement this differently — custom commands, skills,
  rules files, project instructions — but the shared property is a versioned artifact the AI executes
  consistently. Repository placement and pull request review are the author's answer to the risk of the
  instructions becoming a documentation graveyard.
- By the author's heuristic, the approach pays off when AI-assisted output visibly varies with who is
  prompting, or work routes through the few people who know how to prompt: "Teams of five may not need
  this. Teams of fifteen almost certainly do." The costs he names are the effort of creating
  instructions, brittleness when they are overly prescriptive, maintenance as standards evolve, and
  over-engineering.
- The recommended starting point, from the author's experience, is a single instruction — usually a
  generation or review instruction — with further instructions following adoption rather than preceding
  it.

## Context

The article belongs to a series whose earlier installments, by the same author, cover sharing project
context with the AI, structuring design conversations, and keeping decisions durable across sessions;
it positions itself as addressing a different problem from those. Its claims rest on the author's own
experience and observation rather than on measurement. A sidebar points to Lattice, a project
hosted on GitHub, which packages the practice as composable skill "atoms" with self-validation
checklists that teams customize through a guided interview into a versioned standards document.
