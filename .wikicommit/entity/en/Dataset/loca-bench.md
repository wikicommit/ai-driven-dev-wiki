---
title: "LOCA-bench"
type: "schema:Dataset"
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
  description: "An open-source benchmark for LOng-Context Agents that varies the size of the environment an agent must explore while holding task semantics fixed, so context length can be scaled arbitrarily under control. It evaluates models and scaffolds together, making context management strategies a measurable variable rather than a background choice."
  creator: "Weihao Zeng, Yuzhen Huang, and Junxian He (HKUST)"
  datePublished: "2026-02"
  measurementTechnique: "Task success rate as the environment description length is scaled, with the underlying task prompt held constant; scaffold and context-management strategy varied independently"
  sameAs: "https://github.com/hkust-nlp/LOCA-bench"
---

LOCA-bench is a benchmark for **LO**ng-**C**ontext **A**gents introduced in [[ScholarlyArticle/loca-bench]] by researchers at HKUST and released open-source. Its design problem is that existing long-context benchmarks "still fall short of realistic scenarios": most assume a static setting where the model either receives all relevant information upfront or can obtain it with a straightforward retrieval step, reducing the task to locating a few key snippets — a needle in a haystack — or aggregating scattered facts in one step.

The benchmark's argument is that real agentic use is dynamic. An agent "typically begins with limited knowledge about its environment," must decide what to look for, explore during execution, and continually add newly discovered information to its context, so that "the core difficulty is not just finding the right evidence once, but remaining organized and reliable at every action as the context grows over time."

## Composition

Tasks are drawn from real-world scenarios in which models must actively explore an environment through tools grounded in real-world sources. The control mechanism is the distinguishing design choice: rather than varying the prompt, the benchmark varies the **environment description length** — the amount of information in the initial environment state, such as the size of an Excel sheet, a PDF file, or a database — while holding the underlying task prompt and semantics fixed. Because the environment is generated from a configuration, context length can be extended "potentially to infinity in a controlled way."

Four challenges are designed to emerge as that context grows, and they are what the benchmark measures beyond retrieval: **complex retrieval and reasoning**, where multiple pieces of relevant information must be retrieved from tool outputs and reasoned over jointly; **instruction following**, since tasks carry multiple constraints that must all be satisfied and "agents frequently forget earlier instructions"; **environment exploration**, where the authors report agents tending to explore less and behave more conservatively as context grows; and **hallucination**, where models under longer contexts are reported "often subtly altering factual details during generation."

The benchmark deliberately treats a language agent as a *combination of model and scaffold* rather than as a model alone, and decouples environment, tools, tasks, and scaffold so that context engineering strategies can be evaluated across setups — including the Claude SDK and the Claude Code/Agent SDK. The strategies integrated into the evaluation scaffold include context editing methods such as removing stale tool calls and results, stripping thinking content, and compacting conversation history, alongside context awareness, memory tools, and programmatic tool calling.

## Use in Evaluation

The headline pattern is a sharp degradation curve rather than a ranking. Most models perform strongly when the context is short, typically above 70% accuracy; as context grows, "performance drops sharply even though the underlying task does not change," and the gap between frontier and open-source models becomes increasingly pronounced. Because task semantics are held fixed by construction, the drop is attributable to context growth rather than to task difficulty — which is what the benchmark exists to establish.

Its second result concerns the scaffold. Context engineering strategies are reported to substantially improve performance, but unevenly: "models differ in how efficiently they apply these strategies, with frontier models generally benefiting more than open source models." Programmatic tool calling is singled out as substantially reducing the intermediate cost of exploration while improving tool orchestration, leading to more reliable behaviour and more precise control flow.

The obvious caution is that the environment-size axis is a proxy for the many ways real context grows, and that a benchmark whose scaffold includes one vendor's context-management features will measure those features' effect on that vendor's models most directly. The reported figures are the authors' own.
