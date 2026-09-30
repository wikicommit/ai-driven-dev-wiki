---
title: "ACEM: A Cost Estimation Model for Agentic Software Engineering"
type: "schema:ScholarlyArticle"
lang: en
tags: [cost-estimation, agentic-software-engineering, token-cost]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2608.02582'
    hash: sha256:0e05d11555293c33baf18153cef7b96135fff0fa8a7ccbb142696d546c2ec904
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A paper from Cairo University proposing ACEM (Agentic Cost Estimation Model), which splits the cost of agentic software development into LLM token, human-in-the-loop and infrastructure dimensions and maps traditional sizing metrics onto estimated token consumption. It is presented as an early-stage, not yet validated proposal."
  author: ["Mohammad El-Ramly"]
  abstract: "Software cost estimation models from COCOMO II to Function Points to Story Points assume that development effort is primarily a function of human labor, an assumption that agentic software engineering challenges. The paper proposes ACEM, decomposing total agentic development cost into LLM, HITL and infrastructure cost without assuming a fixed hierarchy among them, introduces the Revision Factor, the Context Factor and the HITL Intensity Score, and maps Use Case Points, Story Points and Function Points to estimated token consumption. The model is fully specified with symbolic constants and has not yet been validated against real project data."
  keywords: ["software cost estimation", "agentic software engineering", "token consumption", "human-in-the-loop", "use case points", "story points"]
---

This paper argues that established software cost estimation models — COCOMO II, Function Point
Analysis, Use Case Points and Story Points — share the assumption that development effort is a
function of human labor, and that agentic software engineering breaks it. When autonomous agents do
substantial implementation work, human effort shifts from continuous production to planning,
specifying, architecting and validating agent output, and new cost drivers appear: LLM token
consumption across agent actions, [[DefinedTerm/human-in-the-loop]] (HITL) effort for oversight and
correction, and infrastructure for agent orchestration and tooling. These costs are also
non-deterministic, since the same task run twice can consume different numbers of tokens and need
different amounts of human correction.

The paper's answer is ACEM, the Agentic Cost Estimation Model. It models total cost as the sum of
LLM cost, HITL cost and infrastructure cost, treated as additive components without a fixed
hierarchy between them, because the author argues their relative size varies with task complexity,
agent autonomy and pricing model. LLM cost is estimated per task from base input and output tokens
(looked up by artifact type and a three-level complexity scale), multiplied by two corrective factors
and by per-token prices; HITL cost is the sum of checkpoint review time and expected rework time at a
reviewer's hourly rate. Infrastructure cost is included for completeness and follows existing cloud
cost modelling rather than introducing new constructs.

The author presents ACEM as a fully specified model structure and calibration method whose constants
are deliberately left symbolic, and states that it has not been validated against real project data.
The paper closes with a proposed evaluation programme and an invitation to others to calibrate, test
and extend the model.

## Key Points

- The Revision Factor, RF = 1 + (r × n), models token overhead from rejected agent output, where r is
  the rejection rate for a task type and n the average number of extra invocations per rejection; the
  paper describes it as a conservative lower bound, since a retry usually carries extra context.
- The Context Factor, CF = 1 + α × (i/N), models the growth in input tokens as context accumulates
  along a pipeline of N tasks. The paper calls the linear profile a simplifying assumption and notes
  it should not be applied to token counts measured from API logs, which already include
  accumulated context.
- The HITL Intensity Score classifies the oversight a task type needs into four levels, from HIS-1
  (review only at milestone boundaries) to HIS-4 (a human approves every agent action), chosen
  through a decision matrix over domain risk, agent reliability, task complexity and regulatory
  requirements.
- Use Case Points, Story Points and Function Points are mapped to total base token consumption
  through calibration constants (tokens per use case point, per story point, per function point),
  using the unadjusted UCP and FP counts; the paper frames this as empirical correlation — sizing
  metrics as proxies for task complexity — rather than as a claim that they still measure developer
  hours.
- Calibration is a four-step pilot: run a representative sample of tasks, estimate base tokens per
  artifact type and complexity, derive rejection rates, retries and the context coefficient, then
  derive the sizing-metric constants. The paper names computing base tokens from context-inclusive
  input counts as the most common calibration error, because the Context Factor then double-counts
  context growth.
- Two worked examples, using illustrative rather than calibrated figures, put LLM cost at about 5.5%
  of total cost for a simple, standard-oversight task and about 23.2% for a complex task run with
  minimal oversight, which the paper uses to argue that the balance between token and human cost
  shifts with complexity and autonomy rather than being fixed.

## Notes

The author positions ACEM against two earlier papers by Alaswad et al.: a conceptual framework
arguing that LLM-assisted development invalidates the assumptions behind COCOMO, Function Points and
Story Points, and an empirical follow-up that measured effort in developer time rather than tokens.
ACEM's stated contribution is to connect artifact-level sizing to the token as the operating cost
unit of agentic pipelines.

Stated limitations and assumptions include a sequential single-pipeline structure, a task
decomposition done before estimation, constant rejection rates per task type, a single reviewer rate,
independent cost components, and the open questions of whether r, n and α can be separated from pilot
data and whether the constructs capture independent variance. The paper names non-determinism as the
most fundamental challenge for any agentic cost model and suggests that a probability distribution
over costs, for example from Monte Carlo or Bayesian methods, may ultimately suit the domain better
than a deterministic parametric model.
