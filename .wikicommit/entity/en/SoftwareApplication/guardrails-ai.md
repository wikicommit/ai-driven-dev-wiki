---
title: "Guardrails AI"
type: "schema:SoftwareApplication"
lang: en
tags: [guardrails, llm, validation]
sources:
  - type: url
    url: 'https://github.com/guardrails-ai/guardrails'
    hash: sha256:c84fe48b906a6637f0bbbd8d2a408cc257b2cd2a1db7c25fd3aea2a74e01b319
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A Python framework that wraps LLM calls in Input and Output Guards built from reusable validators, and that can force an LLM's output into a declared structured shape."
  applicationCategory: "LLM guardrail framework"
  featureList: "Input/Output Guards composed from validators; Guardrails Hub validator collection; Pydantic-based structured output generation; standalone Flask-served Guardrails Server with a REST API"
---

Guardrails AI is a Python framework for building what it calls reliable AI applications, and its
README states its purpose as two functions rather than one. The first is running **Input and Output
Guards** inside an application: measures that detect, quantify and mitigate specific types of risk
in what goes into and comes out of a model. The second is **generating structured data from LLMs** —
constraining a model's output to a shape the application declared in advance.

It is installed as `guardrails-ai` from PyPI and is Apache-2.0 licensed. It is one concrete
implementation of the broader idea covered under [[DefinedTerm/guardrails]].

## Capabilities

A **validator** is the unit of measurement — a pre-built check for one specific kind of risk.
Validators are combined into a `Guard`, which intercepts an LLM's inputs and outputs; the README's
worked examples build a Guard from a regex match, and another from a competitor check and a toxic
language check together, each configured with an `on_fail` action such as raising an exception.
**Guardrails Hub** is the collection those validators are drawn from, documented at
guardrailsai.com/hub, and a `guardrails` CLI configures the project and creates guard
configurations.

For structured output, a Guard is built from a Pydantic `BaseModel` describing the shape wanted —
`Guard.for_pydantic(output_class=..., prompt=...)` — and the framework then obtains that shape by
one of two routes depending on the model: function calling where the LLM supports it, and otherwise
prompt optimization, appending the expected output schema to the prompt so the model can produce
structured data itself.

Guardrails can also run as a **standalone service** rather than a library: `guardrails start`
serves it with Flask behind a REST API, which the project presents as simplifying development and
deployment of Guardrails-powered applications.

## Adoption & Ecosystem

The project's own news entries in the repository record two changes worth noting for anyone reading
older material about it. In February 2025 it launched **Guardrails Index**, which it describes as
the first benchmark of its kind comparing the performance and latency of 24 guardrails across six
common categories. In July 2026 it announced that validators are moving to standard PyPI packages
installed directly with `pip` — the README's examples already use that form, `pip install
guardrails-ai-regex-match` rather than a hub URL — and that its hosted remote inferencing is being
discontinued, with a planned cutoff of August 25, 2026.

## Related

[[DefinedTerm/guardrails]], [[SoftwareApplication/nemo-guardrails]]
