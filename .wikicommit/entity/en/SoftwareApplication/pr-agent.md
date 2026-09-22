---
title: "PR-Agent"
type: "schema:SoftwareApplication"
lang: en
tags: [code-review, coding-tools, agents]
sources:
  - type: url
    url: 'https://github.com/qodo-ai/pr-agent'
    hash: sha256:bae9d7a3b5520e87b29aedabf95fe580660a51d935b8c5996921390dc0fa1966
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source pull-request review agent, built by Qodo and since donated to the open-source community, that exposes its functions as slash commands run from a pull request comment or a CLI."
  applicationCategory: "Code review"
  featureList: "/describe, /review, /improve, /ask, /similar_issue"
  author: "[[Organization/qodo]]"
---

PR-Agent is an open-source, AI-powered code review agent that operates on pull requests. Its README
styles it "The Original Open-Source PR Reviewer" and describes it as a community-maintained legacy
project of [[Organization/qodo]], the company that built it. It is published under an MIT license,
with its own site at <https://www.pr-agent.ai> and documentation at <https://docs.pr-agent.ai>.

The project's functions are exposed as slash commands, run either as a comment on a pull request or
from a CLI against a pull request URL. `/describe`, `/review`, `/improve` and `/ask` act on a pull
request; `/similar_issue` is scoped to an issue instead. The README states that each of `/review`, `/improve` and `/ask` runs in a single LLM call,
which it puts at roughly thirty seconds and a low cost.

The README distinguishes the project from Qodo's own current offering, which it describes as a
feature-rich, context-aware experience, while labelling PR-Agent itself a community-maintained legacy
project. It is explicit that this repository is not Qodo's free tier for open-source projects, which
is a separate thing Qodo offers.

## Capabilities

The commands above are the interface. The README glosses only two of them — `/ask` takes a free-text
question about the pull request, and `/similar_issue` finds issues in the repository resembling a
given one — and lists the rest bare, deferring to its documentation site for the feature and git
provider support matrix and for each tool's own page. It does note that `/help_docs` has been
temporarily disabled since `v0.36.1` pending a fix for a credential-exposure issue, so the command
set a given installation exposes depends on which version it is running.

Two properties are claimed for the project as a whole rather than for any one command. A PR
compression strategy is credited with letting it process both small and large pull requests
effectively. Separately, prompting is JSON-based, which the README gives as what makes review
categories and behaviour customizable through configuration files rather than by editing the tool.

Nothing in the README ties the review output to a particular model. Models named as usable are
OpenAI's GPT, Anthropic's Claude, Google's Gemini, DeepSeek and Mistral, and beyond those any model
reachable through [[SoftwareApplication/litellm]] — a list that the README extends to Azure OpenAI,
AWS Bedrock, Vertex AI, Databricks, OpenRouter and Ollama.

## Adoption & Ecosystem

PR-Agent is platform-agnostic across both the forge it reviews on and the way it is deployed. The git
providers it supports are GitHub, GitLab, BitBucket, Azure DevOps and Gitea; the
deployment shapes are a CLI, a GitHub Action, Docker, a self-hosted instance and webhooks. The
quick-start paths the README leads with are a GitHub Actions workflow referencing the project's own
action, and `pip install pr-agent` followed by a CLI invocation carrying an API key in the
environment.

Docker images moved namespace partway through the project's life: releases from `0.34.2` onward are
published under `pragent/pr-agent`, while releases up to and including `v0.31` remain at the earlier
`codiumai/pr-agent` namespace as a frozen archive that receives no new images. The README asks that
pinned image references be updated when upgrading across that boundary.

The project's governance has moved as well. Qodo donated it to the open-source community; it now
lives in its own GitHub organization, is described as fully community-owned and open to additional
maintainers, and has gained its first external maintainer. The README states that it is in the
process of being donated to an open-source foundation, and that its documentation has moved to
docs.pr-agent.ai. Qodo remains its gold sponsor, under a heading stating that the project's ongoing
development is supported by its sponsors.
