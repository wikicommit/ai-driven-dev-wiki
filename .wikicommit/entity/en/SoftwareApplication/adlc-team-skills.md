---
title: "adlc-team-skills"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-skills, agentic-engineering, spec-driven-development, sdlc, evals]
sources:
  - type: url
    url: 'https://github.com/tikalk/adlc-team-skills'
    hash: sha256:cd465f376e830cc0d6e662bd36e98e3a04d558a78ce98fb40457fc5d8b387e19
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An MIT-licensed collection of agent skills from the tikalk GitHub organization that loads a team's shared rules into a coding agent at session start as a lightweight index, runs spec-gated missions, captures session learnings back into a versioned team repository, and adds a 'software factory' outer loop from work intake to reviewed pull requests."
  applicationCategory: "Coding agent skills collection"
  featureList: "Session-start index of team directives with rules loaded on demand; mission-brief spec contract with a specify, plan, implement and converge loop; Context Directive Records extracted from sessions and scored by confidence; eval skills that build binary graders validated with holdout splits; product, architecture and change decision-record lifecycles; software-factory skills for intake, mission execution, PR review and learning; build-to-delete rule pruning"
---

adlc-team-skills is a collection of [[DefinedTerm/agent-skills]] that aims to give coding agents a team's
context at the start of every session, "so they stop working like strangers". It is published under the
MIT License in the tikalk GitHub organization, states that it implements the
[[DefinedTerm/twelve-factor-agentic-sdlc]], and works with agents that support the Agent Skills standard,
naming [[SoftwareApplication/claude-code]], Codex, [[SoftwareApplication/opencode]], Cursor and Copilot.

Its central idea is that a team's rules live in a separate, version-controlled "team-ai-directives"
repository, reviewed through pull requests and shared by the whole team, instead of in personal
`CLAUDE.md` files that live on one machine and drift. At session start a `team-boot` skill, fired by a
session-start event hook, injects only a lean index of those rules — roughly a hundred tokens of names
and one-line descriptions — and the agent pulls a rule's full text only when the current task matches
it. The README justifies this "index, not injection" design by citing research that long contexts
degrade model performance even with perfect retrieval; the team repository's per-type index files are
likewise described as [[DefinedTerm/progressive-disclosure]].

## Capabilities

The README describes a basic session workflow of four parts. `team-boot` injects the directives index.
`mission-brief` stops the agent jumping to code by first forcing a contract — goal, constraints,
non-goals and success criteria — and then walks a specify → plan → implement ↔ converge loop with gates,
a circuit breaker, resume and an audit trail. At session end, `team-learn` extracts hard-won fixes as
Context Directive Records (CDRs), scores them by confidence, batch-reviews them and publishes accepted
ones as a draft pull request to the team repository, keeping drafts and usage data on an orphan
branch so that later sessions rank CDRs by real usage. `team-repair --build-to-delete` re-runs evals
without a rule and proposes deleting the rule if the model passes anyway.

Further skill families cover evaluations (building executable graders — binary checks wherever code can
verify, LLM judges only for what static checks cannot — validated with holdout splits and true-positive and true-negative
rates); product and architecture decision records that generate `PRD.md` and `AD.md`;
change decision records mined from issue-linked commits in git history; and a tech-selection skill that
injects the Tikal Tech Radar's view before a choice is recorded as an architecture decision record.
`mission-brief` can also hand steps to skills from other collections installed alongside it, choosing
among them by reading their `SKILL.md` frontmatter; the README names [[SoftwareApplication/superpowers]]
among the collections it works alongside.

Around this session loop sits what the README calls the **software factory**, the outer loop of an
agentic SDLC: `factory-init` bootstraps an existing repository, `factory-queue` triages incoming work
behind a human-approved intent gate, `factory-mission` executes it as spec-gated missions in isolated
worktrees with a test-first split between a test agent and an implementation agent, `factory-review`
grades the resulting pull requests against policy written as code, and `factory-learn` feeds what the
runs taught back into the team repository. The README states that every automated stage is advisory,
humans hold the gates, and nothing auto-merges.

## Adoption & Ecosystem

The skills are installed through the project's own `adlc-cli`, which wraps the generic skills installer
and additionally generates slash commands and wires the session-start hooks for nine coding agents, or
as plain skills without those hooks. A companion document covers installing it alongside
[[SoftwareApplication/agentic-sdlc-spec-kit]] from the same organization. The project's stated philosophy
is that rules should shrink over time rather than grow, that anything code can check should get a binary
grader, and that every decision class should live in version-controlled repositories and trace from
record to document to code.

The README also records a security incident: on 2026-07-27 a supply-chain worm used a stolen maintainer
token to inject a malicious payload into the repository's `.claude/` and `.vscode/` directories for
several hours. It says the payload ran only for someone who cloned the repository and opened it in VS
Code or started a Claude Code session inside it, that the skills install path never shipped those
files, and that history was rewritten, secrets rotated and branch protection tightened. Its stated
lesson for any repository is to treat `.vscode/tasks.json` and `.claude/settings.json` in a clone as
executable code.
