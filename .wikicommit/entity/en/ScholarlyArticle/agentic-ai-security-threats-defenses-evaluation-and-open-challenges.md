---
title: "Agentic AI Security: Threats, Defenses, Evaluation, and Open Challenges"
type: "schema:ScholarlyArticle"
lang: en
tags: [security, agents, prompt-injection, survey]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2510.23883'
    hash: sha256:75f2887438616fbeb497cd7a4ba2432f934fa9470415e6899cd1d35706b091f6
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A survey of the security risks specific to agentic AI systems built on large language models, organized as a taxonomy of threats, a review of defenses and security controls, a review of capability and security benchmarks, and a set of open challenges."
  author: ["Anshuman Chhabra", "Shrestha Datta", "Shahriar Kabir Nahin", "Prasant Mohapatra"]
  abstract: "Agentic AI systems powered by LLMs and endowed with planning, tool use, memory and autonomy can autonomously execute tasks across web, software and physical environments, which creates new and amplified security risks distinct from both traditional AI safety and conventional software security. The survey outlines a taxonomy of threats specific to agentic AI, reviews recent benchmarks and evaluation methodologies, discusses defense strategies from technical and governance perspectives, and highlights open challenges, aiming to support the development of secure-by-design agent systems."
  keywords: ["Agentic AI", "Security", "Threats", "Defenses", "Evaluation"]
---

This survey, by authors at the University of South Florida and carrying the DOI
10.1109/ACCESS.2026.3675554, argues that the properties that make agentic AI systems useful —
autonomy and persistence, tool integration, and coordination among agents — are also what create
security risks that neither traditional AI safety nor conventional software security fully covers.
Autonomy and persistence enlarge the attack surface, tool integration magnifies potential misuse,
and coordination among agents introduces unpredictability. The authors position the work against
existing surveys of autonomous agents, which they describe as mostly detailing capabilities and
benchmarks or treating trust and risk management without a singular focus on security.

The paper is organized in four parts: a taxonomy of threats, a review of defense approaches, a
review of benchmarks and evaluation practice, and a list of open challenges. It includes a table
mapping individual defense systems onto secure-by-design components (input governance, tool-call
guards, policy engine, sandboxing/isolation, rate limiting, audit trails, and rollback/recovery)
and a table comparing capability and security-specific benchmarks.

## Key Points

- The threat taxonomy has five categories: prompt injection and jailbreaks; autonomous
  cyber-exploitation and tool abuse; multi-agent and protocol-level threats; interface and
  environment risks; and governance and autonomy concerns. The authors state that the categories
  are not mutually exclusive but organize attacks by their primary distinguishing property.
- It calls [[DefinedTerm/prompt-injection]] the most widely discussed attack in the literature and
  classifies it along several axes: [[DefinedTerm/direct-prompt-injection]] versus
  [[DefinedTerm/indirect-prompt-injection]]; intentional versus unintentional (for example
  ambiguous user queries or contextual drift in long chats); attack modality (text, image or video,
  audio, and hybrid); propagation (non-propagating attacks versus recursive injection and
  autonomous propagation such as worms that spread across agents); multilingual and obfuscated
  injections; and payload splitting, where a malicious instruction is fragmented across benign-looking
  inputs and only takes effect when the model aggregates them.
- Autonomous cyber-exploitation is distinguished from prompt injection in that the agent itself
  identifies, organizes and carries out attacks when given code-execution or system-level tools;
  the survey groups this into exploitation of one-day vulnerabilities, autonomous website hacking,
  and emergent tool abuse, drawing on prior studies.
- For multi-agent systems it discusses protocol-level threats against the
  [[DefinedTerm/model-context-protocol]] and the [[DefinedTerm/agent2agent-protocol]], restricting
  its discussion to those two, and reorganizes cross-domain multi-agent threats from a threat actor's
  perspective into six classes: impersonation and role abuse, coordination manipulation, knowledge
  and learning manipulation, inference and policy evasion, accountability obfuscation, and
  confidential data tampering or exfiltration.
- Interface and environment risks are framed as arising from the agent's interaction with its
  operating environment rather than from its internal reasoning: observation–action space
  misalignment, perception–action fragility in realistic environments (misinterpreting prior inputs,
  premature termination, brittleness across templates), and dynamic content, localization and robot
  detection.
- Prompt-injection defenses are grouped as agent-focused (prompt engineering and runtime behavior,
  and supervised fine-tuning), user-focused (human verification signals, such as confirmation before
  sensitive actions), and system-focused (detection, isolation, prompt augmentation and quality-based
  defenses), with a further split into training-based and training-free methods. The authors
  summarize the trade-off as user-focused defenses sacrificing automation, agent-focused defenses
  risking degraded capabilities or failure against adaptive attacks, and system-focused defenses
  adding complexity, and note that practical deployments increasingly favor hybrid designs.
- Among system-focused defenses the survey lists design patterns including
  [[DefinedTerm/llm-map-reduce-pattern]], [[DefinedTerm/code-then-execute-pattern]],
  [[DefinedTerm/dual-llm-pattern]] and [[DefinedTerm/context-minimization-pattern]], and among
  agent-focused defenses the [[DefinedTerm/action-selector-pattern]] and
  [[DefinedTerm/plan-then-execute-pattern]].
- Policy filtering and enforcement is divided into governance-centric (runtime) enforcement, which
  regulates agents' actions and decision sequences directly, and signal-centric (non-runtime)
  enforcement, which scans inputs and outputs for violations. The survey also covers
  [[DefinedTerm/sandboxing]] and capability confinement, detection and monitoring, and
  organizational frameworks such as the NIST AI RMF Generative AI Profile, the OWASP Agentic AI
  Threats project and the CSA MAESTRO framework.
- On evaluation, the authors separate capability benchmarks (for example
  [[Dataset/tau-bench]]) from security- and safety-specific benchmarks (for example
  [[Dataset/agentdojo]] and [[Dataset/agent-security-bench]]), and argue that security evaluation
  should move toward process-aware scoring of trajectory segments, repeated-trial metrics reported as
  distributions rather than a single average, judges validated against humans, sandboxing and
  emulation with explicit fidelity assumptions, and reproducible configurations.
- The open challenges it lists are long-horizon security, novel multi-agent security
  considerations, improved safety and security benchmarks, tracing agent decisions efficiently and
  securely, safety against adaptive attacks, agentic AI security in the physical world, and
  human–agent security interfaces.

## Notes

The survey is a synthesis of existing research rather than a new empirical study; the attack
success rates and benchmark figures it reports are drawn from the works it cites. Its discussion
of protocol-level threats names but does not cover the [[DefinedTerm/agent-network-protocol]] and
the [[DefinedTerm/agent-communication-protocol]]. On adaptive attacks, it observes that most work
evaluates defenses for AI agents only against static attacks, and that in adversarial ML more
generally many defenses first reported as effective are undermined soon after release. Its
treatment of the human–agent boundary notes that human oversight itself can be adversarially
influenced, for example by users being socially engineered into approving unsafe actions.
