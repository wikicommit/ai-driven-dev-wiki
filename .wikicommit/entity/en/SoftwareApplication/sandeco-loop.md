---
title: "sandeco-loop"
type: "schema:SoftwareApplication"
lang: en
tags: [loop-engineering, agent-skills]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.00038'
    hash: sha256:2f17c51102988847128a0fb57824555d6ac3a32183f9ed61e269f1a63d48d4c0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An open skill that writes hardened loop specifications: it triages whether a task needs a loop at all, interviews the author about the loop's design elements, applies a hardening pass against known anti-patterns, and emits a single specification document with a way to actuate it."
  applicationCategory: "Agent skill"
---

sandeco-loop is an open skill released as a deliverable accompanying
[[ScholarlyArticle/stop-hand-holding-your-coding-agent]]. It turns that paper's principles and
anti-patterns into a repeatable procedure for authoring a [[DefinedTerm/loop-specification]]. The
paper stresses that the skill does not run a loop; it writes the specification of one — a single
document capturing the trigger, goal, check, stopping rule and memory, which a human can read,
version and hand to an agent harness.

## Capabilities

The skill works in stages. It first triages the task by asking whether the outcome of each turn
changes the next action; if not, it says so and returns a simple scheduled prompt instead of a loop.
For a task that survives triage, it conducts a short interview, one question at a time, covering the
goal and whether success is verifiable, the concrete check, the trigger, the named stop states beyond
success, the named skills and any nested sub-loops, where state lives between turns, and guardrails
such as iteration and budget ceilings and points needing human approval.

A hardening pass then maps onto the paper's anti-patterns: it insists on an external check rather
than a self-score, keeps the maker distinct from the checker, requires terminal states in which an
error or exhausted budget never counts as success, enforces one change per turn with the worst item
first, caps nested sub-loops with a multiplicative ceiling and forbids a sub-loop from invoking its
caller, puts state on disk, and records cost per accepted change as a health metric.

The output is a single `<name>-loop.md` document with a fixed skeleton — description and "use when",
goal and verification, the steps of one turn, named stop states, guardrails, memory location,
sub-loops, a short "why it works" section, and an actuation clause. Actuation is either a `/goal`
command, when the work fits inside a single context window, or a fresh-context
[[DefinedTerm/ralph-loop]] skeleton when it is long enough that a single context would degrade; the
skill can optionally also emit a `/loop-<name>` command. The paper's worked example is a
test-coverage loop whose terminal states are success at full coverage, no-progress after two barren
rounds, and exhaustion after a turn ceiling.

## Adoption & Ecosystem

The paper offers the skill as a bridge from principles to a writable artifact, not as an evaluated
contribution, and reports no usage data for it; whether specifications written this way improve
outcomes is left as an open empirical question. It is published in the author's prompts repository
on GitHub.
