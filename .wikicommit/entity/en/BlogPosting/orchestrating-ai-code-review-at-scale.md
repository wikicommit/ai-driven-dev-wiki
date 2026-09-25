---
title: "Orchestrating AI Code Review at scale"
type: "schema:BlogPosting"
lang: en
tags: [code-review, multi-agent, ci-cd, agents-md]
sources:
  - type: url
    url: 'https://blog.cloudflare.com/ai-code-review/'
    hash: sha256:3713b9e52fb6d7bc6997a3eb6390c9e942880583682e40e2101d03533bc6657b
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An April 2026 Cloudflare engineering post describing the company's internal CI-native AI code review system, in which a coordinator agent running on OpenCode spawns up to seven specialised reviewer agents on each merge request, consolidates their findings and posts a single structured review."
  author: ["Ryan Skidmore"]
  datePublished: "2026-04-20"
  publisher: "Cloudflare"
---

This post on Cloudflare's blog, tagged as part of the company's Agents Week 2026, describes how Cloudflare
built its internal AI code review system. It recounts that off-the-shelf AI review tools did not offer
enough flexibility for an organisation of Cloudflare's size, and that feeding a raw diff into a single
prompt produced noisy output — vague suggestions and hallucinated syntax errors. The team instead built a
CI-native orchestration system around [[SoftwareApplication/opencode]], an open-source coding agent, in
which each merge request receives an initial pass from up to seven specialised reviewer agents covering
security, performance, code quality, documentation, release management, AGENTS.md upkeep and compliance
with Cloudflare's internal Engineering Codex. A coordinator agent deduplicates their findings, judges
severity and posts one structured review comment, and can approve, comment, or block the merge.

Most of the post is an engineering account of running LLMs in the critical path of a CI/CD pipeline:
the plugin architecture, how OpenCode is driven programmatically, prompt design for the specialists,
risk-based tiering, concurrency, resilience against provider failures, a configuration control plane,
incremental re-reviews, and figures from the system's first month. It is a firsthand account of one
company's internal system rather than a general method, and an example of
[[DefinedTerm/agentic-code-review]] organised as a coordinator over specialist sub-agents.

## Key Points

- The system is built on a composable plugin architecture in which plugins contribute to a review
  through a controlled context API — registering agents, providers, prompt sections and permissions —
  and a core assembler merges the result into the configuration file OpenCode consumes; the post says
  this keeps VCS-specific and AI-provider-specific concerns isolated from each other.
- The post says OpenCode was chosen because the team already used it, because it is open source (it
  reports Cloudflare engineers landing over 45 pull requests upstream), and above all because it is
  structured server-first, which let the team create sessions, send prompts and collect results from
  concurrent sessions through an SDK rather than scripting a CLI.
- The coordinator runs as an OpenCode child process whose prompt is passed on stdin to avoid the kernel's
  argument-length limit, with its output consumed as JSON Lines; a runtime plugin gives it a
  `spawn_reviewers` tool that launches each specialist in its own OpenCode session.
- The post argues that telling a model what not to flag is where the real prompt-engineering value lies:
  the security reviewer, for example, is told to report only exploitable or concretely dangerous issues
  and to skip theoretical risks and defence-in-depth suggestions. Findings are structured with a
  critical, warning or suggestion severity.
- Models are assigned by task difficulty — top-tier models for the coordinator, standard-tier models for
  code quality, security and performance, and a lighter model for text-heavy reviewers — and every
  assignment can be overridden at runtime from a configuration Worker, which the post says lets an entire
  provider be disabled across running jobs within seconds.
- Each merge request is classified into a trivial, lite or full risk tier by diff size and whether
  security-sensitive paths are touched, and each tier runs a different number of agents; lock files,
  vendored and minified assets and generated files are filtered out first, with database migrations
  exempted from the generated-file filter.
- The `spawn_reviewers` tool acts as a small scheduler with per-task and overall timeouts, inactivity
  detection, a circuit breaker per model tier modelled on Netflix's Hystrix, and failback chains that fall
  back to an older model generation within the same family; only retryable API errors trigger failback.
- Diffs are written to per-file patch files and a shared context file rather than embedded in each
  prompt, which the post says avoids multiplying token costs across concurrent reviewers and contributes
  to a reported 85.7% cache hit rate.
- A human can comment "break glass" to force approval; re-reviews are incremental, receive the previous
  findings and their resolution status, and resolve or keep threads accordingly.
- A dedicated AGENTS.md reviewer flags merge requests that make material architectural changes, such as
  switching test framework or package manager, without updating the repository's AGENTS.md (see
  [[DefinedTerm/agents-md]]), and penalises filler content and overly long files.
- For its first 30 days the post reports 131,246 review runs across 48,095 merge requests in 5,169
  repositories, a median review time of 3 minutes 39 seconds, about 1.2 findings per review, and "break
  glass" used on 0.6% of merge requests — self-reported figures from Cloudflare's own telemetry.

## Context

The post is explicit that the system is not a replacement for human code review with today's models. It
lists architectural awareness, cross-system impact such as downstream consumers of a changed API
contract, subtle concurrency bugs, and cost growing with diff size as areas where the AI reviewers
struggle. It frames the work as part of Cloudflare's broader engineering-resiliency effort, and the
design choices it reports — a strong bias toward approval, a manual override, and deliberately few
findings per review — are one organisation's answer to keeping an automated reviewer from obstructing
engineers.
