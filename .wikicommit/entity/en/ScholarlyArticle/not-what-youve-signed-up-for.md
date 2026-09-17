---
title: "Not what you've signed up for: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection"
type: "schema:ScholarlyArticle"
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
  description: "A 2023 paper that introduces Indirect Prompt Injection, a class of attacks that remotely exploit LLM-integrated applications by strategically injecting adversarial prompts into data the application is likely to retrieve, rather than requiring the attacker to directly prompt the model."
  author: ["Kai Greshake", "Sahar Abdelnabi", "Shailesh Mishra", "Christoph Endres", "Thorsten Holz", "Mario Fritz"]
  datePublished: "2023-02-23"
  keywords: ["Cryptography and Security", "Artificial Intelligence", "Computation and Language", "Computers and Society"]
---

This paper argues that because large language models can be flexibly modulated via natural language prompts, LLM-integrated applications blur the line between data and instructions, opening a new attack surface beyond the assumption that a user is the one directly prompting the model. It introduces [[DefinedTerm/indirect-prompt-injection]]: strategically planting adversarial prompts in data that an LLM-integrated application is likely to retrieve, letting an attacker remotely exploit the application without any direct interface to it.

The paper derives a taxonomy, from a computer security perspective, to systematically investigate the resulting impacts and vulnerabilities, and demonstrates the attacks' practical viability against real-world systems.

## Key Points

- The paper's taxonomy of impacts and vulnerabilities from indirect prompt injection includes data theft, worming, and information ecosystem contamination, among other novel security risks.
- The attacks were demonstrated as practically viable against real-world systems, including Bing's GPT-4-powered Chat and code-completion engines, as well as against synthetic applications built on GPT-4.
- The paper shows that processing a retrieved, injected prompt can act as arbitrary code execution from the application's perspective, manipulating the application's functionality and controlling whether and how other APIs are called.
- The paper states that, despite increasing integration and reliance on LLMs, effective mitigations for these threats were lacking at the time of writing.

## Notes

This entry is based on the paper's arXiv abstract page rather than its full text; the summary above reflects only what the abstract itself states, not the paper's full methodology or detailed case-study results.
