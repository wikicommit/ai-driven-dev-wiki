---
title: "Claude Artifacts"
type: "schema:SoftwareApplication"
lang: en
tags: [vibe-coding, sandboxing]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Mar/19/vibe-coding/'
    hash: sha256:e725441983198e989861ffd8eb4fbccea921fa47abf24f5644429df24f706ce5
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "One of the first widely available vibe coding platforms, characterised by a sandbox that confines generated code to a locked-down iframe with no outbound network access — a design that limits both the harm and the capability of the projects built in it."
  applicationCategory: "vibe coding platform"
---

Claude Artifacts is described by [[Person/simon-willison]] as one of the first widely available platforms for [[DefinedTerm/vibe-coding]], and as an example of how sandboxing can make that practice safe for complete beginners. Its distinguishing property is the sandbox rather than the code generation: generated code runs inside a locked-down `<iframe>`, can load only approved libraries, and cannot make network requests to other sites.

Willison, who calls the approach "fantastic", frames the design as a deliberate trade. The sandbox makes it very difficult for someone to mess up and cause harm with their project — which is the reason he cites for liking it, since accidents cannot propagate elsewhere. It also greatly limits what those projects can do: an Artifacts project cannot reach data from external APIs, and cannot even run the author's own prompts against an LLM.

## Overview

The platform sits at the beginner-safe end of the vibe coding tool spectrum as Willison presents it. He contrasts it with [[SoftwareApplication/cursor]], which he describes as initially intended for professional developers and as having far less safety rails, and treats the gap between the two as evidence that there is room for innovation in tooling that lets people build their own custom tools both productively and safely.

## Features

The sandbox is the feature the source describes: an `<iframe>` restricted to an approved set of libraries, with outbound network requests to other sites blocked. No other capability of the platform is described in the source available here.
