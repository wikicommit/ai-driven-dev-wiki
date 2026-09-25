---
title: "Edit apply model"
type: "schema:DefinedTerm"
lang: en
tags: [coding-agents, code-editing]
sources:
  - type: url
    url: https://cognition.ai/blog/dont-build-multi-agents
    hash: sha256:c456bd571f488ee46bc4c213e9d4302677f283c444dd4b85a1ad7fa1bd41d480
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A code-editing design in which a large model writes a Markdown explanation of the changes it wants and a small model rewrites the whole file from that explanation. It was common among coding agents, IDEs and app builders in 2024, when large models were unreliable at producing properly formatted diffs."
---

An edit apply model is a small model used in a two-model code-editing setup: a large model decides what
to change and describes the edit as a Markdown explanation, and the small "edit apply" model then
rewrites the entire file to carry that explanation out. As described in
[[BlogPosting/dont-build-multi-agents]], the idea rested on the observation that, at the time, getting a
small model to rewrite a whole file from a description was more reliable than getting a large model to
output a properly formatted diff.

## Usage

That post describes the pattern as a common practice in 2024 among coding agents, IDEs and app builders,
including [[SoftwareApplication/devin]], at a time when many models were bad at editing
code. It uses the pattern as an example of what goes wrong when decisions and actions are split across
models: the small model would often misinterpret the large model's instructions and make an incorrect
edit because of the slightest ambiguity in them. The post adds that edit decision-making and applying
are now more often done by a single model in one action.

## Related Terms

- [[DefinedTerm/context-engineering]] — the post discusses the pattern among its real-world examples of
  architecting agents to avoid conflicting decision-making
