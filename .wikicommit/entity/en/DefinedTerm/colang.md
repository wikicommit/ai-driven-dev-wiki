---
title: "Colang"
type: "schema:DefinedTerm"
lang: en
tags: [agent-safety, guardrails, dialogue-modeling]
sources:
  - type: url
    url: 'https://github.com/NVIDIA-NeMo/Guardrails'
    hash: sha256:5e355c13851c1bcdbfecb01c03581fb7ca7d93a287620f15481e621963cc9832
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A modeling language introduced by NVIDIA NeMo Guardrails for designing flexible but controllable dialogue flows. It has a Python-like syntax in which user intents, bot responses and the flows connecting them are declared by example, and is the language the toolkit's dialog rails are written in."
---

Colang is a modeling language created specifically for designing flexible, yet controllable,
dialogue flows. It is introduced by [[SoftwareApplication/nemo-guardrails]] as the means of
configuring and implementing that toolkit's various types of guardrail, and its README describes the
syntax as Python-like and as designed to be simple and intuitive, especially for developers.
Definitions live in `.co` files inside a guardrails configuration folder, where they supply the
dialog rails in particular.

Two versions are supported, 1.0 and 2.0, with 1.0 the default.

## Usage

The language's units are declared rather than programmed. A `define user` block names an intent and
lists example utterances that express it — a greeting block giving "Hello!" and "Good afternoon!" —
so that the intent is specified by example rather than by pattern. A `define bot` block names a
response and gives its wording. A `define flow` block then connects them, listing the sequence: a
user expressing a greeting, followed by the bot expressing a greeting and offering to help.

The same three constructs express a constraint as readily as a courtesy. The README's second example
defines a user intent for expressing an insult, with "You are stupid" as its example utterance, and a
flow pairing it with a bot response expressing calm willingness to help — a dialog rail that fixes
the reply to a class of input rather than leaving it to the model.

The canonical-form messages these definitions produce are what the toolkit's dialog rails operate
on when deciding whether an action should execute, whether the model should be invoked for the next
step, or whether a predefined response should be used instead.

## Related Terms

- [[SoftwareApplication/nemo-guardrails]] — the toolkit that introduces and uses the language
- [[DefinedTerm/guardrails]] — the broader family of controls this language expresses one kind of
- [[DefinedTerm/prompt-engineering]] — the alternative approach of stating such constraints in prose
  within the prompt itself
