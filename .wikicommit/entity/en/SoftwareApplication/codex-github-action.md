---
title: "Codex GitHub Action"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, agent-skills, agent-safety]
sources:
  - type: url
    url: 'https://developers.openai.com/blog/skills-agents-sdk'
    hash: sha256:92c2e202346410459520ce7bdf01b1af912f1f79aefe1e1c9bff2e809b5368a4
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "OpenAI's GitHub Action for running Codex inside a GitHub Actions workflow, used to carry a Codex workflow that works locally — such as a repo-local skill — into CI."
  applicationCategory: "CI integration for a coding agent"
  featureList: "Running Codex as a step in a GitHub Actions job; reusing repo-local skills and AGENTS.md rules in CI"
  author: "[[Organization/openai]]"
---

The Codex GitHub Action runs [[SoftwareApplication/openai-codex]] inside a GitHub Actions workflow. In [[BlogPosting/using-skills-to-accelerate-oss-maintenance]], the maintainers of the [[SoftwareApplication/openai-agents-sdk]] repositories describe it as the piece that carries a workflow into CI once it is useful locally: repository policy in [[DefinedTerm/agents-md]] tells Codex which workflows are required, repo-local skills hold those workflows, and the Action runs the same process automatically.

## Capabilities

The source describes the Action by what it is used for rather than by its interface. In the Agents SDK repositories it automates skill-based workflows in CI; the post's example is the JavaScript repository's changeset-validation skill, whose validation rules are kept in a shared prompt so that local runs and GitHub Actions apply the same logic.

For public repositories, the post relays a security checklist for the Action: limit who can start the workflow, prefer trusted events or explicit approvals, sanitize prompt inputs taken from PRs, commits, issues or comments, keep `OPENAI_API_KEY` protected with `drop-sudo` or an unprivileged user, and run Codex as the last step in the job. It adds that when a workflow is write-capable and takes untrusted public input, the risk usually lies in the trigger design, input handling and runtime privileges around the skill rather than in the skill itself.

## Adoption & Ecosystem

The maintainers' advice is to move a workflow into CI only once it is stable locally, because manual use is where the instructions are debugged, the scripts refined and the real edge cases found. The Action is distinct from Codex's automated PR review on GitHub, which the same post treats as a separate contributor to the repositories' throughput.
