---
title: "Agent-Native Training"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, training, evaluation, agent-state]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.20683'
    hash: sha256:4d2fd9336c3ac20f51ab2d6d4fc4eb98e0ba0673a8d3475e0e286c3fdfc4511a
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The fourth paradigm in Guo et al.'s account of agent engineering, in which agentic behaviours such as planning, tool use, verification and recovery are trained into model parameters through interactive environments, and in which the model, harness and improvement loop co-evolve from deployment traces."
---

Agent-native training is the fourth of the four paradigms of agent engineering set out in [[ScholarlyArticle/survey-on-agent-system-and-harness-design]], following prompt engineering, workflows and context engineering, and harness engineering. It has two directions. The first is internalization: rather than relying solely on prompts, workflows or runtime orchestration, models are trained in interactive environments to plan, use tools, verify intermediate states and recover from errors, so that behaviours first implemented externally may gradually become partially learned inside the model. The second is co-evolution: over deployment, the model, the harness and the improvement loop may all be updated from execution traces that indicate what to keep, change or undo. The survey is explicit that this does not eliminate the harness — it shifts the design question toward how much of agent behaviour is learned in the model, how much stays in the runtime, and how the full stack improves safely over time.

## Usage

For internalization the survey distinguishes two tendencies in recent work: strengthening reasoning-to-action behaviour through reinforcement learning, treating multi-step reasoning, action selection and verification as trainable rather than purely prompt-induced; and reducing train–test mismatch by training agents in environments closer to deployment. It characterises the net effect as a shift in the division of labour rather than a removal of the harness, with more short-horizon behaviour moving into model parameters while the runtime still supplies environment access, state and safety control.

For co-evolution the survey offers a constrained self-evolution loop as a useful abstraction: running the agent produces traces, from which the system extracts an evidence set of outcomes, failure modes, verifier results, cost profiles and safety events; an update operator may then change the model, the harness, or both; and the result is retained only if it passes held-out tasks, regression tests, process checks and safety constraints, and is otherwise rejected or rolled back. The survey presents this not as a fixed algorithm but as a way of making the control structure explicit — reliable self-evolution must couple experience extraction, credit assignment, modification and validation.

The survey separates three layers it says are often conflated under "self-evolve": multi-model harnesses define *who* performs each runtime role, learnable harnesses define *how* runtime policies are optimized, and co-evolution defines *when and how* the model, harness and improvement loop are jointly updated from deployment experience. It treats these as complementary rather than interchangeable.

## When It Applies

This is a direction the survey identifies as future work rather than settled practice: its paradigm diagram marks harness engineering as the current frontier and agent-native training with co-evolution as future. It also notes that all four paradigms coexist in practice today. In the loop the survey describes, execution traces are what the evidence set is extracted from, so the paradigm presupposes traces carrying outcomes, failure modes, verifier results, cost profiles and safety events.

The survey names the risks it sees as specific to this paradigm: benchmark overfitting, incorrect failure attribution, stale memory, and unsafe runtime modification. It reports, as the key lesson of one cited system that freezes the base model and evolves coding-agent harness components from observability-driven feedback, that self-evolution must be observable and falsifiable: components should be explicit and revertible, traces should be distilled into evidence, and proposed changes should make predictions that later outcomes can check. It adds that agent-native training turns the harness into a training environment, evidence pipeline, verifier and governance layer, with held-out evaluation, ablations, audit logs, rollback and human approval for high-impact changes. The survey also cautions that parameter updates alone cannot absorb all runtime bottlenecks, since many failures arise from harness choices such as observation format, action granularity, memory retrieval or verifier timing.

## Related Terms

- [[DefinedTerm/execution-harness]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/prompt-engineering]]
- [[DefinedTerm/value-aware-agent-evaluation]]
