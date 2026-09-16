---
title: "AIShellJack"
type: "schema:SoftwareApplication"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.22040'
    hash: sha256:da47527629d5433a620dfbe28d8c5d8575458110097f9a4224bd51dd13875a52
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "An open-source, academic security-research framework and benchmark of 314 prompt-injection attack payloads covering 70 MITRE ATT&CK techniques, built to systematically evaluate whether agentic AI coding editors can be hijacked into executing unauthorized terminal commands."
  applicationCategory: "AI agent security benchmark"
---

AIShellJack is an automated evaluation framework and benchmark for testing whether agentic AI coding editors can be hijacked, via prompt injection embedded in external development resources, into executing unauthorized terminal commands. It was built for academic security research into two coding editors' (Cursor and GitHub Copilot) vulnerability to this class of attack, and its reproduction package has been published by its authors.

## Capabilities

The framework contains 314 distinct attack payloads covering 70 techniques drawn from 11 categories of the MITRE ATT&CK framework, adapted from the open-source atomic-red-team security-testing library (originally built for validating antivirus and security-monitoring detection capabilities). Payload descriptions are manually revised to remove explicit adversarial terminology while preserving the underlying command's technical intent, so that the payloads simulate a realistic attacker's disguised instructions rather than an obviously-malicious request. The framework includes a simulation engine that standardizes how attack payloads are injected (via coding-rule files) across different editors and codebases, and an automated, semantics-based matching algorithm that determines whether an injected command both executed and achieved its intended effect, reported to reach 99.1% accuracy in identifying successful attacks, validated against a manually-reviewed sample.

## Adoption & Ecosystem

The framework was used to evaluate Cursor and GitHub Copilot running Claude 4 Sonnet and Gemini 2.5 Pro across five real-world codebases spanning TypeScript, Python, C++, and JavaScript, finding attack success rates from 41.1% to 84.1% depending on the editor/model combination.
