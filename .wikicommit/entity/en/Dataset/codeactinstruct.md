---
title: "CodeActInstruct"
type: "schema:Dataset"
lang: en
tags: [agents, tool-use]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2402.01030'
    hash: sha256:60e732ce79967b6e7697d9419ce0ee738d7dfe6a06f5d3161e4b2f0eecb66448
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An instruction-tuning dataset of 7k multi-turn interactions using CodeAct, collected by the authors of Executable Code Actions Elicit Better LLM Agents and used to finetune CodeActAgent."
  url: "https://github.com/xingyaoww/code-act"
---

CodeActInstruct is an instruction-tuning dataset consisting of 7k multi-turn interactions using
[[DefinedTerm/codeact]], collected by the authors of
[[ScholarlyArticle/executable-code-actions-elicit-better-llm-agents]].

## Contents

The dataset holds 7k multi-turn interactions, and the paper identifies its action format as
CodeAct: under that format an agent emits executable Python code, an integrated Python interpreter
executes it, and the agent dynamically revises prior actions or emits new ones upon new
observations across multiple turns.

## Provenance

The paper states that its authors collected the dataset, and describes it as consisting of 7k
multi-turn interactions using CodeAct. For the work as a whole, code, data, model and a demo are
stated to be available at <https://github.com/xingyaoww/code-act>.

## Use

The authors used CodeActInstruct to finetune [[SoftwareApplication/codeactagent]] from Llama2 and
Mistral. They report that the dataset can be used together with existing data to improve models on
agent-oriented tasks without compromising their general capability — a claim about combining it with
other data rather than about training on it alone.
