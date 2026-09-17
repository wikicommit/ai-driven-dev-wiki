---
title: "AgentDojo"
type: "schema:Dataset"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2406.13352'
    hash: sha256:2c9c613f09075c0bfe05bf53bbf1993749267f8bf72bff9ba1f5651d007d1fff
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "An extensible benchmark environment for evaluating tool-calling AI agents' utility and robustness to prompt injection, populated with four task suites (Workspace, Slack, Travel, Banking) totaling 97 user tasks, 27 injection tasks, and 629 security test cases, introduced in the AgentDojo paper."
  creator: ["Edoardo Debenedetti", "Jie Zhang", "Mislav Balunovic", "Luca Beurer-Kellner", "Marc Fischer", "Florian Tramèr"]
  url: "https://agentdojo.spylab.ai"
---

AgentDojo is a benchmark environment, introduced in [[ScholarlyArticle/agentdojo]], for evaluating the utility and prompt-injection robustness of tool-calling AI agents. Rather than a fixed test suite, it is designed as an extensible framework that can be populated with new environments, tools, attacks, and defenses over time.

## Contents

Each of AgentDojo's four environments (Workspace, Slack, Travel, and Banking) models a stateful application domain — for example, the Workspace environment tracks an email inbox, a calendar, and a cloud drive as mutable Python objects — and exposes a set of tools that read and write that state. A user task is a natural-language instruction paired with a utility function that inspects the model's output and the environment-state changes to determine whether the agent solved it correctly, along with a ground-truth sequence of tool calls. An injection task specifies an attacker's goal (e.g. exfiltrating data) paired with its own security-check function and ground-truth function-call sequence. The collection of user and injection tasks for one environment forms a task suite, and the security test cases for that suite are formed by taking the cross-product of its user and injection tasks. Across its four environments, the first version of AgentDojo totals 97 user tasks, 27 injection tasks, and 629 security test cases; running a user task without any injection present also serves as a benign utility test case.

## Provenance

AgentDojo was created by researchers at ETH Zurich and Invariant Labs and is published at agentdojo.spylab.ai. It is implemented as a Python package: environments, tools, user tasks, injection tasks, attacks, and agent-defense pipelines are each added as code following the framework's component interfaces, so the benchmark can be extended with new environments, tasks, attacks, and defenses without changing its core design.

## Use

[[ScholarlyArticle/agentdojo]] uses this benchmark to evaluate a range of closed- and open-source tool-calling agents, several prompt injection attack phrasings and an adaptive attack, and four prompt-injection defenses, reporting utility and attack-success-rate results for each.
