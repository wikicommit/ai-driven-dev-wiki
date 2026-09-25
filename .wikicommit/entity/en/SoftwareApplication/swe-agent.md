---
title: "SWE-Agent"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-agents, llm, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2508.11126'
    hash: sha256:d8a0f4c103987a46e21f37fca41b5ebfa795945e9c798921c4fdfbfc18bd9346
  - type: url
    url: 'https://arxiv.org/abs/2405.15793'
    hash: sha256:ebb2c6da508182de8f896253125e9ab51d33562a0f61627a99fbb416053c71ec
  - type: url
    url: 'https://github.com/SWE-agent/SWE-agent'
    hash: sha256:c3880592057d87cf91991b5a2b1de6679aed5da5a6ac17d0c891eb8638ed9757
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A system that lets language model agents autonomously use computers to solve software engineering tasks, built around a custom agent-computer interface for creating and editing code files, navigating repositories, and running tests and other programs."
  applicationCategory: "Coding agent"
---

SWE-Agent is a system that facilitates language model agents in autonomously using computers to
solve software engineering tasks. The paper that introduces it,
[[ScholarlyArticle/swe-agent-agent-computer-interfaces-enable-automated-software-engineering]],
presents it as the outcome of an investigation into how interface design affects the performance of
language model agents, built on the premise that LM agents are a new category of end users who
benefit from interfaces built specifically for them.

The project's GitHub repository describes it as an academic project started at Princeton University
and now built and maintained by researchers from Princeton University and Stanford University,
released under the MIT license. Its README presents SWE-Agent as letting a language model of the
user's choice autonomously use tools to fix issues in real GitHub repositories, find cybersecurity
vulnerabilities, or perform custom tasks. The same README now carries a warning that most of the
team's current development effort is on mini-swe-agent, which it says has superseded SWE-Agent,
matching its performance while being much simpler, and it recommends using mini-SWE-agent instead
going forward.

## Capabilities

The introducing paper identifies SWE-Agent's custom [[DefinedTerm/agent-computer-interface]] (ACI)
as the component that does the work, stating that it significantly enhances an agent's ability to
create and edit code files, navigate entire repositories, and execute tests and other programs. The
same paper reports SWE-Agent reaching state-of-the-art performance on [[Dataset/swe-bench]] and
HumanEvalFix, at pass@1 rates of 12.5% and 87.7% respectively, which it describes as far exceeding
the previous state of the art achieved with non-interactive language models. Those figures are
results measured in that paper rather than standing properties of the system.

The repository's README characterises the tool in its own terms: free-flowing and generalizable,
leaving maximal agency to the language model; configurable and fully documented, with its behaviour
governed by a single YAML file; and made for research, simple and hackable by design. It names GPT-4o
and Claude Sonnet 4 as examples of models it can drive, and announces a 1.0 release. The repository
also documents **EnIGMA**, a SWE-Agent mode for solving offensive cybersecurity capture-the-flag
challenges, and advises using SWE-Agent 0.7 for it while EnIGMA is updated for 1.0.

A survey on AI agentic programming gives a different account of the system's internals: it describes
SWE-Agent as a multi-agent coding system that divides a software engineering task among
role-specific LLM agents — an "Architect" for high-level design, a "Coder" for implementation, and a
"Reviewer" for quality assurance — connected through structured dialogue and shared memory. That
survey reports SWE-Agent as using GPT-4 as its underlying model with a 16,000-token default context
window, and as supporting persistent memory across a task by retrieving tool outputs and plan state
from a vector database rather than relying only on what fits in its active context window.

## Adoption & Ecosystem

The same survey classifies SWE-Agent, in its comparative taxonomy of AI agentic programming systems,
as a "Multi-agent System" that is proactive (it initiates its own sub-tasks and plans rather than
only reacting to prompts), multi-turn (it maintains state across an extended interaction),
tool-using, and adaptive (it revises its strategy based on feedback).

The repository documents running SWE-Agent in batch mode for benchmarking on SWE-bench, and presents
it alongside the team's related projects, among them mini-swe-agent, the SWE-ReX and SWE-smith
projects, the sb-cli tool and SWE-bench itself.

Code, data and a demo for SWE-Agent are stated by the introducing paper to be available at
<https://swe-agent.com>.
