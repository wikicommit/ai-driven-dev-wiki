---
title: "Multi-model orchestration"
type: "schema:DefinedTerm"
lang: en
tags: [agents, multi-agent, orchestration]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/62404/'
    hash: sha256:d49efd9233d456d1b205c748e19560ccabe3dc107352ab0e2e2f6f98094dd5ca
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Running coding agents built on models from more than one provider under a single orchestration, dividing roles between them according to each model's characteristics."
---

Multi-model orchestration is the practice of running coding agents built on models from more than one provider under a single orchestration and dividing the work between them according to each model's characteristics. [[BlogPosting/sdd-in-unity-client-antipatterns-and-improvements]] describes it as the fix for a throughput limit: token-consumption limits from a single provider had capped how many work lines could run in parallel, and spreading work across providers raised it.

## Usage

In the post's setup, [[SoftwareApplication/claude-code]] is the main agent and [[SoftwareApplication/openai-codex]] a sub-agent. Specs are written with Opus, and execution runs on Sonnet and GPT-5.3-Codex. The spec-implementation command delegates implementation, test writing and general work to Codex in one piece, while Claude reviews the result for conformance to the spec; if Codex fails several times or regression tests fail, Claude Code takes the work over and implements it itself.

The Codex CLI is called from the shell through a skill, which returns JSON: on success the task output, the tokens used and a log directory; on failure the exit code, tokens used, log directory and a fix Codex suggests. Only on failure is Codex asked again, and its log-based suggestion is passed back to Claude.

## When It Applies

The post applies it when a single provider's token limits cap parallel agent work. It assumes a way to bridge the split in context between models: because the sub-agent does not share the main agent's context, Claude generates the prompt for Codex from the spec, and the author found Codex needs stricter instructions than Claude, so separate skills build prompts suited to it. Two failure points are reported. Context is fragmented across models, and the main agent sometimes gives reasons to avoid delegating to Codex for the sake of efficiency — behaviour the author has not been able to suppress fully and monitors through work logs. This is one engineer's report from one project; the post's summary presents it as an effective means of raising throughput, not as a measured result.

## Related Terms

- [[DefinedTerm/sub-agent-architecture]]
- [[DefinedTerm/context-bloat-loop]]
- [[DefinedTerm/deterministic-quality-gate]]
