---
title: "ClawVM: Harness-Managed Virtual Memory for Stateful Tool-Using LLM Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [agent-architecture, context-engineering, agentic-loop]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.10352'
    hash: sha256:7a767caa51983f4f753aa5982e1e2dae9ca37450e66a43fe2e0d7b116d017c7f
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A EuroMLSys 2026 paper arguing that agent harnesses manage context residency and durability as best-effort heuristics where an operating system would use virtual memory. It proposes managing agent state as typed pages with minimum-fidelity invariants enforced at every lifecycle boundary, and reports eliminating all policy-controllable faults when the minimum-fidelity set fits the token budget."
  author:
    - "Mofasshara Rafique"
    - "Laurent Bindschaedler"
  datePublished: "2026-04"
---

"ClawVM" is a paper by Mofasshara Rafique (independent researcher) and Laurent Bindschaedler (Max Planck Institute for Software Systems), presented at the Sixth European Workshop on Machine Learning and Systems (EuroMLSys '26), Edinburgh, 27–30 April 2026.

Its subject is a class of agent that runs for hours or days across many sessions — persistent assistants managing email, calendars, smart-home devices, messaging, and web automation — for which "the model context window is scarce working memory: it must hold constraints, the active plan, recent dialogue, and tool outputs needed for correct action, while transcripts and artifacts reside in durable backing stores." Coding agents are described as "a narrower but equally demanding subclass" of the same problem.

The failure the paper targets is what happens when the needed state is absent or the correct state is silently discarded: "agents repeat work, violate user preferences, and lose progress mid-plan." Its argument that these are not edge cases rests on public issue trackers and practitioner reports documenting three recurring patterns — rules and constraints lost after context summarization, state silently dropped on session reset, and persistence operations that overwrite rather than merge.

## Key Contributions

- **A diagnosis stated as a missing contract.** The paper accepts that modern harnesses already provide the building blocks — pruning, retrieval, compaction, pre-compaction memory flushes, and external memory plugins — and its criticism is precise: "these improve recall quality, but none provides an enforceable contract over residency, durability, or auditability." Practitioners respond with configuration tweaks and add-on layers, "yet flushes can still be bypassed, writeback can still be destructive, and no mechanism guarantees that critical state survives lifecycle transitions."
- **The operating-systems analogy, pushed further than usual.** Its framing is that "operating systems learned this lesson decades ago: when a runtime manages a fast, scarce tier alongside slow, durable storage, the answer is virtual memory, not best-effort heuristics." The paper notes that prior work has borrowed the paging metaphor but that "no production harness enforces it."
- **Typed pages with minimum-fidelity invariants.** ClawVM manages agent state as typed pages that can be kept at full detail, compressed, reduced to structured fields, or shrunk to a pointer under token-budget pressure. Each page carries a **minimum-fidelity invariant** — how far it may degrade before reclaiming space — and the harness enforces these at every lifecycle boundary, with validated writeback.
- **The harness as the enforcement point.** The paper's argument for placing the mechanism in the harness rather than in a plugin is structural: "because the harness already assembles prompts, mediates tools, and observes lifecycle events, it is the natural enforcement point; placing the contract there makes residency and durability deterministic and auditable."
- **Reported results.** Across synthetic workloads, 12 real-session traces, and adversarial stress tests, ClawVM is reported to eliminate all policy-controllable faults "whenever the minimum-fidelity set fits within the token budget," confirmed by an offline oracle, while adding a median of under 50 microseconds of policy-engine overhead per turn.

## Notes

The reported guarantee is conditional in a way worth stating plainly: faults are eliminated *when the minimum-fidelity set fits within the token budget*. That condition names the real design problem rather than solving it — declaring which pages must survive, and at what fidelity, is a judgment the operator has to make, and the mechanism enforces it rather than deciding it. What the paper contributes is turning residency and durability from emergent properties of a summarizer into a stated, checkable contract.

Its diagnosis converges from an independent direction with [[ScholarlyArticle/governance-decay]], which measures the same "rules and constraints lost after context summarization" failure and reaches the same structural conclusion — that some state must be quarantined from lossy compaction rather than trusted to it. The two propose comparable remedies at different scopes: Constraint Pinning protects governance rules specifically, while ClawVM generalises to all agent state through a typed-page abstraction. Both make the harness the enforcement point, which is the same location [[DefinedTerm/agent-harness]] identifies as owning context management.

The evaluation is of the authors' own system on their own workloads, with 12 real-session traces alongside synthetic and adversarial ones, and its target is persistent general-purpose assistants rather than coding agents specifically.
