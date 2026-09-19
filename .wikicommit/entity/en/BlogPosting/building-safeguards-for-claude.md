---
title: "Building safeguards for Claude"
type: "schema:BlogPosting"
lang: en
tags: [agent-safety, evaluation, security]
sources:
  - type: url
    url: 'https://www.anthropic.com/news/building-safeguards-for-claude'
    hash: sha256:6a49d6c32820761dc21bf0f49ae31d6b9fbf8fca45f239601c5fb33ac418abf1
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Anthropic's account of how its Safeguards team builds protections across a model's lifecycle: policy development, influencing training, pre-deployment testing, real-time classifier-based detection and enforcement, and ongoing monitoring. Notable here for describing enforcement that runs inside the provider's own serving path."
  datePublished: "2025-08-12"
  publisher: "[[Organization/anthropic]]"
---

This post describes how Anthropic's Safeguards team builds protections around Claude, organised as
layers spanning the whole model lifecycle rather than as a single control point: developing usage
policy, influencing model training, testing for harmful outputs before release, enforcing policy in
real time once deployed, and monitoring for novel misuse patterns afterwards. The team is described as
combining policy, enforcement, product, data science, threat intelligence and engineering.

For a reader concerned with agentic systems rather than consumer safety, the post's directly relevant
contribution is its account of runtime enforcement: a layer of [[DefinedTerm/guardrails]] that sits
inside the provider's own serving path, implemented as prompted or fine-tuned Claude models called
classifiers, and capable of altering the system prompt of a live request or stopping a response
outright. It also records a concrete pre-launch finding about [[DefinedTerm/computer-use]] that changed
what shipped with that tool.

Much of the rest of the post concerns harm domains outside this wiki's subject — child safety, election
integrity, CBRNE risk assessment, bias evaluation — and is summarised here only so far as it establishes
the structure the runtime mechanisms sit within.

## Key Points

- Safeguards is described as operating across five layers: policy development, model training, testing
  and evaluation, real-time detection and enforcement, and ongoing monitoring and investigation.
- Policy development is guided by two named mechanisms: a Unified Harm Framework considering physical,
  psychological, economic, societal and individual-autonomy impacts — described as a structured lens
  weighing likelihood and scale rather than a formal grading system — and Policy Vulnerability Testing,
  in which external domain experts stress-test policies against model output under challenging prompts.
- Pre-release evaluation is split into safety evaluations against the Usage Policy, risk assessments for
  high-risk domains conducted with government and industry partners, and bias evaluations; results are
  reported in the system cards released with each model family.
- Safety evaluations are described as covering clear violations, ambiguous contexts and extended
  multi-turn conversations, and as using Anthropic's own models to grade Claude's responses with human
  review as an additional accuracy check.
- Pre-launch evaluation of the computer use tool determined it could augment spam generation and
  distribution. The post states that, before launch, this led to new detection methods and enforcement
  mechanisms — including the option to disable the tool for accounts showing signs of misuse — and new
  protections for users against prompt injection.
- Runtime detection is built on classifiers: prompted or specially fine-tuned Claude models that detect
  specific policy violations in real time, with several deployable simultaneously, each monitoring a
  different type of harm while the main conversation flows normally.
- Two enforcement actions are described. Response steering adjusts how Claude interprets and responds to
  a prompt in real time — the post's example is automatically adding instructions to the system prompt
  when a classifier detects an apparent attempt to generate spam or malware — and in a narrow set of
  cases can stop Claude responding entirely. Account enforcement covers warnings and, in severe cases,
  termination.
- The engineering constraint is stated explicitly: classifiers must process trillions of input and output
  tokens while limiting both compute overhead and enforcement on benign content.
- Ongoing monitoring uses hierarchical summarization — condensing individual interactions into summaries
  and analysing those to identify account-level concerns — which the post says helps spot behaviour that
  appears violative only in aggregate, such as automated influence operations.
- Threat intelligence work is described as comparing indicators of abuse such as unusual spikes in
  account activity against typical usage patterns, cross-referencing external threat data with internal
  systems, and monitoring channels where bad actors operate; findings are published in public threat
  intelligence reports.
- The post states a bug bounty programme is run for testing these defences, and frames safeguarding AI
  use as work no single organization can do alone.

## Context

This is Anthropic's own description of its internal practice, published as product communication rather
than as a research report. No effectiveness figures are given for any of the mechanisms — no classifier
precision or recall, no false-positive rate on benign content, no measure of how much misuse the layers
catch — so what the post establishes is the shape of the system and the existence of each mechanism,
not how well any of them works.

Two of its details carry weight beyond consumer safety. The classifier-and-response-steering
arrangement is a guardrail layer operating inside the provider's serving path, which is a different
location from the organizational, application, framework and toolkit layers other accounts of
guardrails describe; and the computer use finding is a documented case of a pre-deployment evaluation
changing what shipped with an agent capability, which is the pattern the post's testing section argues
for in general.
