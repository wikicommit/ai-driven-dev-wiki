---
title: "SWE-Agent"
type: "schema:SoftwareApplication"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2508.11126'
    hash: sha256:d8a0f4c103987a46e21f37fca41b5ebfa795945e9c798921c4fdfbfc18bd9346
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A multi-agent coding system that assigns role-specific LLM agents — an Architect for high-level design, a Coder for implementation, and a Reviewer for quality assurance — connected through structured dialogue and shared memory to resolve software engineering tasks."
  applicationCategory: "Multi-agent coding system"
---

SWE-Agent is a multi-agent AI coding system that divides a software engineering task among multiple role-specific LLM agents rather than handling it with a single model: an "Architect" agent is responsible for high-level design, a "Coder" agent for implementation, and a "Reviewer" agent for quality assurance, with the three connected through structured dialogue and shared memory.

## Capabilities

A survey on AI agentic programming reports that SWE-Agent uses GPT-4 as its underlying model with a 16,000-token default context window, and that it supports persistent memory across a task by retrieving tool outputs and plan state from a vector database, rather than relying only on what fits in its active context window.

## Adoption & Ecosystem

The same survey classifies SWE-Agent, in its comparative taxonomy of AI agentic programming systems, as a "Multi-agent System" that is proactive (it initiates its own sub-tasks and plans rather than only reacting to prompts), multi-turn (it maintains state across an extended interaction), tool-using, and adaptive (it revises its strategy based on feedback).
