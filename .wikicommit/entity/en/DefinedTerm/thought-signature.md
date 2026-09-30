---
title: "Thought signature"
type: "schema:DefinedTerm"
lang: en
tags: [llm, tool-use, reasoning]
sources:
  - type: url
    url: 'https://developers.googleblog.com/new-gemini-api-updates-for-gemini-3/'
    hash: sha256:5c0c9a076fa04762c9220c98f1a90a42776dffeff714891ebb38383da16fa94f
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "In the Gemini API, an encrypted representation of the model's internal thought process that is returned with a response and passed back to the model in later calls, so that the model keeps its chain of reasoning across a conversation."
---

A thought signature, in [[Organization/google]]'s [[SoftwareApplication/gemini-api]], is an encrypted
representation of the model's internal thought process. The API returns it with the model's output,
and the application passes it back to the model in subsequent API calls; doing so is what lets the
model maintain its chain of reasoning across a conversation. Google presents this as critical for
complex, multi-step agentic workflows, where it says preserving the "why" behind a decision is just as
important as the decision itself.

## Usage

According to [[BlogPosting/new-gemini-api-updates-for-gemini-3]], the API began enforcing the return
of thought signatures starting with Gemini 3, and how strictly it validates them depends on the kind of
request:

- **Function calling** validates signatures strictly on the current turn; a missing signature results
  in a 400 error.
- **Text and chat generation** does not strictly enforce them, but omitting them degrades the model's
  reasoning and answer quality.
- **Image generation and editing** validates strictly for all model parts, including a
  `thoughtSignature`; a missing signature results in a 400 error.

Applications that use the official SDKs with standard chat history do not need to handle signatures
themselves, since the SDKs do so automatically.

## Related Terms

- [[DefinedTerm/function-calling]]
- [[DefinedTerm/client-and-server-tools]]
- [[DefinedTerm/reasoning-effort]]
