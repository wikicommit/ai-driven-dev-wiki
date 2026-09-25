---
title: "The rise of \"context engineering\""
type: "schema:BlogPosting"
lang: en
tags: [context-engineering, agents, prompting]
sources:
  - type: url
    url: 'https://blog.langchain.com/the-rise-of-context-engineering/'
    hash: sha256:32b2b5652177ec8f3a2a23644d8fd7ad0c33e762e6609a596dd0ebbf90f2d682
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A June 2025 LangChain blog post by Harrison Chase that defines context engineering as building dynamic systems to provide the right information and tools in the right format so that an LLM can plausibly accomplish the task, and argues that most agent failures are context failures rather than model failures."
  author: ["Harrison Chase"]
  datePublished: "2025-06-23"
  publisher: "LangChain"
---

In this post on LangChain's blog, Harrison Chase offers a definition of
[[DefinedTerm/context-engineering]]: "building dynamic systems to provide the right information and tools
in the right format such that the LLM can plausibly accomplish the task." He presents it as the
definition he likes, building on recent takes from Tobi Lutke, Ankur Goyal and Walden Yan, and argues that
as LLM applications evolve from single prompts into more complex, dynamic agentic systems, context
engineering is becoming the most important skill an AI engineer can develop — a claim the post links to
Cognition rather than making on its own evidence.

The post's central argument is that when an agent performs unreliably, the usual cause is that the
appropriate context, instructions and tools were not communicated to the model. It breaks the definition
into parts, contrasts context engineering with [[DefinedTerm/prompt-engineering]], lists basic examples,
and closes by describing how LangChain's [[SoftwareApplication/langgraph]] and LangSmith support the
practice. It ends by saying context engineering is not a new idea — agent builders have been doing it for
a year or two — but a new term that aptly describes an increasingly important skill.

## Key Points

- Context engineering is described as a **system**, because complex agents draw context from many
  sources — the developer, the user, previous interactions, tool calls and external data — and as a
  **dynamic** one, because much of that context arrives at run time, so the logic that builds the final
  prompt must be dynamic rather than a static prompt.
- The system must supply the right **information** (models cannot read minds; "garbage in, garbage out"),
  the right **tools** to look things up or take actions when the inputs alone are not enough, and both
  in the right **format** — the post's example is that a short, descriptive error message goes further
  than a large JSON blob, and that tool input parameters matter too.
- Asking whether the model could "plausibly accomplish the task" is presented as a way to separate
  failure modes: a model lacking the right information or tools is fixed differently from one that had
  everything it needed and still failed.
- From first principles, the post says a model errs either because it is not good enough or because it
  was not given the appropriate context, and that more often than not — especially as models improve —
  the second is the cause, whether because context is missing or poorly formatted.
- Prompt engineering is argued to be a subset of context engineering: how context is assembled into the
  prompt still matters, but the task is to format a set of dynamic data rather than to phrase a prompt
  for a single fixed input. Clear behavioural instructions are said to be a bit of both.
- Basic examples given are tool use with LLM-digestible outputs, short-term memory via conversation
  summaries, long-term memory of user preferences, clearly enumerated behavioural instructions in the
  prompt, and retrieval that inserts fetched information before calling the model.
- On LangChain's own products, the post argues that LangGraph's emphasis on control — deciding which steps
  run and exactly what goes into the LLM — enables context engineering, whereas agent abstractions in
  other frameworks can restrict it; and that LangSmith tracing, which shows each step and the exact
  inputs and outputs of LLM calls, helps debug whether the model received the information and tools it
  needed. These are the author's claims about his company's products.

## Context

The post frames itself as naming an existing practice rather than introducing a new one, and it credits
others' recent statements for the definition it adopts. It recommends Dex Horthy's "12 Factor Agents" as
closely related reading and connects the topic to an earlier post of the author's arguing that
communicating with the LLM is hard and often the root cause of agent errors. It is written on LangChain's own blog,
and its product sections are vendor guidance.
