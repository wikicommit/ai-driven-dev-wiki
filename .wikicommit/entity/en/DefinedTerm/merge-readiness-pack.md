---
title: "Merge-Readiness Pack"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, code-review, human-ai-collaboration, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "In the Structured Agentic Software Engineering framework, a structured evidence bundle an agent submits instead of a raw pull request, proving its work is trustworthy against five criteria: functional completeness, sound verification, exemplary SE hygiene, clear rationale, and full auditability."
  termCode: "MRP"
---

A Merge-Readiness Pack (MRP) is the agent-generated deliverable proposed in [[DefinedTerm/structured-agentic-software-engineering]] as the target artifact of an agentic task. Rather than reviewing dozens of raw pull requests, a human reviewer audits a structured bundle of evidence designed to bridge the gap between typical agent output and the standards of a genuinely merge-ready contribution.

## Usage

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] specifies five criteria an MRP must supply evidence for, each paired with the gap it is intended to close:

| Criterion | The gap | The evidence |
| --- | --- | --- |
| Functional completeness | Agents often produce superficial or partial fixes that pass a narrow set of tests but fail to address the holistic user need | Proof, such as end-to-end test results, that the feature is complete and behaves as specified in realistic scenarios |
| Sound verification | Agents may generate code that passes an existing, weak test suite, or fail to create new robust tests for their own logic | Not just passing test logs but the agent's test plan and the new test cases it generated, proving the verification strategy is itself sound |
| Exemplary SE hygiene | Agent-generated code can be functional but hard to maintain, violating project style guides or principles such as DRY and SOLID | Reports from static analysis, linting, and complexity checkers |
| Clear rationale and communication | An agent's reasoning is often buried in low-level, verbose trajectory files or chat logs that are impractical to audit | A clear, human-readable summary — analogous to a pull request description — explaining the approach and trade-offs |
| Full auditability | Reproducibility is hard because of agent non-determinism and environment changes | A "frozen" audit trail including versioned links to the exact BriefingScript, MentorScript, tools, and agent trajectory used |

To keep this density of information reviewable, the paper specifies that the pack must support "progressive disclosure": a reviewer sees a high-level summary and can then drill down into specific evidence such as test logs or execution traces as needed.

The MRP is motivated in the paper by a diagnosed shortfall in current agent output. It cites examinations of agent-generated code and agent-driven pull requests, together with the authors' own hands-on experience, as showing that many agent efforts still fail to meet the quality bar of being truly merge-ready — often containing subtle regressions, superficial fixes, or weak engineering hygiene. The same argument is made about benchmark results: the paper's position is that passing tests, even on verified tasks, is not enough, and that achieving merge-ready status requires a deeper understanding of context, intent, and the broader system.

In the framework's process model, the structure of an MRP is declared by a LoopScript as the evidence-based acceptance criteria for a task, and the pack is consumed by the human under an activity the paper calls Agentic Guidance Engineering (AGE), which produces a Version-Controlled Resolution explicitly linked back to the artifact it addresses.

## Related Terms

The MRP is one of two agent-generated artifacts in the framework; the other is the [[DefinedTerm/consultation-request-pack]], raised mid-task when an agent needs human judgment rather than submitting finished work. Both are reviewed by the human coach inside the [[DefinedTerm/agent-command-environment]], and both are contextualized by the [[DefinedTerm/briefing-script]] that initiated the task.
