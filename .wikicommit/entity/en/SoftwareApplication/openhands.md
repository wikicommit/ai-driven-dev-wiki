---
title: "OpenHands"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-agents, llm, software-engineering, open-source]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2407.16741'
    hash: sha256:01c47d5b7e938859b4b50218e91582dfc7f340a1b2c75d210d80be48372dc1f6
  - type: url
    url: 'https://openhands.dev/blog/20260305-learning-to-verify-ai-generated-code'
    hash: sha256:672e965c31f9cb19e39209c68cf05a7789cd6435e662e2fbef87b99f6c790dfe
  - type: url
    url: 'https://openhands.dev/blog/mitigating-prompt-injection-attacks-in-software-agents'
    hash: sha256:c531528526e6141ec71ff79c2e5e157b6f4eed38552de696dcc4c7135b39d6ff
  - type: url
    url: 'https://openhands.dev/blog/openhands-context-condensensation-for-more-efficient-ai-agents'
    hash: sha256:9c162f7d2b9faa097af2bc398adfb790f05ef67863ae29034d68c30367bfb45b
  - type: url
    url: 'https://www.openhands.dev/blog/one-year-of-openhands-a-journey-of-open-source-ai-development'
    hash: sha256:95b651a75d1dfdd3495be3b52292a94e0ce96f5db80c93d75d7f6b46422ad958
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An open platform for developing AI agents that interact with the world as a human developer does — writing code, working at a command line, and browsing the web — with sandboxed code execution, multi-agent coordination and built-in evaluation benchmarks. Formerly known as OpenDevin."
  applicationCategory: "AI agent development platform"
  featureList: "Implementation of new agents; safe interaction with sandboxed environments for code execution; coordination between multiple agents; incorporation of evaluation benchmarks; a trajectory-level critic model for scoring agent attempts, available in the OpenHands Software Agent SDK and CLI; Docker-sandboxed conversations; a confirmation mode in the OpenHands CLI; a security analyzer for proposed agent actions; a context condenser that summarizes older conversation history once it passes a size threshold"
---

OpenHands, formerly known as OpenDevin, is a platform for the development of powerful and flexible
AI agents that interact with the world in similar ways to those of a human developer: by writing
code, interacting with a command line, and browsing the web. It is introduced in
[[ScholarlyArticle/openhands-an-open-platform-for-ai-software-developers-as-generalist-agents]],
which presents it against the background of rapid development in AI agents that interact with and
affect change in their surrounding environments.

It is released under the permissive MIT license, and the introducing paper describes it as a
community project spanning academia and industry, with more than 2.1K contributions from over 188
contributors at the time of writing. Its code is stated to be at
<https://github.com/All-Hands-AI/OpenHands>.

The project's first-anniversary post,
[[BlogPosting/one-year-of-openhands-a-journey-of-open-source-ai-development]], gives its origin. It
began on 12 March 2024 with the aim of creating an open-source AI agent for software development, and
was originally created as OpenDevin — an homage to [[SoftwareApplication/devin]] by
[[Organization/cognition]], which the post says inspired the project — by Binyuan Hui and Junyang Lin of
the team developing the Qwen open-source language model. The open-source community rallied around it,
and three early contributors, Graham Neubig, Robert Brennan and Xingyao Wang, went on to found
[[Organization/all-hands-ai]] to carry on its mission, at which point the project was renamed
OpenHands.

## Capabilities

The introducing paper describes four things the platform allows for: the implementation of new
agents; safe interaction with sandboxed environments for code execution; coordination between
multiple agents; and the incorporation of evaluation benchmarks.

In a March 2026 post, [[BlogPosting/learning-to-verify-ai-generated-code]], the OpenHands team
describes adding verification to this: a layered "verification stack" whose first layer is a small,
fast [[DefinedTerm/critic-model]] that scores an agent's whole trajectory, trained on real-world
production traces rather than benchmark data. The critic is integrated into the OpenHands Software
Agent SDK, where its score can be used in custom loops for reranking, early stopping or iterative
refinement, and into the OpenHands CLI, where it can be enabled with early stopping, used for
iterative refinement, and given different acceptance thresholds. The post names a second, patch-level layer as still to come.

### Context condensation

An April 2025 post, [[BlogPosting/openhands-context-condensation-for-more-efficient-ai-agents]],
introduces the OpenHands context condenser. Once a conversation grows beyond a threshold, older
interactions are summarized — encoding the user's goals, the agent's progress and what remains, and for
software tasks details such as critical files and failing tests — while recent exchanges are kept
intact. On a subset of SWE-bench Verified instances, the post reports per-turn API cost settling at
less than half the baseline agent's, with an average solve rate of 54% against the baseline's 53%. It
describes context condensation as available in OpenHands, including OpenHands Cloud.

### Security controls

An August 2025 post from the OpenHands team,
[[BlogPosting/mitigating-prompt-injection-attacks-in-software-agents]], describes how OpenHands
addresses the prompt-injection risk of an agent that typically runs without a human watching it. Every
conversation with the agent takes place inside a Docker container, so the local filesystem and
environment are kept safe even if the agent runs a destructive command, though the post notes that
secrets inside that environment, and the source code, can still be exposed. The OpenHands CLI can ask
the user for confirmation before the agent acts, and OpenHands has added a security analyzer, developed
with Invariant Labs, that assesses the actions the agent wants to take for potential threats and can
stop to ask for explicit permission or refuse to proceed. Organizations that self-host OpenHands with
its Kubernetes deployment can additionally restrict the agent inside its sandbox with network policy
and eBPF tooling. The post also reports that how readily the agent refuses a malicious instruction
depends on the model powering it.

## Adoption & Ecosystem

Because evaluation benchmarks are incorporated into the platform itself, the benchmarks it holds are
part of what it offers. The introducing paper reports an evaluation of agents over 15 challenging
tasks based on the benchmarks currently incorporated, spanning software engineering — for which it
names [[Dataset/swe-bench]] — and web browsing, for which it names WebArena, among others.

The anniversary post describes OpenHands being used both by individual developers automating routine
tasks and by large teams on complex refactoring projects. It set out four aims for the project's second
year: a general release of OpenHands Cloud, then in beta, which runs OpenHands without the user's own
server and can be used from a browser, a mobile device or GitHub; continued improvement of the agent,
both in core accuracy on benchmarks such as SWE-Bench and in the range of tasks it performs reliably;
more integrations, including a better CLI and task-management tools such as Jira and Linear; and more
customization to users' preferences, organizational policies and workflows.
