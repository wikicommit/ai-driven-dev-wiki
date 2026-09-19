---
title: "AI Agent Guardrails: Rules That LLMs Cannot Bypass"
type: "schema:BlogPosting"
lang: en
tags: [agents, agent-safety, guardrails, tool-use]
sources:
  - type: url
    url: 'https://dev.to/aws/ai-agent-guardrails-rules-that-llms-cannot-bypass-596d'
    hash: sha256:d321340a9dfb2556bc45605cd43311d6f886dd3c139f618c6380e18345aa7a1a
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A post arguing that business rules written into prompts and tool docstrings are suggestions an LLM may ignore, and that enforcing them in a framework-level hook that runs before a tool executes is the only way to make them binding. Part of a series on stopping agent hallucinations."
  author: "Elizabeth Fuentes L"
  publisher: "AWS"
---

The post takes up a failure it calls hallucinated operation success: an agent reports that it completed an operation which in fact violated a business rule. Its worked example is a travel-booking agent asked to confirm a hotel booking, which calls `confirm_booking(booking_id="BK001")` and returns "SUCCESS" even though no payment was verified — the tool's own docstring says payment must be verified first, and the model read it and proceeded anyway.

Its diagnosis is architectural rather than a matter of prompt quality. Prompts are text the model interprets, so a business rule stated in a docstring or a system prompt becomes a suggestion the model re-decides on every call. The remedy it proposes is to move enforcement outside the model: a hook registered with the agent framework evaluates deterministic rules before a tool runs and cancels the call when one fails, so the model receives a cancellation it has no path to override. The post frames this combination as neurosymbolic — neural LLM reasoning paired with deterministic symbolic rules — and credits the framing to research it cites.

The demonstration uses [[SoftwareApplication/strands-agents]] and its `BeforeToolCallEvent` hook, and is built so that the hook is the only variable: two agents with identical tools, model and prompts, differing by a single `hooks=[hook]` argument. The post notes that comparable interception exists in other agent frameworks, naming LangGraph node guards and AutoGen reply functions.

## Key Points

- An agent can report success for an operation that violated a business rule, and the baseline agent in the demo has no mechanism to detect that it did so — it returns success with full confidence.
- Business rules placed in docstrings or system prompts are context the model interprets, not constraints; the model decides whether to follow them on each call.
- The post names three hallucination patterns it says prompt engineering cannot prevent: parameter errors (calling a tool with a value the docstring forbids), completeness errors (executing without a required prerequisite step), and tool bypass behaviour (claiming success without calling a mandatory validation tool).
- Enforcement placed in a pre-execution hook is not overridable by the model, because the hook runs outside it — the post's stated contrast is that prompts are input to the LLM while hooks are framework-level interceptors.
- Cancelling before execution means there is no completed operation to roll back and no compensating transaction is needed.
- Rules written as plain functions are testable and auditable independently of any agent or model call, and one hook can validate every tool rather than scattering validation across tool definitions.
- The post lists limits of the approach in its own voice: each protected operation needs a rule written for it, the rules are boolean and do not express fuzzy or probabilistic logic, edge cases need explicit handling, and the rules need maintenance as business logic changes.
- Its headline result is stated as "3/3 invalid operations blocked" with zero false positives and zero false negatives. Its worked scenarios are three in number but comprise two invalid cases — a confirmation without payment, and a booking exceeding the guest limit — and one valid booking, which both agents execute; the hooked agent blocks both invalid cases and adds no friction to the valid one.

## Context

The post presents itself as Part 3 of a series on agent hallucinations, published under the AWS organization on DEV Community and originally on the AWS builder site. Its recommendation is scoped rather than general: it advises defining hooks for critical, high-stakes operations such as bookings, payments and cancellations, and logging every rule violation with the tool name, parameters and reason for auditing. The demonstration and the recommendation come from the same author, on a purpose-built example rather than a production workload, so the reported outcome reads as a worked illustration of the pattern rather than independent evidence for it.
