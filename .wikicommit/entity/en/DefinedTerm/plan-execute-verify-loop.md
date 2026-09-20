---
title: "Plan–Execute–Verify Loop"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, verification, agent-tooling, sandboxing]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.18747'
    hash: sha256:b1035aaed7f12c5fa8504dac7f47c2e10dda381065834be2cea784c2f758fb1f
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A harness-level control loop in which a plan forms a contract over an intended change, execution applies it inside a sandboxed and permissioned environment, and verification through deterministic sensors decides whether the resulting state is accepted, revised, escalated or rolled back."
---

The Plan–Execute–Verify loop (PEV) is the control loop [[ScholarlyArticle/code-as-agent-harness]] proposes for turning a model's intentions into bounded, observable and revisable state transitions. Its three phases are: the harness externalises an intended change together with its validation criteria, executes that change inside a sandboxed and permissioned environment, and then verifies the resulting state through deterministic sensors and human-review gates. The framing's purpose is unification — it treats planning, execution, debugging, verification and escalation as parts of a single harness-level control process rather than as separate stages, and in particular recasts feedback-guided debugging as control over executable program state rather than a post-hoc correction step.

## Usage

**Planning as contract formation.** In this framing a plan does more than decompose a request into implementation steps: it identifies relevant files, expected invariants, validation commands, rollback points and risky operations, which makes it a harness artefact rather than an unobserved reasoning trace. In repository-level tasks such artefacts constrain the subsequent action space by specifying which components may be read, which files may be edited, and which criteria must be satisfied before completion.

**Sandboxed execution and permissioned state transition.** The execution phase realises the plan as a bounded, observable transition inside an isolated filesystem, dependency state, shell, language runtime, browser or IDE interface, and resource boundary. The survey argues sandboxes also improve reproducibility, because the harness can replay the same patch, command, seed, dependency lockfile or test configuration under comparable conditions — without which verification signals become hard to interpret and failures may reflect environment drift rather than program defects. Execution is additionally permissioned across a read-only tier, a sandbox-edit tier, and a full-access tier whose actions the authors argue should require human-in-the-loop gates.

**Verification through deterministic sensors.** The verification phase compares the new state against explicit constraints using a graded set of signals: compilation and static-analysis feedback as low-cost sensors before full execution, runtime signals that surface only along concrete execution paths, and test-based feedback evaluating whether observed behaviour satisfies the intended specification. The survey's argument for preferring these over natural-language critique is that they are deterministic, or at least reproducible enough to serve as control signals — and it holds that human or agentic critiques remain useful where failure evidence is sparse, but should interpret sensor outputs rather than replace them.

Verification also supplies the evidence for what happens next, which is why the survey treats repair, reflection and termination as consequences of the Verify phase rather than as an independent stage. The same sensor evidence determines whether to diagnose the failure, retrieve missing context, regenerate a localised patch, route the task to another agent, or abandon the branch. The authors are explicit that termination should be governed by verification rather than by model confidence: a loop stops when required checks pass, when further attempts no longer improve the state, when the risk tier changes, or when human review is required.

The survey describes the harness in this role as a cybernetic governor — a control layer that observes the effects of agent actions through deterministic sensors such as linters, parsers, compilers, type checkers, tests, static analysers, fuzzers, runtime monitors and CI pipelines, and regulates subsequent state transitions rather than merely forwarding error messages to the model.

## When It Applies

PEV applies where an agent mutates state that someone cares about — a repository, a running system — and where sensors exist that can tell whether a transition was acceptable. The survey's own framing makes the dependency explicit: reflection is reliable only when it remains grounded in executable evidence, so the loop presupposes evidence worth grounding in.

Its failure mode is a weak oracle. The survey warns that a harness can become overconfident precisely because it has executable feedback — unit tests may be incomplete, static analysers may over-approximate, GUI checkers may miss unacceptable intermediate actions, and a green test is not the full specification. Where the verifier is weak, the authors argue, a self-repairing or self-evolving harness will learn to optimise against the wrong signal.

PEV is presented as the survey's own synthesis of a body of existing work rather than as a single system's design or a measured result: the authors say the framing unifies static analysis, runtime errors, tests, critique, self-reflection and human review as components of one control process, and their stated conclusion is that reliability comes from governed state transitions rather than from better repair prompts.

## Related Terms

- [[DefinedTerm/agent-harness]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/verification-loop]]
- [[DefinedTerm/output-verifiability]]
