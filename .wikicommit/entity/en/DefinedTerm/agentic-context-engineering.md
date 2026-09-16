---
title: "Agentic Context Engineering"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agents-md/'
    hash: sha256:ee43d2eb32e588d7c7bbadd7d7913c23bca92a53f6a8f01113bcb23e8b12d029
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A framework (ACE, ICLR 2026) that treats an AI agent's context as an evolving playbook maintained through a generator/reflector/curator pipeline, rather than as a static instruction file."
---

Agentic Context Engineering (ACE) is a framework, cited to ICLR 2026, that treats an AI agent's context as an evolving playbook rather than a static file such as `AGENTS.md`. It maintains that playbook through a generator/reflector/curator pipeline, adapting the content an agent sees as tasks and conditions change, instead of loading the same fixed instruction set for every task.

## Usage

The source cites it as a response to the "static file problem": a fixed file like `AGENTS.md` cannot condition its content on what kind of task is currently running, so an instruction that is useful for one task (e.g. always run the full test suite before committing) can waste effort on an unrelated one (e.g. a documentation-only change). The source reports that on agent benchmarks, ACE outperformed static context approaches by 12.3%.

## When It Applies

It applies where the fixed cost of a single static context file — irrelevant instructions competing for a model's attention on tasks they don't apply to — is significant enough to justify an adaptive pipeline instead. The source presents it as one of several proposals responding to the same static-file limitation, alongside a separately-described three-layer routing architecture, without stating that the two approaches have been directly compared to each other.

## Related Terms

[[DefinedTerm/agents-md]], [[DefinedTerm/context-engineering]]
