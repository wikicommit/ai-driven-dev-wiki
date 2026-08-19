---
title: "verification debt"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, verification, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.20456'
    hash: sha256:fcf0fa7c744985d64d3d71a71e82e882a7ad1f5133fca691f23cb211cd7ae8b3
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The condition in which an agent's output of code, tests, documentation, and patches grows faster than a team's capacity to verify it, accumulating weak tests, hidden regressions, broad patches, unvalidated dependencies, undocumented behavior, and increased reviewer burden."
---

Verification debt is the term Christopher Koch uses in [[ScholarlyArticle/agentic-agile-v]] for what accumulates when an agent's output volume grows faster than a team's verification capacity. Agentic AI can increase the volume of code, tests, documentation, and patches; if verification does not keep pace, the result is weak tests, hidden regressions, broad patches, unvalidated dependencies, undocumented behavior, and increased reviewer burden.

## Usage

The concept follows from a diagnosis Koch states at the outset: agentic AI can generate plausible engineering artifacts faster than humans can inspect them, so the bottleneck shifts from code synthesis to specification quality, execution context, verification, traceability, and controlled iteration.

He grounds the risk in empirical results rather than presenting it as a theoretical concern. The paper points to the METR randomized trial — in which AI tools increased task completion time for experienced developers working in mature repositories — and to maintenance-burden research suggesting AI-assisted output may shift review and rework load toward experienced developers, as indications that review and cleanup can erase perceived speedups.

The paper argues the stakes rise sharply outside pure software. In hardware and embedded work, it states, verification debt can become operational or physical risk, because incorrect pin mappings, register values, timing assumptions, bus behavior, reset handling, or memory layout can produce failures that are costly or unsafe. Its corresponding rule for those domains is that compilation is not proof, and that simulation, formal checking, hardware-in-the-loop tests, timing analysis, and traceability from requirement to verification evidence are essential.

Verification debt is the problem [[DefinedTerm/agentic-agile-v]] is constructed to counter. The framework's answers to it are the Prove and Verify steps of the [[DefinedTerm/scope-v]] loop, which treat verification as recurring rather than final; risk-adaptive acceptance gates that scale required evidence to the risk class of the task; and an evidence-bundle acceptance model under which agent output is not accepted because it is plausible but because it satisfies evidence appropriate to its risk level. Among the paper's practical recommendations for teams are separating implementation and verification agents where risk is high, and tracking review load, defect escape, rework, and lead time rather than only code volume.

The paper also names it as an open research question, asking whether evidence bundles can reduce verification debt without eliminating productivity gains.

## Related Terms

Verification debt is the motivating problem behind [[DefinedTerm/agentic-agile-v]] and its [[DefinedTerm/scope-v]] task loop. Koch frames the shift it demands as one away from [[DefinedTerm/vibe-coding]] at scale and toward verified engineering with agents inside the loop.
