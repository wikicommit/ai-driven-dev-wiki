---
title: "Gemini API developer skill"
type: "schema:SoftwareApplication"
lang: en
sources:
  - type: url
    url: 'https://developers.googleblog.com/closing-the-knowledge-gap-with-agent-skills/'
    hash: sha256:99da78c38e52825287d818db6e10f2cf2d633b7e9479102298bccb809800d651
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"
tags: [agent-skills, agent-tooling, context-engineering]

properties:
  description: "A Google-maintained agent skill that gives a coding agent current knowledge of the Gemini API's models, SDKs and documentation entry points."
  applicationCategory: "Agent skill"
  author: "[[Organization/google]]"
---

The Gemini API developer skill (`gemini-api-dev`) is an [[DefinedTerm/agent-skills]]
package published by Google at github.com/google-gemini/gemini-skills, built so that a
coding agent working against the Gemini API uses Google's current models and SDKs rather
than whatever was current at the model's training cut-off. Its authors describe it as an
example of what any SDK maintainer can do about that gap, rather than as something only a
model builder could provide.

## Capabilities

The skill supplies what its authors call a basic set of primitive instructions: it explains the high-level
feature set of the API, describes the current models and SDKs for each language,
demonstrates basic sample code for each SDK, and lists the documentation entry points as
sources of truth. Its authors characterize this as a primitive set of instructions that
guides an agent toward the latest models and SDKs while also referring it to the
documentation, so that fresh information is retrieved from the source of truth rather
than read only from the skill itself.

Google reports keeping the skill maintained as it ships model updates. Its authors also
name the maintenance limitation the format carries: there is no good update story beyond
asking users to update manually, which they warn could leave stale skill information in
users' workspaces over time.

## Adoption & Ecosystem

The skill is distributed from GitHub and can be installed into a project directly, either
through Vercel skills or through Context7:

```
# Install with Vercel skills
npx skills add google-gemini/gemini-skills --skill gemini-api-dev --global

# Install with Context7 skills
npx ctx7 skills install /google-gemini/gemini-skills gemini-api-dev
```

Google evaluated the skill against an evaluation harness of 117 code-generation prompts and
reported that it improved results substantially for its newer, stronger-reasoning models
and much less for older ones — the figures and the method are given in
[[BlogPosting/closing-the-knowledge-gap-with-agent-skills]].
