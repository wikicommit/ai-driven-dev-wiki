---
title: "The New Skill in AI is Not Prompting, It's Context Engineering"
type: "schema:BlogPosting"
lang: en
tags: [context-engineering, agents, prompt-engineering]
sources:
  - type: url
    url: 'https://www.philschmid.de/context-engineering'
    hash: sha256:60c94b352e94f9439ea264fbbd3685d4eaac9584b49ebb35c7d352f265d954ed
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A June 2025 blog post by Philipp Schmid arguing that the conversation is shifting from prompt engineering to context engineering, which it defines as the discipline of designing and building dynamic systems that provide an LLM with the right information and tools, in the right format, at the right time."
  author: ["Philipp Schmid"]
  datePublished: "2025-06-30"
---

In this short post on his blog, Philipp Schmid argues that [[DefinedTerm/context-engineering]]
is a term gaining traction and that the conversation in the AI world is shifting from
[[DefinedTerm/prompt-engineering]] to this broader concept. He opens with Tobi Lutke's description of it
as "the art of providing all the context for the task to be plausibly solvable by the LLM", and states
that with the rise of agents, the quality of the context given to an agent is the main thing that
determines whether it succeeds or fails — most agent failures, in his words, are no longer model
failures but context failures.

The post first widens the meaning of "context" to everything the model sees before it generates a
response, then illustrates why it matters with a worked example, and ends with its own definition:
context engineering is "the discipline of designing and building dynamic systems that provides the
right information and tools, in the right format, at the right time, to give a LLM everything it needs
to accomplish a task."

## Key Points

- Context is not just the single prompt sent to an LLM but everything the model sees before responding.
  The post lists seven parts: instructions or system prompt, the user prompt, state or history
  (short-term memory), long-term memory, retrieved information (RAG), available tools, and structured
  output definitions.
- The difference between a "cheap demo" agent and a "magical" one lies in the quality of the context,
  not in the code or framework. The post's example is a scheduling request: an agent that sees only the
  email replies robotically, while one given the user's calendar, past emails with the sender, contact
  list and invite-sending tools can decline tomorrow, propose another slot and send an invite.
- In that framing the code's primary job is to gather the information the LLM needs before calling it,
  rather than to work out how to respond.
- Context engineering is described as a system rather than a string — the output of a system that runs
  before the main LLM call — and as dynamic, created on the fly for the immediate task.
- Its core job is to make sure the model is not missing crucial details ("Garbage In, Garbage Out"),
  supplying both knowledge and tools only when they are required and helpful.
- Format matters: the post states that a concise summary is better than a raw data dump and a clear
  tool schema better than a vague instruction.
- The post concludes that building reliable agents is becoming less about a magic prompt or model
  updates and more about engineering context, which it calls a cross-functional challenge involving the
  business use case and the definition of outputs.

## Context

The post presents itself as an overview drawn from deep and manual research, and its
acknowledgements credit several earlier tweets and blog posts on the topic as sources of inspiration.
It reports no measurements; the case for the
practice rests on the illustrative scheduling example and on the author's assertion that agent
failures are mostly context failures.
