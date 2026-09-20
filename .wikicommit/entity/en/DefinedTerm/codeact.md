---
title: "CodeAct"
type: "schema:DefinedTerm"
lang: en
tags: [agents, tool-use, agent-architecture, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2402.01030'
    hash: sha256:60e732ce79967b6e7697d9419ce0ee738d7dfe6a06f5d3161e4b2f0eecb66448
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An approach, proposed in the paper Executable Code Actions Elicit Better LLM Agents, in which an LLM agent's actions are consolidated into a single unified action space of executable Python code rather than JSON or text in a pre-defined format."
---

CodeAct is the name
[[ScholarlyArticle/executable-code-actions-elicit-better-llm-agents]] gives to using executable
Python code to consolidate a large language model agent's actions into a unified
[[DefinedTerm/action-space]]. It is proposed against the common arrangement in which an agent is
prompted to produce actions by generating JSON or text in a pre-defined format — an arrangement the
paper describes as limited by a constrained action space, such as the scope of the pre-defined
tools, and by restricted flexibility, such as an inability to compose multiple tools.

## Usage

CodeAct is paired with an integrated Python interpreter. With one in place, the paper states that
CodeAct can execute code actions and dynamically revise prior actions or emit new actions upon new
observations, through multi-turn interactions — so the code is not only the notation for an action
but the thing that runs, and its result feeds the next turn.

## When It Applies

The approach applies to agents that act by calling tools and operating on an environment, and it
assumes two things are available: a Python interpreter the agent's output can be executed by, and a
model able to emit code as its action format. Where those hold, the paper's argument is that one
action space subsumes what a fixed tool schema would have to enumerate, because composing several
tools is ordinary code rather than a capability the format has to provide for.

Its standing is that of a proposal with a reported comparison behind it rather than a settled
convention. The paper reports an analysis of 17 LLMs on API-Bank and a newly curated benchmark in
which CodeAct outperforms widely used alternatives by up to 20% higher success rate, and the same
authors go on to finetune [[SoftwareApplication/codeactagent]] on
[[Dataset/codeactinstruct]], a dataset of 7k multi-turn interactions using CodeAct. The work was
accepted by ICML 2024.

## Related Terms

- [[DefinedTerm/action-space]]
- [[DefinedTerm/tool-use-design-pattern]]
- [[DefinedTerm/code-then-execute-pattern]]
- [[DefinedTerm/code-execution-mcp]]
