---
title: "Devstral"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, coding-tools, open-source]
sources:
  - type: url
    url: 'https://mistral.ai/news/devstral'
    hash: sha256:391e456654323c32f4e71ba4eaf0b08ccd8b7650155b2bf99f04f989ea5772cb
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Mistral AI's May 2025 announcement of Devstral, an Apache 2.0 agentic LLM for software engineering built with All Hands AI and trained to resolve real GitHub issues while running over code agent scaffolds. The post argues that atomic code generation and real-world software engineering are different problems, and presents Devstral as small enough to run on a single consumer GPU."
  author: "Mistral AI"
  publisher: "Mistral AI"
  datePublished: "2025-05-21"
---

*Devstral* is Mistral AI's announcement, published on 21 May 2025, of an agentic LLM aimed
specifically at software engineering tasks, built in collaboration with All Hands AI and released
under the Apache 2.0 license. The post's opening move is to separate two things it argues are
routinely conflated: writing a standalone function or completing a line, which it says ordinary
LLMs already do well, and resolving a real software engineering problem, which it says they
struggle with.

The distinction the post draws is about context rather than raw code quality. Real development,
on its account, requires situating code within a large codebase, identifying relationships between
disparate components, and finding subtle bugs in intricate functions — none of which an atomic
completion task exercises. Devstral is presented as trained against that harder shape of problem
directly: on real GitHub issues, running over code agent scaffolds that define the interface
between the model and the tests.

The post's second argument is about size. Mistral presents Devstral as light enough to run on a
single consumer GPU or a 32GB Mac, and draws two consequences from that: local deployment against
a local codebase, and use inside enterprises with privacy, security or compliance constraints that
make sending a repository to a hosted model unattractive. The release is labelled a research
preview, with a larger agentic coding model promised to follow in the coming weeks.

## Key Points

- The post's central claim is that typical LLMs are good at atomic coding tasks such as standalone functions and completion but struggle with real-world software engineering, because real development requires contextualising code within a large codebase, identifying relationships between disparate components, and finding subtle bugs in intricate functions.
- Devstral is described as trained to solve real GitHub issues and as running over code agent scaffolds such as [[SoftwareApplication/openhands]] or [[SoftwareApplication/swe-agent]], which the post says define the interface between the model and the test cases.
- Mistral reports Devstral at 46.8% on [[Dataset/swe-bench-verified]], which the post characterises as more than 6 percentage points above the prior open-source state of the art. This is the vendor's own reported figure in its own launch post.
- The post states that under the same test scaffold — OpenHands, provided by All Hands AI — Devstral exceeds far larger models including Deepseek-V3-0324 at 671B and Qwen3 232B-A22B, and that compared against models evaluated under any scaffold it surpasses "the recent GPT-4.1-mini by over 20%" — the post does not say whether that figure is percentage points or a relative margin. The scaffold caveat is the post's own and is what makes the two comparisons different claims.
- Mistral presents the model as light enough to run on a single RTX 4090 or a Mac with 32GB of RAM, which the post offers as the basis for local deployment and on-device use.
- The post argues that this local-deployment property also suits agentic coding on privacy-sensitive enterprise repositories subject to stringent security and compliance requirements. The backing offered is Mistral's own positioning rather than a reported deployment.
- Devstral was released under Apache 2.0 and distributed through Hugging Face, Ollama, Kaggle, Unsloth and LM Studio, as well as through Mistral's own API.
- The post labels the release a research preview and states that a larger agentic coding model was in progress at the time of writing.

## Context

The post is written from Mistral's own vantage as the model's publisher, and its benchmark and
comparison claims are all its own. Its most load-bearing qualification is one it states itself:
the strongest of its comparisons holds when competing models are evaluated under the same
scaffold, and the post separates that case from comparisons against models "evaluated under any
scaffold (including ones custom for the model)". It draws the distinction without saying how large
an effect the scaffold has.

What the post claims as distinctive is a combination rather than any single property: a model
trained for agentic software engineering rather than code completion, light enough to run on a
single consumer GPU or a 32GB Mac, and released under a permissive license. The framing that
separates [[DefinedTerm/software-issue-resolution]] from atomic code generation is the post's own
way of motivating that combination, and this page does not extend it to any other release of the
period — the post discusses no others except as benchmark comparisons.
