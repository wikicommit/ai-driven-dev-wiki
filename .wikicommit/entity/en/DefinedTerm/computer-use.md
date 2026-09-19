---
title: "Computer Use"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://ai.google.dev/gemini-api/docs/interactions/computer-use'
    hash: sha256:d486d7160af7c8122be4193362027e3fc85461533dae5589ecb0049302b8480e
  - type: url
    url: 'https://platform.openai.com/docs/guides/tools-computer-use'
    hash: sha256:b981146b951cbe05f5084f9bf92ce301183dfed2c810a242adaab76293df9394
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An agent capability in which a model operates a browser, mobile app, or desktop interface on a user's behalf, working from screenshots of the screen and returning either discrete UI actions or code that drives the interface, which a client-supplied environment then executes."
---

Computer use is an agent capability in which a model operates a graphical interface — a browser, a mobile app, or a desktop environment — on a user's behalf, rather than calling a purpose-built API. The model works from screenshots of the screen together with the task prompt and any prior context, and the caller supplies the environment that actually carries out what the model asks for. Vendors differ on what the model returns: it may emit discrete UI actions (mouse clicks, keystrokes, scrolling, drag-and-drop) for a client-side handler to replay, or it may write code that drives the interface through an automation library.

## Usage

Both published implementations are built around a loop, and differ in what crosses the boundary between the model and the environment on each turn.

Google's Gemini API exposes a `computer_use` tool, similar to function calling, that targets a browser, mobile, or desktop environment. The application sends the model a screenshot with the task prompt, the model returns a UI action (in Gemini 3.x models each action carries an `intent` string explaining the model's reasoning for choosing it), the client scales the model's normalized coordinates to the real screen and executes the action with a browser- or OS-automation library, and the client captures a fresh screenshot and sends it back to continue the loop. Gemini's implementation supports both a current action vocabulary (`click`, `type`, `scroll`, `navigate`, and others, varying by environment) and a legacy one (`click_at`, `type_text_at`, `scroll_at`) for older models, and lets a caller exclude default predefined actions and register custom ones instead — for example, a `yield_to_user` function that hands control back to a human for cases the model judges unsafe or ambiguous.

OpenAI's documentation presents two integration styles for the same capability and recommends the first for its GPT-6 Astra model, with the second retained as a supported alternative. Under **code execution**, the model is given an ordinary function tool that accepts a script; the application runs that script in an isolated browser or desktop environment and returns its output, including screenshots. Because the unit of exchange is a script rather than a single gesture, one call can combine several actions, loops, or conditional logic. Under **the computer tool**, the model instead returns structured mouse and keyboard actions that the application translates into browser or desktop input, and the loop continues until the model stops returning `computer_call` items. Either way the environment must stay available between calls so the model can build on earlier work, and OpenAI notes that an application already exposing UI operations through function calling or remote MCP tools can keep that interface instead. OpenAI publishes a CUA sample app with JavaScript/Playwright and Python/PyAutoGUI implementations.

## When It Applies

Because a computer-use agent takes real actions inside a real screen environment, both vendors treat it as higher-risk than an ordinary function-calling tool, and their guidance converges on four controls.

*Restrict the environment.* Google recommends a sandboxed VM, container, or dedicated browser profile with limited permissions rather than a host system, plus allowlists and blocklists governing where the agent can navigate; OpenAI asks for an isolated browser or VM and an allow list of sites and actions, keeping access limited to what the task needs.

*Treat what is on screen as untrusted.* OpenAI states the principle directly: text in a page, document, or tool result cannot grant permission or override the user's instructions. Google's safety guidance makes the same point from the threat side — a model acting on a user's behalf may encounter untrusted content on screen — and Gemini 3.5 Flash and later models offer an opt-in scan of the screenshot for hidden adversarial instructions before acting on it. This is the screen-borne form of [[DefinedTerm/indirect-prompt-injection]].

*Confirm consequential actions.* Gemini's implementation can return a `safety_decision` marking an action `require_confirmation` or blocking it outright, covering built-in categories such as financial transactions, sensitive-data modification, account creation, and accepting legal agreements. OpenAI asks that users stay in control of purchases, data transmission, and destructive or hard-to-reverse changes, and counts typing sensitive information into a form as transmission.

*Bound and verify the run.* OpenAI recommends step, time, or cost limits, support for cancellation, and checking the actual outcome in the application rather than relying on the model's final answer. Google's parallel recommendations are sanitizing user-supplied text before it reaches the prompt and logging prompts, screenshots, and executed actions for later audit. Google additionally documents its Gemini implementation as a Preview capability that "may contain errors and security vulnerabilities" and recommends against using it for critical decisions, sensitive data, or actions where serious errors cannot be corrected.

## Related Terms

[[DefinedTerm/sandboxing]], [[DefinedTerm/agent-hooks]], [[DefinedTerm/indirect-prompt-injection]], [[DefinedTerm/human-in-the-loop]]
