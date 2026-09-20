---
title: "CodeActAgent"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, open-source]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2402.01030'
    hash: sha256:60e732ce79967b6e7697d9419ce0ee738d7dfe6a06f5d3161e4b2f0eecb66448
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An open-source LLM agent finetuned from Llama2 and Mistral that acts by emitting executable Python code, integrated with a Python interpreter and tailored to perform sophisticated tasks using existing libraries and to self-debug autonomously."
  applicationCategory: "LLM coding agent"
  featureList: "Acts by emitting executable Python code; integrated with a Python interpreter; performs sophisticated tasks such as model training using existing libraries; autonomously self-debugs; collaborates with users in natural language"
---

CodeActAgent is the open-source LLM agent built by the authors of
[[ScholarlyArticle/executable-code-actions-elicit-better-llm-agents]] to put
[[DefinedTerm/codeact]] into practice. Where CodeAct is the approach — consolidating an agent's
actions into a unified action space of executable Python code — CodeActAgent is the model they
finetuned to work that way, starting from Llama2 and Mistral.

The paper frames it as following from its own analysis: the reported performance of CodeAct over
widely used JSON- and text-based action formats is what motivated the authors to build an
open-source LLM agent that interacts with environments by executing interpretable code and
collaborates with users using natural language.

## Capabilities

CodeActAgent is integrated with a Python interpreter, which is what lets its code actions actually
run rather than only be emitted. The paper describes it as uniquely tailored to perform
sophisticated tasks — model training is the example given — using existing libraries, and as able to
autonomously self-debug. Alongside acting, it collaborates with users using natural language.

## Adoption & Ecosystem

The agent was finetuned on [[Dataset/codeactinstruct]], a dataset of 7k multi-turn interactions
using CodeAct that the same authors collected. They report that this data can be used with existing
data to improve models on agent-oriented tasks without compromising their general capability. Code,
data, model and a demo are stated to be available at <https://github.com/xingyaoww/code-act>.
