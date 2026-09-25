---
title: "12 Factor Agents"
type: "schema:BlogPosting"
lang: en
tags: [agent-architecture, context-engineering, llm-agents]
sources:
  - type: url
    url: 'https://www.humanlayer.dev/blog/12-factor-agents'
    hash: sha256:6feff37ebfec7b730750b8225051221bdd60d67033fc5bc7e515f108314d5576
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A HumanLayer post, based on the original 12 Factor Agents write-up on GitHub and modelled on 12 Factor Apps, that proposes twelve principles for building LLM-powered software good enough to put in front of production customers."
  author: ["Dex"]
  datePublished: "2025-04-03"
  publisher: "HumanLayer"
---

This post sets out to answer one question: what principles can be used to build LLM-powered software
that is good enough to put in the hands of production customers? It is based on the original 12 Factor
Agents write-up on GitHub and styled after 12 Factor Apps. The author reports having tried many agent
frameworks and finding that most products billed as "AI agents" are not very agentic — mostly
deterministic code with LLM steps placed at the right points — and that the founders he talked to
building customer-facing agents mostly roll their own stack rather than using a framework.

Its argument against the plain "prompt, bag of tools, loop until the goal is reached" pattern is that
agents get lost once the context window grows long, repeating the same broken approach. The post
posits that even as models support longer context windows, a small, focused prompt and context will
always give better results, and that what works in practice is "micro agents": the agent pattern used
for well-scoped tasks inside a broader, mostly deterministic workflow. Its worked example is a
deployment bot that HumanLayer runs, where deterministic code handles staging and tests and hands a
small agent the production deployment, with a human approving each deploy call.

## Key Points

- An agent is described as four parts: a prompt that makes the LLM output a JSON description of the
  next step, a switch statement that decides what to do with that JSON, accumulated context of what has
  happened so far, and a loop that repeats until the LLM emits a terminal step.
- Factor 1, natural language to tool calls: convert a request into a structured object that
  deterministic code then executes.
- Factor 2, own your prompts: treat prompts as first-class code rather than relying on a framework's
  black-box prompt construction, for control, testing and evals, iteration and transparency.
- Factor 3, own your context window: the input to the LLM at any point is "here's what's happened so
  far, what's the next step", and the post argues for custom, token- and attention-efficient context
  formats (for example, the whole history packed into one user message as XML-style events) instead of
  the standard message format. It states that "everything is context engineering", and notes that the
  term context engineering became popular about two months after 12-factor agents was published.
- Factor 4, tools are just structured outputs: a tool call is JSON that triggers deterministic code, and
  the code does not have to execute a fixed corresponding function each time.
- Factor 5, unify execution state and business state: where possible, infer execution state (current
  step, waiting status, retries) from the context window rather than tracking it separately.
- Factor 6, launch/pause/resume with simple APIs: agents should be easy to start, pause for long-running
  operations, and resume from external triggers such as webhooks.
- Factor 7, contact humans with tool calls: have the LLM always output JSON and express intents such as
  asking a human for input as structured calls, which the post links to "outer loop" agents started by
  events or crons rather than by a person (see [[DefinedTerm/outer-loop]]).
- Factor 8, own your control flow: build control structures that can break out of the loop to wait for a
  human or a long-running task — the author's top request of every framework is the ability to interrupt
  between tool selection and tool invocation so a call can be reviewed before it runs.
- Factor 9, compact errors into the context window: feed errors back so the model can self-correct, with
  a limit (around three consecutive attempts in the example) before escalating.
- Factor 10, small, focused agents: keep each agent to roughly 3-10, maybe 20 steps so its context stays
  manageable, and expand scope only as models become reliable over longer contexts.
- Factor 11, trigger from anywhere: let users start agents from Slack, email, SMS or other channels and
  have agents reply through the same channels — which the post openly calls the HumanLayer pitch.
- Factor 12, make your agent a stateless reducer: presented by the author as "mostly just for fun".

## Context

The post is written from the author's own experience building agents and talking to founders, not from
a measured comparison, and its recurring caveat is that the author does not know the best prompt or
context format, only that builders need the flexibility to try everything. It is openly partly a
product pitch for HumanLayer. Related pages in this wiki include [[DefinedTerm/context-engineering]],
[[DefinedTerm/function-calling]], [[DefinedTerm/human-in-the-loop]] and, from the same publisher,
[[BlogPosting/advanced-context-engineering-for-coding-agents]].
