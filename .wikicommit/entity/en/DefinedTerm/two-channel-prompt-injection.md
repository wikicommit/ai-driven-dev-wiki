---
title: "Two-Channel Prompt Injection"
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
  description: "A tool-invocation hijacking technique that splits a malicious payload across two channels of an agent's interaction with a compromised tool — the tool's description, which lures the agent into invoking it, and the tool's return value, which then injects instructions the agent follows."
---

Two-channel prompt injection is a technique, identified in academic security research on coding agents, for hijacking an agent's tool-invocation behavior by splitting a malicious payload across two separate channels of its interaction with a compromised external tool. The tool's description channel is used first, to lure the agent into selecting and invoking the attacker-controlled tool. The tool's return-value channel is used second: because a model tends to treat a tool's returned output as more actionable than its description (the description is read as documentation, while the return value is fed back to drive the next action), embedding follow-up instructions there was found more effective at getting the agent to carry them out — in the research this was used to trigger unauthorized command execution.

## Usage

In empirical testing, this two-channel approach achieved remote code execution on every one of six tested real-world coding agents in at least one configuration, and outperformed both single-channel baselines (embedding the same content only in the tool description) and several existing agent-security benchmarks' attack payloads adapted to the same goal. The research found that agent-side architectural changes — specifically, "progressive disclosure," where only a tool's name rather than its full description is surfaced to the model — substantially blocked the technique's first (lure) stage in newer releases of some tested agents, while newer, more safety-aligned backend models reduced but did not eliminate its effectiveness even when the description channel remained exposed.

## When It Applies

It applies to agents that can be induced to connect to an attacker-controlled or attacker-compromised external tool and that treat tool descriptions and tool returns as part of a single, undifferentiated text context rather than architecturally separating instructions from data. The research frames this lack of instruction/data separation as the underlying architectural condition the technique depends on, and points to instruction-data-separation designs (cited examples include SecAlign, MetaSecAlign, and StruQ) as a more durable defense than detecting malicious payloads after the fact.

## Related Terms

[[DefinedTerm/toolleak]], [[ScholarlyArticle/red-teaming-coding-agents-tool-invocation]]
