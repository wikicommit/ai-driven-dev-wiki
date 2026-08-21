---
title: "Productivity-Reliability Paradox"
type: "schema:DefinedTerm"
lang: en
tags: [productivity, code-quality, verification, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.01160'
    hash: sha256:5df903e44f8c186d0b13aaf412c53e475ccd30551e159a2cbba53b5c0a79dd50
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A term proposed by Farrag (2026) for the phenomenon in which AI coding assistants produce statistically significant gains in individual-level output metrics that coexist with statistically significant degradation in system-level dependability metrics."
  termCode: "PRP"
  inDefinedTermSet: ""
---

The Productivity-Reliability Paradox — abbreviated PRP — is a term proposed in [[ScholarlyArticle/productivity-reliability-paradox]] for the empirically observed phenomenon in which AI-powered coding assistants produce statistically significant improvements in individual-level output metrics (task completion speed, lines of code, suggestion acceptance rates) that coexist with statistically significant degradation in system-level dependability metrics (delivery stability, change failure rate, code churn, defect density in production). It is that paper's own coinage rather than an established term in the field.

The paper is precise about why it calls this a paradox rather than a trade-off. A trade-off would be a conscious exchange of quality for speed; the PRP is the claim that the *same* intervention simultaneously improves and degrades different dimensions of the same system. Its illustrative case is that developers perceive themselves as faster — a perception the paper says the METR study's self-reports confirmed even where objective measurement showed a 19% slowdown — while the systems they produce show measurable dependability regressions.

## Usage

**The contradictory evidence it is built from.** On the gain side the paper cites a GitHub-run controlled study finding developers with Copilot completed tasks 55–56% faster, a McKinsey laboratory experiment finding tasks completed up to twice as fast, and a Google enterprise randomised controlled trial measuring a 21% speedup. On the degradation side it cites the METR randomised controlled trial, which it calls the most methodologically rigorous study in the literature, finding 16 experienced open-source developers 19% slower with AI tools despite forecasting a 24% speedup; Google's 2024 DORA report associating a 25% increase in AI adoption with a 7.2% decrease in delivery stability; GitClear's analysis of 153 million changed lines projecting a doubling of code churn by 2024; and Uplevel Data Labs finding higher bug rates among developers with Copilot access without corresponding throughput gains.

**Three moderating variables** are what the paper says dissolve the apparent contradiction. *Task abstraction level*: the tools excel at low-abstraction syntactic work and struggle with high-abstraction architectural decisions. *Codebase maturity*: greenfield projects benefit disproportionately, while mature codebases incur verification overhead that can exceed the generation savings. *Developer experience*: novice developers show gains of 30–40% but exhibit measurable skill atrophy, while senior developers meet a "verification tax" that can negate nominal speedups.

**Two amplifying mechanisms** are described as distinct from the causes. The context window constraint means an agent progressively loses awareness of distant modules, implicit conventions and cross-cutting dependencies as a project grows, producing code that is locally correct but systemically incoherent, and — for autonomous multi-step runs — drift in which later steps contradict earlier decisions. The code review bottleneck is the organisational counterpart: the paper cites Faros AI's 2025 telemetry across more than 10,000 developers in 1,255 teams, where high-AI-adoption teams completed 21% more tasks and merged 98% more pull requests, but PR review time rose 91%, average PR size grew 154%, and bug counts rose 9%, with organisational DORA metrics showing no measurable improvement.

**Its proposed resolution** is governance rather than better models: the paper's thesis is that specification discipline, not model capability, is the binding constraint on AI-assisted software dependability, formalised as the [[DefinedTerm/specification-governance-model]]. It also reads the paradox temporally, as the bottom of a productivity J-curve where the complementary intangible investments have not yet been made.

## Related Terms

The PRP overlaps with, and is argued to be amplified by, the [[DefinedTerm/verification-bottleneck]]; its temporal reading is the [[DefinedTerm/ai-adoption-j-curve]]. The governance response the paper derives from it is [[DefinedTerm/spec-driven-development]], operationalised through the [[DefinedTerm/specification-governance-model]] and classified across methodologies by the [[DefinedTerm/ai-augmented-methodology-taxonomy]].
