---
title: "Structured Query"
type: "schema:DefinedTerm"
lang: en
tags: [llm, security, prompt-injection, agent-safety]
sources:
  - type: url
    url: 'https://www.usenix.org/system/files/usenixsecurity25-chen-sizhe.pdf'
    hash: sha256:91f97972f9337ec68915889ea729157686ff67d4a51b175b55127f2e715de659
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An input to an LLM consisting of two separate parts, a prompt and data, proposed as a safe-by-design replacement for the single concatenated string that makes prompt injection possible."
---

A structured query is an input to an LLM that consists of two separate parts, a prompt (the
instruction) and the data, rather than a single string containing both. It is proposed in
[[ScholarlyArticle/struq]] as a general approach to prompt injection: on that argument, existing
LLMs expose an unsafe-by-design API in which the application developer is expected to concatenate
prompt and data and send them to the model as one combined input, and the natural fix is to change
the API so the control part is presented separately from the data part. An LLM trained to follow
instructions found only in the prompt part, and never in the data input, would be immune to prompt
injection, because the user can only influence the channel the model has been taught not to seek
instructions in.

## Usage

The paper reaches the idea by analogy rather than from first principles about language models. It
treats [[DefinedTerm/prompt-injection]] as the latest instance of the classic injection pattern,
in which control and data are sent over the same channel and maliciously constructed data can spoof
commands: the 2600 Hz tone that phone phreakers played into a handset over the same voice channel
the switch listened on, SQL injection arising because the database API accepts one string mixing
the command type with the values to match on, cross-site scripting arising because an HTML page is
one string mixing markup with page content, and command injection arising because a Unix shell
executes a single string mixing the program name and separators with the arguments. In each case
the paper's reading is that the most robust solution has been to stop mixing them, its named
example being SQL prepared statements, which change an unsafe-by-design API into a safe-by-design
one by taking the query template as one argument and the parameters as another.

Three research challenges are stated for building a system that supports structured queries:
security, meaning the system must not under any conditions execute instructions found in the data
part; utility, meaning it must stay close to existing LLMs in capability; and feasible training,
since training a state-of-the-art LLM from scratch costs millions of dollars and so a way must be
found to build on existing LLM technology. StruQ is the paper's answer to the third — a front-end
plus [[DefinedTerm/structured-instruction-tuning]] applied to an existing base model — and the
paper frames it as a first step towards the vision rather than its completion, inviting other
researchers to find a more robust implementation.

## When It Applies

The approach applies to programmatic LLM-integrated applications, where a developer invokes a model
through an API or library and may be willing to use one that takes the prompt and the data
separately. The paper states it is not applicable to web-based chatbots offering multi-turn,
open-ended conversation, on the reasoning that end users are unlikely to be happy marking which
parts of their contributions are instructions and which are data. It is a defense against prompt
injection specifically, and the paper says it is not designed to defend against jailbreaks, data
extraction or other attacks on LLMs. Its evidence is one implementation, evaluated by its own
authors on two 7B open-source models, and the paper's own conclusion is that structured queries are
a promising direction rather than a settled one.

## Related Terms

[[DefinedTerm/prompt-injection]], [[DefinedTerm/control-data-plane-confusion]],
[[DefinedTerm/structured-instruction-tuning]], [[DefinedTerm/completion-attack]]
