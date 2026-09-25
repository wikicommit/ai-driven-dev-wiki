---
title: "Trace grading"
type: "schema:DefinedTerm"
lang: en
tags: [agent-evaluation, observability]
sources:
  - type: url
    url: 'https://platform.openai.com/docs/guides/agent-evals'
    hash: sha256:f3f1a40cb1a29b25715cb477da00597d7c7821efc4a84971077c37f0713cbf02
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An agent-evaluation practice in which graders score recorded end-to-end traces of an agent's runs — its model calls, tool calls, guardrails and handoffs — against structured criteria, to find workflow-level regressions and failure modes. OpenAI's documentation presents it as the starting point while agent behaviour is still being debugged."
---

Trace grading is the practice of evaluating an agent workflow by scoring its **traces** with
**graders**. In OpenAI's documentation on evaluating agent workflows, a trace is the end-to-end record
of one run — the model calls, tool calls, guardrails and handoffs it involved — and a grader scores such
traces against structured criteria, so that regressions and failure modes can be found at scale. The
documentation calls it the fastest way to identify workflow-level issues, and positions it as the place
to start while an agent's behaviour is still being debugged.

## Usage

The questions trace grading is suggested for are about the workflow rather than a single answer: whether
the agent picked the right tool, whether a handoff happened when it should have, whether the workflow
violated an instruction or safety policy, and whether a prompt or routing change improved end-to-end
behaviour. The workflow OpenAI describes on its platform is to open the traces view in its dashboard,
inspect a representative workflow trace, create a grader and run it against the selected traces, and
use the results to refine prompts, tool surfaces, routing logic or guardrails. For code-first workflows
built with the [[SoftwareApplication/openai-agents-sdk]], it points to the SDK's tracing integration as
the way to get high-signal traces before formalizing graders.

## When It Applies

- **Conditions.** It is recommended while behaviour is still being debugged and the question is what
  is going wrong in individual runs.
- **What it assumes.** Runs must be recorded as traces, and someone must be able to say what a good run
  looks like well enough to write a grader's criteria.
- **Where it stops.** The documentation treats it as a first stage rather than the whole of evaluation:
  once it is clear what "good" looks like, it recommends moving from individual traces to repeatable
  datasets and eval runs, to benchmark changes, compare prompts, or run larger-scale evaluations over
  time.
- **How established.** The source is a single vendor's product documentation describing its own
  platform's evaluation surfaces; it recommends the practice rather than reporting measured results.

## Related Terms

- [[DefinedTerm/trajectory-evaluation]]
- [[DefinedTerm/llm-as-a-judge]]
- [[DefinedTerm/guardrails]]
