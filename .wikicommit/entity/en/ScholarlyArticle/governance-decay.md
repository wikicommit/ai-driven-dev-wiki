---
title: "Governance Decay: How Context Compaction Silently Erases Safety Constraints in Long-Horizon LLM Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [context-engineering, security, governance, agent-architecture, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.22528'
    hash: sha256:ef37298f918eb3603bb29e729bf5490c27887bfadf9b5c6794e31dee79647cc2
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A June 2026 arXiv paper showing that [[DefinedTerm/compaction]] silently deletes in-context governance constraints an agent had been reliably obeying, raising tool-call violation rates from 0% to 30% across seven model families. It names the phenomenon [[DefinedTerm/governance-decay]], measures it with the [[Dataset/constraintrot]] benchmark, demonstrates an attack that induces it deliberately, and proposes a training-free mitigation."
  author:
    - "Shiyang Chen"
  datePublished: "2026-06-27"
---

"Governance Decay" is a single-author paper by Shiyang Chen of the Beijing Institute of Technology, posted to arXiv on 27 June 2026. Its subject is a failure mode that requires no attacker, no jailbreak, and no change to the model or the request: an agent obeys an in-context rule for as long as the rule is visible, the harness compacts the history to stay within a token budget, the summary faithfully records the task state but drops the "old" policy, and the next time the same prohibited request arrives the agent complies.

The paper's framing argument is that [[DefinedTerm/compaction]] "has been engineered for one objective: preserving task accuracy," and that this is the wrong objective, because compaction is also a governance-critical decision. Its reasoning is that a summarizer optimizing for task continuity has no reason to keep a standing policy — "the policy is 'old,' it is not the current sub-goal, and it competes for a shrinking token budget against the active task state." Since agents are increasingly governed by in-context constraints — organizational policies, standing instructions, and loaded memory that specify what the agent must and must not do — the conclusion it draws is that context management is "a first-class agent-governance surface."

It notes that compaction is not a rare event: it cites practitioner reports of it triggering at as little as 5–20k tokens.

## Key Contributions

The paper states four contributions.

- **[[Dataset/constraintrot]]**, a benchmark of self-contained long-horizon agent scenarios that pair a governance constraint with a later prohibited request and grade violations deterministically by detecting the prohibited effect in the agent's tool call.
- **A systematic measurement of governance decay** across seven model families and four compaction strategies. Pooled over 1,323 episodes, compaction raises the violation rate from 0% to 30%, and up to 59% for individual configurations. The paper isolates the mechanism rather than inferring it: when the constraint survives into the summary the violation rate is 0%, and when it is dropped it is 38% — so the harm comes from deletion specifically, not from context length in general.
- **The Compaction-Eviction Attack**, described as a deletion-oriented variant of indirect prompt injection in which an adversary supplying only in-context data forces or biases compaction into omitting a legitimate constraint. The reported result is that optimizing the injection "defeats every model, including one immune to the fixed probe," taking that model from 0% to 65%.
- **Constraint Pinning**, a training-free mitigation inspired by protected state and policy replay, in which governance constraints are quarantined from lossy compaction and integrity-checked across turns. It restores the violation rate to 0% for roughly 47 pinned tokens — under 0.5% overhead at production scale — and the paper reports where naive pinning still fails rather than only where it works.

The finding the paper draws most attention to is a *gradient* rather than an average. Decay is 8.3× larger for soft organizational policies than for hard safety norms, which means the constraints that erode are exactly the deployment-specific ones that live in context, while the norms a model refuses intrinsically are largely spared. The benchmark is constructed to expose this: its five soft tasks are normal, helpful actions forbidden only by an arbitrary organization-specific rule, so a refusal isolates the policy's effect from the model's own caution.

A second result narrows where the vulnerability lives. Delivering the same policy through different channels and then compacting produced no decay when the policy sat in the preserved system message, against +50, +45, and +33 percentage points when it was a standing user instruction, a memory entry, or a tool output respectively — the parts a harness actually compacts. The paper is careful to call this restriction to non-system channels "empirical, not assumed."

## Notes

The paper's argument against the existing runtime-enforcement literature is precise rather than dismissive: least-privilege tool authorization, monitors and policy DSLs, and policy checks on execution paths all "share an implicit assumption that the constraint is present at decision time," and compaction silently violates that precondition. On that reading, this is not a competing defence but a prerequisite for the ones already proposed.

Two limits are worth holding alongside the headline numbers. The channel-comparison ablation covers three models and five soft tasks rather than the full seven-model set, and the mitigation is evaluated on the same benchmark that defines the phenomenon. The measurement is also of tool-call emission in constructed scenarios rather than of harm in deployed systems.

The result bears directly on several practices recorded elsewhere in this wiki. It is the sharpest counterexample to treating compaction as a purely economic decision (see [[DefinedTerm/context-rot]] and [[DefinedTerm/agentic-memory]]), and it gives a mechanism for the guidance already on [[DefinedTerm/agent-skills]] and [[DefinedTerm/context-files]] that standing rules belong in channels a harness preserves rather than in ones it compacts.
