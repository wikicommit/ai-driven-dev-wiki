---
title: "Governed AI-Assisted Engineering: Graduated Human Oversight for Agentic Code Generation in Regulated Domains"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, governance, human-ai-collaboration, code-review]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.22484'
    hash: sha256:8f1931054ccf2ec54cb6c22999eaff8b64c45d2e2def87a208bed1a6895ad2e8
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A 2026 paper proposing GAIE, a three-tier graduated human oversight model that routes agentic code-generation tasks by regulatory impact, customer proximity, reversibility, and data sensitivity rather than applying uniform review. It maps the tiers to several jurisdictions' AI regulations and estimates the velocity cost of the arrangement."
  author:
    - "Richard Kang"
  datePublished: "2026-07-04"
---

"Governed AI-Assisted Engineering" is a single-author paper by Richard Kang of DoiT International, revised on arXiv 4 July 2026. Its problem is one of calibration rather than of permission: the adoption of agentic coding systems "creates a governance challenge in regulated industries," and the paper's criticism of existing frameworks is that they "address AI-assisted development maturity or the productivity-reliability tension but offer no mechanism for calibrating human oversight intensity to regulatory impact."

Its statement of the underlying tension is drawn from conflicting evidence rather than from a single claim. It reports that controlled studies find productivity gains of 20–56% on well-scoped tasks, that "the most rigorous randomized controlled trial documents a 19% slowdown for experienced developers," and that telemetry across large developer populations shows substantially more pull requests but far longer review times with flat delivery metrics. Those figures are the paper's citations of other work rather than its own measurements.

## Key Contributions

- **A graduated oversight model.** GAIE is a three-tier arrangement in which the amount of human involvement is set by the nature of the change rather than applied uniformly: **human-in-the-loop** for strategic functions, **human-over-the-loop** for customer-impacting work, and **automated-with-monitoring** for internal work.
- **A deterministic router.** The **Oversight Classification Model (OCM)** is "a deterministic decision function that classifies code generation tasks by regulatory impact, customer proximity, reversibility, and data sensitivity" and routes each into one of the three tiers. Making the routing deterministic is what distinguishes this from case-by-case judgment: the tier a change lands in is derivable from its properties.
- **Evidence requirements attached to each tier.** Each tier "defines required evidence artifacts for compliance auditability," which is what makes the model usable as a compliance mechanism rather than only as a policy.
- **Cross-jurisdiction mapping.** The paper maps GAIE against the Bank of Thailand's 2025 AI risk-management policy and argues applicability to MAS (Singapore), the NIST AI Risk Management Framework, ISO/IEC 42001, and the EU AI Act.
- **An estimated cost of governance.** Evaluated through regulatory coverage analysis, comparative framework analysis, and analytical productivity modeling, the paper suggests that graduated oversight "preserves 84–97% of agentic coding velocity (central estimate: 91%)" while maintaining compliance evidence coverage.

## Notes

The velocity figure is the paper's central selling point and its weakest evidence. It comes from analytical modeling rather than from deployment: no organisation is reported to have run GAIE and measured what it cost them. The 84–97% range should be read as what the model implies under its own assumptions.

What the framework contributes independently of that number is the routing criterion. Most discussion of human oversight in agentic coding treats review as a single dial to be turned up or down — the argument recorded in the comment thread on [[BlogPosting/spec-driven-development-a-spec-first-approach-to-ai-native-engineering]], for instance, runs between "human gates are hindrance" and "human gates are accountability" as though one setting must apply throughout. GAIE's premise is that the dial should be per-change and derivable, with reversibility and customer proximity doing the work.

That premise finds unintentional empirical support in [[ScholarlyArticle/security-in-the-age-of-ai-teammates]], which measures human reviewers *already* triaging agentic pull requests — a median 3.92 hours on security-relevant ones against 0.11 hours on the rest — but doing so on surface cues such as complexity and verbosity rather than on stated risk properties. Read together, the two suggest graduated oversight is happening whether or not it is designed; the question GAIE addresses is whether the grading is principled and auditable.
