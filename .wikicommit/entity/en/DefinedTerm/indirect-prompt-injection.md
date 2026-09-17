---
title: "Indirect Prompt Injection"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/abs/2302.12173'
    hash: sha256:1e144027a6780c13f8ad053d161433e874416a09dfb69becbdb3ebfac34f9e31
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A prompt-injection technique in which an attacker plants adversarial instructions in data an LLM-integrated application is likely to retrieve and process — rather than typing them into the model directly — letting the attacker remotely exploit the application without any direct interface to it."
---

Indirect prompt injection is a technique, introduced by Greshake et al. in [[ScholarlyArticle/not-what-youve-signed-up-for]], for remotely exploiting an LLM-integrated application by strategically planting adversarial prompts in data the application is likely to retrieve — rather than an attacker needing to directly prompt the model themselves. It exploits the fact that LLM-integrated applications blur the line between data and instructions, so content the application merely retrieves and feeds to the model as context can act on the model the same way a direct instruction would.

## When It Applies

It applies to LLM-integrated applications that retrieve data likely to contain adversarial content and pass it to the model as part of its context, without the application separating retrieved data from instructions. The paper that introduced the technique demonstrated its practical viability against real-world systems, including Bing's GPT-4-powered Chat and code-completion engines, and against synthetic applications built on GPT-4, showing that a retrieved, injected prompt can act as arbitrary code execution from the application's perspective and can manipulate whether and how the application calls other APIs. The introducing paper states that effective mitigations against this class of attack were lacking at the time of writing.

## Related Terms

[[ScholarlyArticle/not-what-youve-signed-up-for]]
