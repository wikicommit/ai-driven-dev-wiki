---
title: "Context poisoning"
type: "schema:DefinedTerm"
lang: en
tags: [context-window, llm, agents]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/60229/'
    hash: sha256:10d03ac2a5d00b558656acc685e174052e16d06256b8fd88f86df9be1d954d01
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The production of output that is locally consistent but wrong as a whole because errors or noise are mixed into the information given to an LLM as the premise of a generation task."
---

Context poisoning is the phenomenon in which errors or noise mixed into the information given to a language model as the premise of a generation task cause it to produce output that is logically consistent locally but wrong as a whole. [[BlogPosting/spec-driven-development-context-engineering-custom-slash-commands]] names it as one of three problems that [[DefinedTerm/context-engineering]] is meant to address, alongside [[DefinedTerm/context-rot]] and [[DefinedTerm/context-confusion]]. Its symptoms, in that post's account, are incorrect implementations or documentation, and implementations or explanations that contradict the current specification.

## Usage

The post traces the cause to outdated specifications, comments that were never updated, and similar code unrelated to the task finding its way into the context. Because the model tries to produce an answer consistent with the information it is given, it reproduces an error in its input "in a clean form".

In the post's account of designing [[DefinedTerm/custom-slash-commands]], context poisoning is one of the reasons for making every command write its result to a file: output left only in the console can be used only within that session, which amounts to being unable to reset the context, and carrying an overloaded context forward invites context poisoning and context rot. Passing a file from one command to the next, and clearing the context in between, is presented as the way to cut that carried-over noise.

## Related Terms

- [[DefinedTerm/context-rot]]
- [[DefinedTerm/context-confusion]]
- [[DefinedTerm/context-engineering]]
