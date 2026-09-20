---
title: "Executable Code Actions Elicit Better LLM Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, tool-use, agent-architecture, llm]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2402.01030'
    hash: sha256:60e732ce79967b6e7697d9419ce0ee738d7dfe6a06f5d3161e4b2f0eecb66448
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The arXiv preprint that proposes CodeAct, consolidating an LLM agent's actions into executable Python code as a unified action space, and reports it outperforming JSON- and text-based alternatives by up to 20% in success rate."
  author: ["Xingyao Wang", "Yangyi Chen", "Lifan Yuan", "Yizhe Zhang", "Yunzhu Li", "Hao Peng", "Heng Ji"]
  datePublished: "2024-02-01"
  abstract: "The paper observes that LLM agents are typically prompted to produce actions as JSON or text in a pre-defined format, which limits them to a constrained action space and restricts their flexibility to compose multiple tools. It proposes CodeAct, which consolidates an agent's actions into a unified action space of executable Python code, run by an integrated Python interpreter so that prior actions can be revised or new ones emitted across multi-turn interactions. An analysis of 17 LLMs on API-Bank and a newly curated benchmark reports CodeAct outperforming widely used alternatives by up to 20% in success rate; the authors then collect CodeActInstruct, a 7k multi-turn instruction-tuning dataset, and finetune CodeActAgent from Llama2 and Mistral."
---

This arXiv preprint addresses how a large language model agent's actions are represented. The
authors observe that LLM agents — capable of a broad range of actions such as invoking tools and
controlling robots — are typically prompted to produce those actions by generating JSON or text in a
pre-defined format. They identify two limits in that arrangement: a constrained action space, for
example the scope of the pre-defined tools, and restricted flexibility, for example an inability to
compose multiple tools.

The paper's proposal is [[DefinedTerm/codeact]]: use executable Python code to consolidate an LLM
agent's actions into a unified action space. Integrated with a Python interpreter, CodeAct can
execute code actions and dynamically revise prior actions or emit new actions upon new observations,
through multi-turn interactions.

The authors report an extensive analysis of 17 LLMs on API-Bank and a newly curated benchmark, in
which CodeAct outperforms widely used alternatives by up to 20% higher success rate. That result is
given as the motivation for building an open-source LLM agent that interacts with environments by
executing interpretable code and collaborates with users using natural language. To that end the
authors collect [[Dataset/codeactinstruct]], an instruction-tuning dataset of 7k multi-turn
interactions using CodeAct, and report that it can be used alongside existing data to improve models
on agent-oriented tasks without compromising their general capability. The resulting agent,
[[SoftwareApplication/codeactagent]], is finetuned from Llama2 and Mistral.

The paper is filed under Computation and Language (cs.CL) and Artificial Intelligence (cs.AI). It
was first submitted on 1 February 2024 and last revised on 7 June 2024 as version 4, carries the
arXiv-issued DOI 10.48550/arXiv.2402.01030, and was accepted by ICML 2024. Code, data, model and a
demo are stated to be available at <https://github.com/xingyaoww/code-act>.

## Key Points

- The paper's stated problem is that LLM agents are usually prompted to emit actions as JSON or text in a pre-defined format, which constrains the action space and restricts flexibility such as composing multiple tools.
- CodeAct is proposed as the alternative: executable Python code consolidating the agent's actions into one unified action space.
- Because a Python interpreter is integrated, CodeAct can execute code actions and dynamically revise prior actions or emit new ones upon new observations, across multi-turn interactions.
- The reported evaluation covers 17 LLMs on API-Bank and a newly curated benchmark, with CodeAct outperforming widely used alternatives by up to 20% higher success rate — "up to" being the paper's own qualifier on the figure.
- The authors collect CodeActInstruct, 7k multi-turn interactions using CodeAct, and report that adding it to existing data improves models on agent-oriented tasks without compromising their general capability.
- CodeActAgent, finetuned from Llama2 and Mistral, is presented as the open-source agent the analysis motivated, integrated with a Python interpreter and tailored to perform sophisticated tasks such as model training using existing libraries, and to self-debug autonomously.

## Notes

The paper's claim has two parts that are established differently. The comparison against JSON and
text action formats rests on the 17-model analysis, while the claim that instruction tuning on
CodeActInstruct does not compromise general capability rests on the authors' own fine-tuning
experiments on two base model families. The two benchmarks used are not symmetric either: API-Bank
is an existing one, and the second was curated by the authors for this work.
