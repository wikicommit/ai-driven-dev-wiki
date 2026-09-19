---
title: "NVIDIA NeMo Guardrails"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-safety, guardrails, security, open-source]
sources:
  - type: url
    url: 'https://github.com/NVIDIA-NeMo/Guardrails'
    hash: sha256:5e355c13851c1bcdbfecb01c03581fb7ca7d93a287620f15481e621963cc9832
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An open-source, Apache-2.0 Python toolkit for adding programmable guardrails between application code and an LLM. It defines five rail types covering input, dialog, retrieval, execution and output, configured through YAML plus a purpose-built modeling language, and is presented as a defence against jailbreaks and prompt injections among other uses."
  applicationCategory: "LLM guardrails toolkit"
  operatingSystem: "Linux, macOS, Windows"
  featureList: "Five rail types (input, dialog, retrieval, execution, output); YAML guardrails configuration; Colang dialogue modeling language; sync and async Python API; guardrails server; optional LangChain integration; built-in guardrails library"
  author: "[[Organization/nvidia]]"
---

NVIDIA NeMo Guardrails is an open-source toolkit for adding *programmable guardrails* to LLM-based
conversational applications. Its README defines rails — the shortened term it uses throughout — as
specific ways of controlling the output of a large language model, giving as examples not talking
about politics, responding in a particular way to specific user requests, following a predefined
dialog path, using a particular language style, and extracting structured data. The library is
distributed on PyPI as `nemoguardrails`, licensed under Apache 2.0, and requires Python 3.10 through
3.13.

Its position in an application is architectural: the toolkit enables developers to add programmable
guardrails *between the application code and the LLM*, rather than inside the prompt. The README
states three key benefits — building trustworthy, safe and secure LLM applications by defining the
behavior permitted on specific topics; connecting models, chains and other services securely; and
controllable dialog, steering the model along pre-defined conversational paths to enforce standard
operating procedures such as authentication or support flows. It names four use-case shapes:
retrieval-augmented question answering with fact-checking and output moderation, domain-specific
assistants, custom LLM endpoints, and an optional integration wrapping LangChain chains.

## Capabilities

Five types of rail are documented, distinguished by where in the request they apply. **Input rails**
apply to user input and can reject it outright, stopping further processing, or alter it — masking
sensitive data or rephrasing. **Dialog rails** influence how the model is prompted, operating on
canonical-form messages to determine whether an action should execute, whether the model should be
invoked for the next step or a response, or whether a predefined response should be used instead.
**Retrieval rails** apply to retrieved chunks in a RAG scenario and can reject or alter a chunk
before it reaches the prompt. **Execution rails** apply to the input and output of custom actions,
the toolkit's term for tools. **Output rails** apply to generated output and can reject it before it
reaches the user, or alter it to remove sensitive data.

A guardrails configuration is a folder combining a `config.yml` naming the models and active rails,
an optional `config.py` for custom initialization, an `actions.py` for custom Python actions, and
`.co` files holding definitions in [[DefinedTerm/colang]]. The README notes that a configuration
with no rails configured essentially forwards requests to the model. Its example `config.yml` lists
input flows for jailbreak checking and sensitive-data masking and output flows for fact and
hallucination self-checks and moderation, together with a block configuring which entity types are
masked on input.

Using the toolkit from Python is described as requiring only minimal changes: load a configuration
into a `RailsConfig`, create an `LLMRails` instance, and call `generate` in place of the model, with
an input and output format similar to OpenAI's chat completions API. The library is described as
async-first, its core mechanics built on Python's async model, with sync and async variants of the
public methods. A guardrails server is offered as an alternative to the Python API.

## Adoption & Ecosystem

The README presents protection against common LLM vulnerabilities — naming jailbreaks and
[[DefinedTerm/prompt-injection]] — as one of the toolkit's purposes, and reports a vulnerability
scan comparing guardrail configurations against a bundled example bot, pointing to its own
documentation for the results and methodology. It states that the toolkit works with multiple model
providers and ships a library of built-in guardrails.

The project is documented at NVIDIA's own documentation site, and its README points to a paper
introducing the library and giving a technical overview and evaluation. Because that paper is known
here only through the README's reference to it, its own title, authorship and findings are not
restated as established facts. Development happens on a `develop` branch tracking the latest work,
with releases tagged separately.
