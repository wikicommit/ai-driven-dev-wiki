---
title: "Prompt Chaining"
type: "schema:DefinedTerm"
lang: en
tags: [prompt-engineering, agent-design-patterns, workflows]
sources:
  - type: url
    url: 'https://www.anthropic.com/research/building-effective-agents'
    hash: sha256:611504eb30423330be060ed8f00e432a0adcb417f992b2cfb5cbf9ccd8d511bf
  - type: url
    url: 'https://github.com/phodal/build-agent-context-engineering'
    hash: sha256:cac7baf9e9ec7a1bfb8c190343db878dcc207737e772a46a03276d7b4be6094a
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A workflow pattern for LLM applications in which a task is decomposed into a sequence of steps, each handled by its own LLM call or prompt that works on the output of the previous one, with the results combined at the end."
---

Prompt chaining is a pattern for building LLM applications in which a task is broken into a sequence
of subtasks, each handled by its own prompt or model call, with each step working on what the
previous one produced and the results integrated at the end. Anthropic, in
[[BlogPosting/building-effective-agents]], presents it as one of the compositional workflows it has
seen in production agentic systems, and adds that programmatic checks — a "gate" — can be placed on
any intermediate step to keep the process on track. A Chinese-language overview of agent
construction by the developer phodal describes the same idea as a way to decompose complex problems
systematically, and treats it as a companion to [[DefinedTerm/prompt-routing]]: once requests can be
routed, a complex one can be split into a chain.

## Usage

The two accounts stress different benefits. Anthropic frames the pattern as a trade: accepting
higher latency in exchange for accuracy, by making each LLM call an easier task. Its examples are
generating marketing copy and then translating it into another language, and writing a document
outline, checking that it meets certain criteria, and then writing the document from the outline.

phodal's overview frames it as modularity: each subtask concentrates on one stage, any subtask can be
rewritten or have its prompt replaced as needed, and later prompts can be adjusted according to what
an earlier stage produced. Its example is turning a product manager's idea into requirements through
four stages — collecting ideas and initial requirements, sorting out the requirement logic and
feature priorities, drafting a preliminary requirements document or task list, and finalizing the
requirements into a formal document — with each stage able to be handled by a different prompt or
sub-agent, such as a search-capable agent for the first.

## When It Applies

Both sources place it where the steps are known in advance. Anthropic describes it as ideal when a
task can be easily and cleanly decomposed into fixed subtasks; phodal describes it as suited to
processes with a fixed flow in which some steps can be skipped. It assumes that the decomposition is
known before the task starts.
Anthropic's stated cost is latency, since the task is spread across several sequential calls.

The pattern's standing rests on practitioner accounts rather than measurement: Anthropic presents it
as a pattern it observed across teams building agents, and phodal as teaching material drawn from
training developers to build agents.

## Related Terms

- [[DefinedTerm/prompt-routing]] — the companion pattern that sends an input to a specialized path
- [[DefinedTerm/augmented-llm]] — the building block each call in a chain is assumed to be
- [[DefinedTerm/prompt-engineering]] — the discipline phodal's overview places it under
