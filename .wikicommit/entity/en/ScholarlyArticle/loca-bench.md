---
title: "LOCA-bench: Benchmarking Language Agents Under Controllable and Extreme Context Growth"
type: "schema:ScholarlyArticle"
lang: en
tags: [benchmark, evaluation, context-engineering, agent-architecture]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2602.07962'
    hash: sha256:795a9ba68ee512a5cd028441b92ad7ecf110f3ae5db70692b69b065e92a2a77a
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A February 2026 HKUST paper introducing [[Dataset/loca-bench]], which scales an agent's context by scaling the environment it must explore rather than the prompt it is given. It reports that accuracy falls sharply as context grows even with task semantics fixed, and that context engineering strategies recover a substantial part of the loss — unevenly across models."
  author:
    - "Weihao Zeng"
    - "Yuzhen Huang"
    - "Junxian He"
  datePublished: "2026-02-08"
---

"LOCA-bench" is a paper by three authors at HKUST, posted to arXiv in February 2026. It addresses a mismatch between how long-context ability is measured and how it is used: existing benchmarks mostly assume a static setting in which the model receives all relevant information upfront or can retrieve it in one step, so the task reduces to finding a needle in a haystack or aggregating scattered facts. Real agentic work, the paper argues, is dynamic — an agent begins with limited knowledge of its environment, decides what to look for, explores during execution, and continually adds what it discovers to its own context.

That reframing changes what the difficulty *is*. In the paper's formulation, "the core difficulty is not just finding the right evidence once, but remaining organized and reliable at every action as the context grows over time."

Its instrument, [[Dataset/loca-bench]], scales context by scaling the environment rather than the prompt: environment description length — the size of an Excel sheet, a PDF, a database — is varied while task semantics stay fixed, which lets context length be extended "potentially to infinity in a controlled way" without making the task itself harder. The benchmark is open-sourced.

## Key Contributions

- **A controlled axis for context growth.** Because the environment is generated from a configuration and the task prompt is held constant, any change in success rate is attributable to context length rather than to task difficulty. This is the paper's methodological claim, and it is what distinguishes the benchmark from static long-context suites.
- **Four failure dimensions that appear as context grows**, which the benchmark is designed to surface together rather than in isolation: complex retrieval and reasoning over multiple pieces of evidence from tool outputs; instruction following, where multi-constraint tasks expose that "agents frequently forget earlier instructions"; environment exploration, where the authors report agents exploring less and behaving more conservatively as context lengthens; and hallucination, where models under longer contexts are reported "often subtly altering factual details during generation."
- **Agents evaluated as model *plus* scaffold.** The benchmark decouples environment, tools, tasks, and scaffold, integrating context engineering strategies into the evaluation harness — context editing such as removing stale tool calls and results, stripping thinking content, and compacting conversation history, plus context awareness, memory tools, and programmatic tool calling. This makes the context-management choice a measured variable rather than an uncontrolled part of the setup.
- **The degradation result.** Most models score above 70% accuracy at short context; as context grows, "performance drops sharply even though the underlying task does not change," and the gap between frontier and open-source models widens.
- **The recovery result, and its unevenness.** Context engineering strategies are reported to substantially improve performance, but "models differ in how efficiently they apply these strategies, with frontier models generally benefiting more than open source models." Programmatic tool calling in particular is reported to substantially reduce the intermediate cost of exploration while improving tool orchestration.

## Notes

The paper positions its degradation finding against the phenomenon it names as commonly called [[DefinedTerm/context-rot]], and its contribution there is one of measurement rather than of explanation: it does not propose a mechanism, it builds an axis along which the effect can be observed at controlled magnitudes in an agentic rather than a retrieval setting.

Its second finding is the more consequential one for practice, because it makes scaffold choice empirically visible. If frontier models benefit more from context engineering than open-source ones do, then a benchmark that reports a model's score without stating its scaffold is under-specified — the same argument [[ScholarlyArticle/dont-blame-the-large-language-model]] reaches from the opposite direction by holding the model fixed and varying the harness. Together the two point at the same methodological conclusion: model and harness are not separable variables in agent evaluation.

The stated caveats are those any benchmark of this shape carries. Environment size is one proxy for the many ways context grows in practice; the scaffold's strategy list draws heavily on one vendor's features and SDKs, which shapes which models the harness is best suited to; and the reported figures are the authors' own.
