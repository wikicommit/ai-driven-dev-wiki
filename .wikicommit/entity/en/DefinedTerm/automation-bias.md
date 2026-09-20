---
title: "Automation Bias"
type: "schema:DefinedTerm"
lang: en
tags: [agents, human-oversight, governance, agent-safety]
sources:
  - type: url
    url: 'https://www.imda.gov.sg/-/media/imda/files/about/emerging-tech-and-research/artificial-intelligence/mgf-for-agentic-ai.pdf'
    hash: sha256:ade20c2fa2aedf4f9ea3efe129e8b2ed3cc7823b414e766050586231d956645e
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The tendency to over-trust an automated system, especially one that has performed reliably in the past - a growing concern as humans supervise increasingly capable agents, and the reason human oversight is treated as something to be audited rather than assumed."
---

Automation bias is the tendency to over-trust an automated system, especially when it has performed
reliably in the past. [[TechArticle/model-ai-governance-framework-for-agentic-ai]] identifies it as
one of three challenges to human accountability for agents, alongside actions that emerge
dynamically rather than from fixed logic and a value chain that diffuses responsibility across
multiple actors, and states that it becomes a bigger concern as humans supervise increasingly
capable agents. On that framework's account it is the reason
[[DefinedTerm/human-in-the-loop]] has to be adapted rather than simply adopted for agentic
deployments.

## Usage

The framework treats the effectiveness of human oversight as something to measure over time rather
than something a checkpoint guarantees. Two indicators are named. The human override rate — how
often humans reject or modify agent actions — is read as a signal in the low direction: a low rate
may indicate rubber-stamping. Human response times during review are read in the short direction: a
shorter time may indicate automation bias or review fatigue. It also suggests using data analytics
to identify "outlier" humans whose decision patterns deviate significantly from the norm, which it
says may indicate compromised oversight.

Alongside measurement, the framework recommends training human overseers to recognise common agent
failure modes such as inconsistent reasoning or reliance on outdated policies, and notes in the same
place that chain-of-thought reasoning, sometimes used for explainability, is not analogous to human
reasoning and may not be a faithful explanation of the agent's actions. It also asks that overseers
actually possess the domain expertise to evaluate what they are approving, giving as its example
users who use agents to "vibe code" without the software engineering expertise to review the
robustness of the generated code.

## When It Applies

Guarding against automation bias applies wherever a human approval step is the control an
organisation is relying on, and it assumes that step is frequent enough for a pattern to be visible
in override rates and response times. The framework's own account of why the problem grows is that
the speed of agent decisions makes real-time oversight hard, and that requiring human approvers to
continuously oversee agents as a safeguard can itself produce automation bias and alert fatigue —
so the measures above sit against a background where adding more approval points can make the
underlying problem worse rather than better. Its complementary recommendation is not more approvals
but automated real-time monitoring: alerts on logged events, anomaly detection over agent
trajectories, agents monitoring other agents, and denying action by default when approval
infrastructure fails. These practices are presented as emerging best practice collated with
government agencies and companies, in a document that describes itself as living and expects to be
updated.

## Related Terms

[[DefinedTerm/approval-fatigue]], [[DefinedTerm/human-in-the-loop]],
[[DefinedTerm/cognitive-surrender]], [[DefinedTerm/verification-debt]]
