---
title: "Cloudflare VibeSDK"
type: "schema:SoftwareApplication"
lang: en
tags: [vibe-coding, agents, coding-agents, open-source]
sources:
  - type: url
    url: 'https://github.com/cloudflare/vibesdk'
    hash: sha256:e96a16b67969e2a5198bef237bcc885330257439519b6d86c1d6ee712bc224a4
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source, MIT-licensed agentic platform from Cloudflare for building and deploying full-stack applications by working with an AI coding agent, running every part of that workflow on Cloudflare's own services; its repository calls it a vibe coding platform for building your own vibe-coding platform."
  applicationCategory: "AI app-building platform"
  author: "Cloudflare"
---

Cloudflare VibeSDK is an open-source platform, published by Cloudflare under the MIT license, for
building and deploying full-stack applications by working with an AI coding agent. A user describes
what they want, answers the agent's clarifying questions, and follows along as the agent plans, edits
files, deploys previews, inspects errors and iterates with the user in the loop. The repository
describes it as an open-source [[DefinedTerm/vibe-coding]] platform "that helps you build your own
vibe-coding platform", built entirely on the Cloudflare stack; Cloudflare runs a public instance at
build.cloudflare.dev, and the project documents how to deploy one's own.

## Capabilities

Generation is agentic rather than staged: the README describes building iteratively through a
model-and-tool loop instead of a fixed sequence of generation phases. The agent can ask structured
questions when a request is underspecified ([[DefinedTerm/human-in-the-loop]] clarification), streams
its output, tool activity, file changes and deployment status to the interface, and shows generated
files in an integrated code editor. It works through explicit tools — reading and editing the
workspace, creating restore points, deploying previews, inspecting browser logs and asking questions
— and bash access is disabled.

The README sets the agent's workflow out as seven steps: understand the request, asking questions
where important details are missing; build by creating and editing files; save coherent restore
points; deploy by committing and bundling the current branch into a preview; verify by inspecting the
live preview and its browser console output; repair build or runtime errors and repeat the
deploy-and-verify loop; and stream progress to the interface throughout. Each generated application
gets its own isolated SQLite-backed storage that the user can inspect and reset, rollback restores a
chosen commit as a new commit rather than rewriting history, and finished projects can be exported to
continue development outside VibeSDK.

Every part of this runs on Cloudflare services. An agent built on Cloudflare Think and backed by a
Durable Object runs the model-and-tool loop; a separate Durable Object provides each project's
isolated workspace and files; Cloudflare Artifacts holds git history and restore points; generated
code is bundled and loaded as a Dynamic Worker preview, so no long-running development server is
needed; each generated app's data lives in a Durable Object Facet; and model providers are routed
through AI Gateway, which adds centralised observability and caching. The README lists the isolation
this gives: each app has its own agent, workspace, Artifacts repository and storage, and preview URLs
use signed, branch-scoped access.

## Adoption & Ecosystem

Running one's own instance requires a Cloudflare account with the relevant Workers features, a
Cloudflare API token, and credentials for at least one supported model provider unless provider keys
are stored in AI Gateway; production previews additionally need a Workers Paid plan with Workers for
Platforms access, and a production deployment needs a custom domain with wildcard DNS. Local
development uses Node.js and Bun, with a setup script that configures Cloudflare resources, AI
Gateway, model providers, authentication and database migrations.
