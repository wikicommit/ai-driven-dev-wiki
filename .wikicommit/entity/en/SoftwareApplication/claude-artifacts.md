---
title: "Claude Artifacts"
type: "schema:SoftwareApplication"
lang: en
tags: [ai-assisted-programming, coding-tools, sandboxing]
sources:
  - type: url
    url: https://simonwillison.net/2025/Mar/19/vibe-coding/
    hash: sha256:653ba52b66ad62da601ae6fd257897841726d7ac6a07029edc6d0e1c5b12188f
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "One of the first widely available platforms for building software by prompting an LLM, notable for running generated code inside a locked-down sandbox that cannot reach the network."
  applicationCategory: "Vibe coding platform"
  featureList: "Sandboxed execution in a locked-down iframe; loading restricted to approved libraries; no outbound network requests to other sites"
---

Claude Artifacts is described in [[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]] as
one of the first widely available platforms for [[DefinedTerm/vibe-coding]] — building software by
prompting a language model rather than by writing and reviewing code. What distinguishes it in that
account is not its generation ability but its containment: the code it produces runs inside a
sandbox that limits what a program its author has not read can do.

Simon Willison singles the sandboxing approach out as fantastic and treats it as the model for how
vibe coding is made safe for people new to building software. The same post is candid that the
containment is a real trade-off rather than a free one, and that the restrictions rule out whole
categories of project.

## Capabilities
Generated code is restricted to running in a locked-down iframe, can load only approved libraries,
and cannot make network requests to other sites. Willison's assessment is that this combination
makes it very difficult for someone to mess up and cause harm elsewhere with a project — the
sandbox absorbs the accidents that unreviewed code would otherwise cause.

The same restrictions bound what can be built. A project running under them cannot reach data from
external APIs, and cannot run its own prompts against an LLM. Willison names both limits explicitly
while still endorsing the design.

## Adoption & Ecosystem
The post positions Claude Artifacts at one end of a spectrum of vibe coding tools, with tools
originally aimed at professional developers — [[SoftwareApplication/cursor]] is the example given —
at the other, carrying far fewer safety rails. Willison presents this contrast as an open design
problem rather than a settled ranking, saying he hopes to see a wide proliferation of tooling that
helps people build their own custom tools both productively and safely.
