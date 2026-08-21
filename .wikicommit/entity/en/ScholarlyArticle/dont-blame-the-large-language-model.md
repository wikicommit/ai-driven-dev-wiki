---
title: "Don't Blame the Large Language Model: How Agent Harness Evolution Shapes Coding Agent Quality"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, agent-architecture, empirical-study, metrics, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.03691'
    hash: sha256:2ca8495996618345fe8107bd0b9cf73cf84283dc0135c961a0fadc83ce891c49
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A controlled longitudinal study, dated July 2026, that holds the language model fixed and varies only the [[DefinedTerm/agent-harness]] across 35 sequential Qwen Code CLI releases. It finds no statistically significant improvement in SWE-bench Verified resolve rate across those releases while token consumption and tool calls roughly double, and argues the missing practice is agentic quality assurance."
  author:
    - "Oussama Ben Sghaier"
    - "Hao Li"
    - "Bram Adams"
    - "Ahmed E. Hassan"
  datePublished: "2026-07-20"
---

"Don't Blame the Large Language Model" is an empirical software engineering paper by four authors at Queen's University, Canada, posted to arXiv on 20 July 2026 and submitted to *ACM Transactions on Software Engineering and Methodology*. Its subject is the [[DefinedTerm/agent-harness]] as a *software system that evolves* — "a middleware layer in between a developer and a large language model that orchestrates system prompts, tool execution, context management, and iterative reasoning loops."

Its methodological contribution is an inversion of the usual experimental setup. Where prior work fixes the harness and varies the model, this study fixes the model and varies only the harness, which is what lets it attribute quality changes to the harness rather than conflating them with model updates. The authors state this is the first controlled longitudinal study to isolate the harness contribution, and motivate it from a specific practitioner behaviour: users regularly report quality regressions after harness updates and "consistently attribute them to the underlying model rather than the harness itself."

The design has two parts. A landscape analysis covers five major open-source harnesses — Codex, Qwen Code, Gemini CLI, OpenCode, and OpenHands — measuring release velocity, development activity, and maintenance burden against VS Code and GitHub CLI as baselines. A controlled deep dive then evaluates 35 sequential releases of Qwen Code CLI against 50 stratified tasks from SWE-bench Verified (see [[Dataset/swe-bench]]) while holding the underlying LLM constant, chosen because that harness natively supports custom local LLM endpoints.

## Key Contributions

- **Hyper-churn: harnesses evolve far faster than ordinary software.** The five harnesses average 1.5–18 releases per week and 2.8–34 commits per day, with median pull-request review times under four hours, against 0.6–0.8 releases per week for VS Code and GitHub CLI over the same period — making the most active harnesses 13–28× more release-intensive. The paper names this pattern **hyper-churn**. The mechanism it identifies is not raw commit volume but conversion rate: agent harnesses need only 7–14 commits per release on average, against 421.4 for VS Code and 52.2 for GitHub CLI, even though VS Code sustains a higher commit rate at 47.9 per day. The authors note the near-instantaneous review times "may partly reflect the use of agentic AI for code review, given that these projects are themselves agent harnesses."
- **Issue backlogs grow rather than close.** Gemini CLI accumulated 9,951 issues in 224 days, OpenCode 8,621 in 278 days, and Codex 5,574 in 293 days. The comparison the paper draws is with close rates rather than volumes: VS Code took 40,074 issues over twelve months but closed 89.3% of them with a dedicated team averaging 68 active contributors per month, and GitHub CLI received 1,118 with an 82.1% close rate. Bug-fix commits account for roughly 30% of all development effort across the harnesses.
- **The central negative result.** Across the 35 Qwen Code releases with the model held fixed, there is **no statistically significant improvement in task resolve rate** — and early versions sometimes outperform their more sophisticated successors. Meanwhile token usage and tool-call counts more than double in some cases without corresponding gains. The authors call this "a fundamental disconnect between development activity and agent effectiveness." They also report that failed tasks consume more resources than successful ones, and trace token inflation to larger system prompts compounding with more conversation turns.
- **Which release patterns move quality.** Feature-heavy releases correlate significantly with higher resolve rates (ρ = 0.438) but at the cost of increased token consumption and tool calls; fix-heavy releases raise token consumption without improving resolve rates; releases with larger average PR sizes correlate with *lower* token consumption, which the authors read as consolidating changes into coherent PRs costing less overhead than many small ones; and higher code-deletion volume is associated with lower token consumption. Refactoring churn ratio and release cadence show no quality benefit.
- **Which components are risky to touch.** Mapping every commit onto a reference harness architecture, the paper identifies the **LLM Provider layer** and **Context Management** as high-risk zones whose modifications are most frequently associated with quality degradation — the authors' explanation being that these directly govern how information passes to and from the model. Changes to **Extensibility** and **Security** components are consistently associated with safe or neutral outcomes. Expanding context management specifically is associated with lower token efficiency.
- **The proposed missing practice.** The paper attributes all of the above to the absence of **agentic quality assurance**: automated quality regression testing that evaluates the agent's actual non-functional quality — token consumption, tool-call overhead — rather than merely verifying the correctness of a generated patch. Its supporting evidence is that its inspection of the projects' CI/CD pipelines found that "every concrete example of quality degradation we document passed all existing automated checks." Its recommendations are that developers monitor resolve rate, token consumption, and tool-call overhead across releases, and that researchers "report and control for agent harness versions alongside the underlying LLM."

## Notes

The paper's own stated reason why this practice does not already exist is cost: running representative evaluations at the commit cadence of an actively developed project is expensive, which is also why the regressions it documents are invisible to conventional unit and integration tests — they are "emergent behavioral effects of the interaction between the agent harness and the LLM."

Two boundaries are worth keeping in view when reading the negative result. The controlled deep dive covers one harness (Qwen Code CLI) with one model family and 50 stratified SWE-bench Verified tasks, so the no-improvement finding is established for that configuration rather than across harnesses; the landscape analysis covering five harnesses establishes only the development-intensity picture, not the quality one. And resolve rate on a bug-fixing benchmark is a narrow definition of quality — the cautions recorded on [[Dataset/swe-bench]] about test-passing as a proxy for merge-readiness apply here too.

The finding is nonetheless the sharpest available empirical support for the premise behind [[DefinedTerm/harness-engineering]] — that the harness, not the model, is where a large share of agent behaviour is determined — while cutting against the assumption that a newer harness is a better one.
