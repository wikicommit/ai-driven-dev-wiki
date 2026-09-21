---
title: "4D-ARE"
type: "schema:DefinedTerm"
lang: en
tags: [agents, requirements-engineering, spec-driven-development]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2601.04556'
    hash: sha256:47686611cd9c576575a542851a7df72a328d486ff7ae3ce584ed719df20ad9f9
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "4-Dimensional Attribution-Driven Agent Requirements Engineering: a proposed design-time methodology for specifying what an LLM decision-support agent should reason about, organizing domain knowledge into four causally ordered dimensions and five specification layers whose artifacts compile into the agent's system prompt."
---

4D-ARE — 4-Dimensional Attribution-Driven Agent Requirements Engineering — is a methodology for specifying LLM decision-support agents, proposed in [[ScholarlyArticle/4d-are-bridging-the-attribution-gap]]. It addresses design time rather than runtime: where [[DefinedTerm/react-prompting]] and [[DefinedTerm/chain-of-thought]] govern how an agent reasons during execution, 4D-ARE is a method for deciding what it should reason about in the first place, and for writing that down in a form that reaches the agent. Its organizing claim is that the domain knowledge a decision-support agent needs is attribution logic — how outcomes connect to causes — and that this logic falls into four dimensions.

## Usage

The four dimensions are **Results** (observable outcome metrics), **Process** (controllable actions a decision-maker can manipulate directly), **Support** (configurable resources, changeable within a planning horizon but not immediately) and **Long-term** (environmental context that constrains but cannot be controlled). They are ordered causally — Long-term constrains Support, Support enables Process, Process produces Results — and attribution runs the chain backwards: when Results show a gap, the agent asks which Process failed, then which Support was missing, then which Long-term factor changed.

Two things follow. From the ordering comes a completeness criterion: a response counts as attribution-complete if and only if it addresses every dimension on the backward path from the one queried, on the argument that omitting Process leaves the decision-maker knowing what happened but not what to change, omitting Support leaves them without what enables the change, and omitting Long-term risks attempting changes that are futile given the environment. Separately, from what its proposers call the actionability separation principle, the agent's authority is graduated by dimension: it may interpret and recommend specifically for Process, recommend only open-endedly for Support, and offer neither interpretation nor recommendation for Results or Long-term, where strategic judgment is held to lie outside its scope.

The methodology is operationalized through five layers, each producing artifacts that compile into a component of the system prompt: a **Question Inventory** fixing what the agent perceives, an **Attribution Model** fixing how it traces causality, a **Data Mapping** fixing what data it can reach, **Dual-Track Logic** fixing when it interprets versus recommends, and **Boundary Constraints** fixing what it must not do. The artifacts are written as YAML. The layers are presented as sequential but iterable — data-mapping problems at Layer 3 may expose gaps in the Layer 1 inventory.

Layer 1 is elicited from domain experts using the four dimensions as an interview scaffold, one prompt per dimension: what outcomes do you track to judge success, what operational indicators signal problems, what resources must be in place, what strategic factors affect future performance.

## When It Applies

Its stated scope is LLM agents for decision support in enterprise settings — agents that support a human decision-maker, work in a domain with causal structure, must produce explainable output, and must respect operational boundaries. Its proposers frame it as complementary to runtime reasoning frameworks rather than competing with them, and separately as complementary to process-oriented specification tooling: on their account such tooling organizes how development proceeds, while 4D-ARE supplies what the agent should know about the domain.

Two reported findings from the single pilot bear on adoption, both subject to a caveat the paper states at the head of that section: to protect sensitive business intelligence, its specific metrics and examples are constructed for demonstration purposes while reflecting realistic patterns. Effort is reported as concentrated where it may not be expected — data mapping at 60% of implementation effort against roughly 40% for the four conceptual layers together — which the authors read as the methodology front-loading specification work rather than reducing the total. And boundary constraints are presented as load-bearing rather than decorative: without explicit Layer 5 constraints, pilot testing is reported to have produced agents generating personnel recommendations, unfounded claims and overconfident language, which the authors say disappeared once the constraints were in place.

What is not yet established is whether any of this generalizes. The four-dimensional structure is presented as motivated by Pearl's causal hierarchy and control theory but not derived from them — its proposers call it a useful conceptual organization rather than a mathematical necessity — and the evidence is one agent type in one organization in one domain, with the authors stating their observations are hypotheses for future investigation rather than validated findings.

## Related Terms

[[DefinedTerm/attribution-gap]], [[DefinedTerm/spec-driven-development]], [[DefinedTerm/react-prompting]], [[DefinedTerm/chain-of-thought]], [[DefinedTerm/prompt-engineering]]
