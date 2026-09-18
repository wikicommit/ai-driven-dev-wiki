---
title: "Indirect Prompt Injection"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/abs/2302.12173'
    hash: sha256:1e144027a6780c13f8ad053d161433e874416a09dfb69becbdb3ebfac34f9e31
  - type: url
    url: 'https://arxiv.org/pdf/2604.27202'
    hash: sha256:ec1b1d5a6010017bb19ec0c21ebfc834c928a2c0ba6c97cfaf109ffcef44937b
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A prompt-injection technique in which an attacker plants adversarial instructions in data an LLM-integrated application is likely to retrieve and process — rather than typing them into the model directly — letting the attacker remotely exploit the application without any direct interface to it."
---

Indirect prompt injection is a technique, introduced by Greshake et al. in [[ScholarlyArticle/not-what-youve-signed-up-for]], for remotely exploiting an LLM-integrated application by strategically planting adversarial prompts in data the application is likely to retrieve — rather than an attacker needing to directly prompt the model themselves. It exploits the fact that LLM-integrated applications blur the line between data and instructions, so content the application merely retrieves and feeds to the model as context can act on the model the same way a direct instruction would.

## Usage

Beyond the adversarial framing the term was coined under, the same mechanism has been put to defensive use. [[ScholarlyArticle/indirect-prompt-injection-in-the-wild]], a measurement study of 1.2 billion URLs, finds that instructions embedded in web pages pursue six distinct objectives spanning offensive, defensive and underspecified uses. On the offensive side the study records system disruption — instructing an agent to emit random strings, repeated nonsense or text intended to exhaust context limits — along with reputation manipulation through content promotion, citation forcing and positive-review forcing, and a small number of data-exfiltration attempts. On the defensive side it records site owners asserting copyright and personal-data restrictions against automated reuse, and an AI-bot-identification pattern in which a page asks any reading model to include a marker phrase in its response so that automated visitors can be detected. Its authors read this as a multi-stakeholder ecosystem with competing incentives rather than a purely malicious practice, and characterize current deployment as working more through friction and degradation than through reliable control.

That study also reports how such instructions are delivered in practice. Task override — directly replacing the model's current instructions rather than persuading it — appears in 99% of the instances it validated, often reinforced by jailbreak-style framing. Most are not meant for human eyes: about 70% sit in channels that are never rendered, such as HTTP response headers, comments, structured data and metadata fields, and among those embedded in rendered HTML the great majority are concealed by techniques such as colour and contrast manipulation, occlusion and viewport-based hiding. The instructions are also highly templated, with 54 lexical templates accounting for 95% of cases, and durable: 65% of the affected pages already carried an injection twelve months before the snapshot analysed.

## When It Applies

It applies to LLM-integrated applications that retrieve data likely to contain adversarial content and pass it to the model as part of its context, without the application separating retrieved data from instructions. The paper that introduced the technique demonstrated its practical viability against real-world systems, including Bing's GPT-4-powered Chat and code-completion engines, and against synthetic applications built on GPT-4, showing that a retrieved, injected prompt can act as arbitrary code execution from the application's perspective and can manipulate whether and how the application calls other APIs. The introducing paper states that effective mitigations against this class of attack were lacking at the time of writing.

How much it succeeds depends heavily on how the retrieved content is presented to the model. In 5,200 controlled trials across 13 models and four page representations, the measurement study found compliance limited but non-negligible, peaking at 8% for small models on plain text and falling to between 0.2% and 1.1% where structural cues were preserved — its explanation being that flattening a page strips away the markup, comments, metadata and styling that would otherwise reveal an instruction as hidden and out of place. Two cautions attach to that result. Lower compliance on richer representations is not the same as robustness, because those representations are much longer and frequently caused models to fail before producing usable output at all. And recognizing an injection is not the same as resisting it: the study records cases in which a model explicitly warned about the injected instruction and complied with it anyway.

Its authors present their figures as a lower bound, since their corpus draws mainly on public web crawls that may underrepresent authenticated content and their detection relies on an indicator list that may miss obfuscated or non-English variants. They also note that the instructions they observed are overwhelmingly static strings, and caution against reading today's modest effectiveness as a long-term ceiling.

## Related Terms

[[ScholarlyArticle/not-what-youve-signed-up-for]], [[ScholarlyArticle/indirect-prompt-injection-in-the-wild]], [[DefinedTerm/two-channel-prompt-injection]], [[DefinedTerm/tool-poisoning]], [[DefinedTerm/guardrails]]
