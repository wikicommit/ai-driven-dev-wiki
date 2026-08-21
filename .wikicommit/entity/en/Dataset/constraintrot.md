---
title: "ConstraintRot"
type: "schema:Dataset"
lang: en
tags: [benchmark, evaluation, security, governance, context-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.22528'
    hash: sha256:ef37298f918eb3603bb29e729bf5490c27887bfadf9b5c6794e31dee79647cc2
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A benchmark of nine long-horizon agent scenarios, each pairing an in-context governance constraint with a later request whose natural completion would violate it, designed to measure [[DefinedTerm/governance-decay]] under [[DefinedTerm/compaction]]. Violations are graded deterministically by detecting the prohibited effect in the agent's emitted tool call."
  creator: "Shiyang Chen"
  datePublished: "2026-06-27"
  measurementTechnique: "Deterministic detection of a prohibited effect in the agent's emitted tool call, compared across four conditions: policy present, compacted, absent, and pinned"
---

ConstraintRot is the benchmark introduced in [[ScholarlyArticle/governance-decay]] to measure whether an agent still obeys an in-context rule after its harness has compacted the conversation that contained the rule. Its design goal is to isolate compaction from generic long-context effects, which it does by running the same trigger under four conditions: with the policy present, compacted, absent, and pinned.

## Composition

Each scenario is a single agent session with three parts: a policy turn that establishes an in-context governance constraint; a long sequence of benign task turns that grow the context past the compaction budget; and a trigger request whose natural completion violates the policy. Triggers are deliberately self-contained — all data needed to act is provided inline and the agent is instructed to emit a single terminal tool call — "so that a refusal is driven by the policy, not by missing capability."

The nine tasks split into two kinds, and the split is what makes the benchmark's central finding visible. Five are **soft** organization-specific policies: an external-email restriction, a spend-approval limit, report-channel routing, a region standard, and an English-only language policy. Four are **hard** safety norms the model often refuses intrinsically: destructive production operations, secret and SSH-key exfiltration, PII disclosure, and disabling security controls. Because a soft task asks for a normal, helpful action forbidden only by an arbitrary organizational rule, a refusal there isolates the policy's effect from the model's own caution.

The agent acts by emitting a tool call — the paper names `send_email`, `db_exec`, `read_file`, `disclose`, and `purchase` — and a violation is graded deterministically by detecting the prohibited effect in the emitted action rather than by judging the agent's prose.

## Use in Evaluation

The benchmark's published run covers seven model families and four compaction strategies, pooling 1,323 episodes. Its headline result is that compaction raises the violation rate from 0% to 30%, and up to 59% in the worst configuration; conditioning on whether the constraint survived into the summary separates the mechanism, giving 0% when it survives and 38% when it is dropped.

The soft/hard split delivers the paper's most-cited number: decay is 8.3× larger for soft organizational policies than for hard safety norms. The per-task table shows this concretely — the hard tasks covering PII disclosure and disabling audit logging show +0 percentage points of decay, while dropping `DROP` on a production database and reading an SSH key show +14 and +10 respectively, all far below the soft-policy figures.

The benchmark is also used to evaluate the paper's own attack and mitigation, which is its main limitation as an independent measure: the same instrument defines the phenomenon, demonstrates that an optimized injection can induce it deliberately, and certifies that Constraint Pinning removes it. Its scenarios are constructed rather than drawn from deployed systems, and what it measures is tool-call emission rather than realized harm.
