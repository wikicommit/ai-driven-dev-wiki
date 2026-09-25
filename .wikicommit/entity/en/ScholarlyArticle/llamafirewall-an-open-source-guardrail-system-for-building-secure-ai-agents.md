---
title: "LlamaFirewall: An open source guardrail system for building secure AI agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [security, prompt-injection, guardrails, agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2505.03574'
    hash: sha256:0900d1fe1156d88f445d11ba287178f12bfb25c5db87cc4a10cea036ac7a7ac5
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Meta paper introducing LlamaFirewall, an open-source, security-focused guardrail framework intended as a final layer of defense for LLM agents against prompt injection, agent misalignment and insecure code."
  author: ["Sahana Chennabasappa", "Cyrus Nikolaidis", "Daniel Song", "David Molnar", "Stephanie Ding", "Shengye Wan", "Spencer Whitman", "Lauren Deason", "Nicholas Doucette", "Abraham Montilla", "Alekhya Gampa", "Beto de Paola", "Dominik Gabi", "James Crnkovich", "Jean-Christophe Testud", "Kat He", "Rashnil Chaturvedi", "Wu Zhou", "Joshua Saxe"]
  datePublished: "2025-04-29"
  abstract: "LLMs have evolved into autonomous agents that edit production code, orchestrate workflows and take higher-stakes actions based on untrusted inputs, introducing security risks that model fine-tuning and chatbot-focused guardrails do not fully address. The authors introduce LlamaFirewall, an open-source security-focused guardrail framework designed as a final layer of defense against security risks associated with AI agents, mitigating prompt injection, agent misalignment and insecure code through three guardrails: PromptGuard 2, a universal jailbreak detector; Agent Alignment Checks, a chain-of-thought auditor that inspects agent reasoning for prompt injection and goal misalignment, which is still experimental; and CodeShield, an online static analysis engine aimed at preventing coding agents from generating insecure or dangerous code. It also includes customizable scanners based on regular expressions or LLM prompts. LlamaFirewall is used in production at Meta."
---

This paper from Meta argues that, as LLMs turn into autonomous agents that write code, orchestrate
workflows and act on untrusted inputs such as web pages and emails, security infrastructure has not
kept pace: much existing work moderates chatbot content, and proprietary safety systems built into
model APIs offer limited visibility, auditability and customization. Given that no deterministic
solution exists for these risks, the authors call for a real-time guardrail monitor that serves as a
final layer of defense and supports system-level, use-case-specific policies.

Their answer is [[SoftwareApplication/llamafirewall]], an open-source framework that combines three
guardrails in a policy engine where developers can build pipelines, define remediation strategies
and plug in new detectors. PromptGuard 2 is a fine-tuned BERT-style classifier for direct
[[DefinedTerm/jailbreaking]] attempts; AlignmentCheck is an experimental auditor that uses an LLM to
inspect an agent's chain of thought and actions for signs that [[DefinedTerm/indirect-prompt-injection]]
has hijacked its goal; and CodeShield is a static-analysis engine for insecure LLM-generated code.
The paper walks through two scenarios — a travel agent whose goal is hijacked by a poisoned web
page, and a coding agent that picks up an insecure SQL pattern — to show the layers engaging only
when needed.

The evaluations use a private jailbreak benchmark, the public [[Dataset/agentdojo]] benchmark, and
an in-house goal-hijacking benchmark built in Meta's agentic simulation framework. The authors
compare the framework's role to Snort, Zeek or Sigma in traditional security: a shared, open
foundation for policies and detectors.

## Key Points

- The paper groups agent security risks into direct and indirect universal jailbreak prompt injections, insecure coding practices, and malicious code introduced via prompt injection, and maps each to the scanners that cover it.
- PromptGuard 2 comes in an 86M-parameter model based on mDeBERTa-base and a 22M-parameter model based on DeBERTa-xsmall; its scope was narrowed from PromptGuard 1's broader goal-hijacking detection to explicit jailbreak techniques, because the broader scope caused excessive false positives.
- On the authors' out-of-distribution jailbreak benchmark, PromptGuard 2 86M reaches 97.5% recall at a 1% false positive rate in English, against 21.2% for PromptGuard 1.
- The authors describe AlignmentCheck as, to their knowledge, the first open-source guardrail to audit an LLM's chain of thought in real time for injection defense.
- On the in-house goal-hijacking benchmark, AlignmentCheck backed by large models such as Llama 4 Maverick and Llama 3.3 70B achieved over 80% recall with a false positive rate below 4% without fine-tuning; smaller models had higher false positive rates.
- On AgentDojo, the baseline attack success rate of 17.6% fell to 7.5% with PromptGuard 2 86M alone, to 2.89% with AlignmentCheck alone, and to 1.75% with both combined, while task utility fell from 47.7% to 47.0%, 43.1% and 42.7% respectively.
- The authors note that AgentDojo focuses on a narrow class of attacks, so PromptGuard alone may not suffice in more varied adversarial settings.
- CodeShield uses a two-tier scan in which, in internal production deployments, about 90% of inputs are resolved by a fast first tier; evaluated in CyberSecEval 3, it reached 96% precision and 79% recall in identifying insecure code.

## Notes

The authors acknowledge that CodeShield is not comprehensive and may miss nuanced or
context-dependent vulnerabilities, that AlignmentCheck needs large, capable models and adds latency,
and that AlignmentCheck can itself be targeted by injections aimed at the guardrail model, which they
mitigate by passing it only the agent's reasoning and actions rather than raw tool outputs and by
pre-scanning its inputs with PromptGuard. The paper states the number of languages CodeShield covers
as eight in its introduction and seven in its evaluation section. Future work listed includes
multimodal agents, lower latency through model distillation, broader threat coverage such as
malicious code execution and unsafe tool use, and more realistic agent benchmarks. The paper
compares LlamaFirewall with other guardrail frameworks including
[[SoftwareApplication/nemo-guardrails]], [[SoftwareApplication/guardrails-ai]] and Invariant Labs'
framework, and positions it as a defense against [[DefinedTerm/prompt-injection]] within the broader
practice of [[DefinedTerm/guardrails]].
