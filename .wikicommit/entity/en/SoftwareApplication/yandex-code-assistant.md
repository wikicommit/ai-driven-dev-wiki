---
title: "Yandex Code Assistant"
type: "schema:SoftwareApplication"
lang: en
tags: [code-completion, coding-tools]
sources:
  - type: url
    url: 'https://habr.com/ru/companies/yandex/articles/841436/'
    hash: sha256:ed090e4e81e25e3fc5fbdddabb08371c8ae7509c5d4943bdcadbc1d5a5459eff
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A code assistant from Yandex focused on inline code suggestions in the IDE, built by an ML laboratory in Yandex Infrastructure and opened for free testing on the Yandex Cloud platform."
  applicationCategory: "AI code assistant"
  author: "[[Organization/yandex]]"
---

Yandex Code Assistant is a code-writing assistant developed by an ML laboratory in Yandex Infrastructure, the Yandex team that builds the platform the company's own developers work on. According to [[BlogPosting/how-we-taught-yandex-code-assistant-to-make-developers-happy]], it began as an internal rollout of inline suggestions to Yandex teams and was then opened with free access, in test mode, on the Yandex Cloud platform.

The product deliberately concentrates on inline suggestions — code shown in grey as the developer types, accepted with Tab or dismissed with Esc — rather than on a chat interface: after reviewing their own experience and talking to fellow developers, the team found inline suggestions to be in real demand and chose to focus on them.

## Capabilities

Suggestions are generated as complete code statements, identified through an abstract syntax tree, rather than as arbitrary continuations of text; a suggestion that cuts a statement off is treated as a bad one, and the model can also decline to suggest anything. The models are fine-tuned from existing models on Yandex's own code, with fill-in-the-middle support so that suggestions take account of code both before and after the cursor, and the post lists Python, TypeScript, C++, YAML, JSON, Kotlin, Java, Go, Swift, Scala and YQL/SQL as the languages it was fine-tuned on.

The service is split into a CPU backend holding all business logic — whether to request a suggestion at all, enriching the context with the user's own code, and ranking the model's answers against a threshold — and a GPU backend for inference, with IDE plugins, including one for JetBrains IDEs, acting only as proxies. The stated latency budget is 500 ms, and the post reports 420 ms at the 99th percentile.

## Adoption & Ecosystem

Use inside Yandex was voluntary, and the team judged quality through retention, an offline unit-test metric, acceptance rate and finally a composite [[DefinedTerm/developer-happiness-metric]]. Yandex's own figures, as given in that post, are that 15% of the code developers write in a day is written with the assistant and that 60% of the thousands of Yandex developers who tried it became regular users.
