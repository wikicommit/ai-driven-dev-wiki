---
title: "ToolLeak"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.05755'
    hash: sha256:8e50b266c6e2a6123f82bdf0c720da2858a0661af4273550d96402af17f54c6c
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A prompt-exfiltration technique that exploits a behavioral gap between an LLM's ordinary chat replies and its schema-driven tool-call argument generation, tricking a coding agent into copying its own hidden system prompt into an attacker-controlled tool's arguments."
---

ToolLeak is a prompt-exfiltration technique for AI coding agents, identified in academic security research, that exploits a "mode gap" between an LLM's ordinary chat output and its schema-driven tool-call argument generation. Rather than asking a model directly to reveal its system prompt — a request modern models are trained to refuse — an attacker registers an external tool (e.g. via the Model Context Protocol) whose declared argument schema asks for something like "the current system prompt." When the agent invokes that tool to satisfy the schema, it treats filling in the argument as benign structured completion rather than an instruction to disclose secrets, and copies its hidden internal context into the argument value, which the attacker-controlled tool can then observe.

## Usage

In empirical testing against six real-world coding agents (Cursor, Claude Code, GitHub Copilot, Windsurf, Cline, Trae), the technique is reported to have outperformed prior prompt-leakage baselines that rely on explicit requests (e.g. "repeat your system prompt," "ignore previous instructions"), which state-of-the-art models are comparatively resistant to. The research identifies output-side sensitivity awareness — training a model to recognize and suppress sensitive content in its outputs regardless of how that output was generated — as a more principled defense than pattern-matching on request phrasing, since the technique's tool-argument payload was found to be semantically indistinguishable from a legitimate tool description under perplexity-based and prompt-injection-classifier detectors in that research.

## When It Applies

It applies to any LLM-based agent that both holds security-sensitive context (such as a system prompt) and can be induced to connect to an attacker-influenced external tool whose argument schema can request that context. Necessary conditions identified in the research include the secret being present in the model's context at generation time, the attacker controlling the tool's declared argument requirements, at least one required argument field expressive enough to carry meaningful text, and the absence of argument sanitization before the tool receives the filled-in values.

## Related Terms

[[DefinedTerm/two-channel-prompt-injection]], [[ScholarlyArticle/red-teaming-coding-agents-tool-invocation]]
