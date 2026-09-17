---
title: "Computer Use"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://ai.google.dev/gemini-api/docs/interactions/computer-use'
    hash: sha256:d486d7160af7c8122be4193362027e3fc85461533dae5589ecb0049302b8480e
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "An agent capability in which a model is given screenshots of a computer screen and generates UI actions (mouse clicks, keystrokes, scrolls) that a client executes on its behalf to operate a browser, mobile app, or desktop environment."
---

Computer use is an agent capability in which a model receives screenshots of a computer screen and responds with specific UI actions — mouse clicks, keystrokes, scrolling, drag-and-drop — that a client-side handler executes on the model's behalf. Google's Gemini API offers this as a `computer_use` tool, similar to function calling, that targets a browser, mobile, or desktop environment; the caller must implement the client-side execution environment that receives and carries out the actions.

## Usage

Building an agent around a computer-use tool means running a continuous loop: the application sends the model a screenshot together with the task prompt and any prior context, the model returns a UI action (in Gemini's Gemini 3.x models, each action carries an `intent` string explaining the model's reasoning for choosing it), the client scales the model's normalized coordinates to the real screen and executes the action with a browser- or OS-automation library, and the client then captures a fresh screenshot and sends it back to continue the loop until the task is complete or terminated. Gemini's implementation supports both a current action vocabulary (`click`, `type`, `scroll`, `navigate`, and others, varying by browser/mobile/desktop environment) and a legacy one (`click_at`, `type_text_at`, `scroll_at`) for older models, and lets a caller exclude default predefined actions and register custom ones instead — for example, a `yield_to_user` function that hands control back to a human for cases the model judges unsafe or ambiguous.

## When It Applies

Because a computer-use agent can take real actions inside a real screen environment, it is treated as a higher-risk capability than an ordinary function-calling tool: Google documents its Gemini implementation as a Preview capability that "may contain errors and security vulnerabilities" and recommends against using it for critical decisions, sensitive data, or actions where serious errors cannot be corrected, and its safety guidance notes that a model acting on a user's behalf might encounter untrusted content on screen or make execution errors. Recommended mitigations include running the agent in a sandboxed VM, container, or a dedicated browser profile with limited permissions rather than directly on a host system; requiring human confirmation before consequential actions (Gemini's implementation can return a `safety_decision` marking an action `require_confirmation` or blocking it outright, covering built-in categories such as financial transactions, sensitive-data modification, account creation, and accepting legal agreements); sanitizing user-supplied text before it reaches the prompt; using allowlists/blocklists to control where the agent can navigate; and logging prompts, screenshots, and executed actions for later audit. Because a screenshot handed to the model could itself carry hidden adversarial instructions, Gemini 3.5 Flash and later models offer an opt-in scan of the screenshot for such content before acting on it.

## Related Terms

[[DefinedTerm/sandboxing]], [[DefinedTerm/agent-hooks]]
