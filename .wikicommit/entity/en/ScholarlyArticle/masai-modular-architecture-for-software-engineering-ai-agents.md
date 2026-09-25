---
title: "MASAI: Modular Architecture for Software-engineering AI Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, agent-architecture, software-engineering, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2406.11638'
    hash: sha256:3568f52d7c2620f8fee514720c61b18a5338c4c2ade0fe9a0c79c623cfe2258f
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Microsoft Research India paper proposing MASAI, an architecture in which LLM-powered sub-agents with well-defined objectives and separately tuned strategies are composed to resolve repository-level issues, reported as reaching a 28.33% resolution rate on SWE-bench Lite."
  author: ["Daman Arora", "Atharv Sonwane", "Nalin Wadhwa", "Abhav Mehrotra", "Saiteja Utpala", "Ramakrishna Bairi", "Aditya Kanade", "Nagarajan Natarajan"]
  abstract: "Inspired by the common practice of dividing a complex software engineering problem into sub-problems, the authors propose a Modular Architecture for Software-engineering AI (MASAI) agents, where different LLM-powered sub-agents are instantiated with well-defined objectives and strategies tuned to achieve those objectives. They list three advantages: employing and tuning different problem-solving strategies across sub-agents, enabling sub-agents to gather information from different sources scattered throughout a repository, and avoiding unnecessarily long trajectories which inflate costs and add extraneous context. MASAI achieved a 28.33% resolution rate on SWE-bench Lite, 300 GitHub issues from 11 Python repositories, which the authors report as the highest performance on that dataset, and they evaluate MASAI against other agentic methods and analyse the effect of their design decisions."
---

This paper from Microsoft Research India starts from the way software engineers handle a complex
coding problem: they break it down into sub-problems and deal with each using a different strategy.
The authors argue that, as problem complexity grows, a single over-arching strategy that works
across the board becomes hard to devise, and propose MASAI, a Modular Architecture for
Software-engineering AI agents. Rather than treating issue resolution as one long chain of reasoning
and actions, MASAI divides it among LLM-powered sub-agents, each specified by an input, a
problem-solving strategy — such as vanilla completion, [[DefinedTerm/chain-of-thought]],
[[DefinedTerm/react-prompting]] or RAG — and an output specification. Sub-agents are composed by
passing one sub-agent's output to another's input; the authors describe this as simpler than
multi-agent frameworks such as AutoGen, [[SoftwareApplication/chatdev]] and
[[SoftwareApplication/metagpt]], because it does not require one-to-one or group conversations
between sub-agents.

For repository-level issue resolution the paper instantiates five sub-agents. A Test Template
Generator (ReAct) works out how to write and run a new test in the repository; an Issue Reproducer
(ReAct) uses that template to write a test reproducing the reported issue; an Edit Localizer
(ReAct) navigates the repository to find the code locations to edit; a Fixer (chain of thought),
given no environment actions, proposes multiple candidate patches as minimal rewrites that are
located in the file by line numbers with fuzzy matching; and a Ranker (chain of thought) runs the
reproduction test on each patch and ranks the patches by how likely they are to resolve the issue.
The sub-agents act on the repository through a small action space: READ, which returns a lazy
representation of a file, class or function, EDIT, ADD, WRITE, LIST, COMMAND for shell commands,
and DONE.

Evaluated on SWE-bench Lite with GPT-4o in every sub-agent, MASAI resolves 28.33% of the issues,
which the paper reports as the highest resolution rate among the methods it compares, tied with
CodeR. The rest of the paper analyses where that comes from — fault localization, sampling and
ranking of candidate patches, issue reproduction, and the representation used for edits — and the
authors contributed their results to the SWE-bench Lite leaderboard for validation.

## Key Points

- MASAI composes sub-agents that each have a well-defined objective and a strategy tuned to it, instead of one long trajectory; the authors credit this with allowing different strategies per sub-agent, gathering information from different parts of a repository, and avoiding long trajectories that inflate cost and add extraneous context.
- The issue-resolution instantiation uses five sub-agents: Test Template Generator, Issue Reproducer, Edit Localizer, Fixer and Ranker, the first three using ReAct and the last two chain of thought.
- On SWE-bench Lite (300 GitHub issues from 11 Python repositories), MASAI reports a 28.33% resolution rate, a 75% file-level localization rate and a patch application rate above 95%, at an average cost of 1.96 USD per issue with GPT-4o.
- The Edit Localizer's 75% localization rate is compared with 61% and 63% for SWE-agent and OpenDevin, methods that do not use a separate localization sub-agent.
- Sampling five candidate patches from the Fixer raises the oracle resolution rate from 23.33% with one sample to 35%, but an LLM choosing among them without a test reaches only 23.33%; ranking with the generated reproduction test reaches 28.33%.
- Test reproduction is split into two steps — generating a repository-specific test template, then an issue-specific test — to cope with repositories that use uncommon testing frameworks.
- The paper argues MASAI works at a high level of autonomy, relying only on the original SWE-bench Lite setup, whereas some compared methods use extra inputs such as hints text or pre-determined test commands.

## Notes

The evaluation is confined to SWE-bench Lite, and the authors note that its issues are limited to
those that can be validated with tests and that its issue descriptions are all in English. All
sub-agents were instantiated with GPT-4o for time and cost reasons, so the paper does not compare
different LLMs on a fixed strategy, although the architecture permits a different model per
sub-agent. On broader concerns, the authors note that agents able to run shell commands can cause
unintended side effects on the user's system, which guardrails and sandboxing can mitigate, and
that code changes suggested by such a tool should be reviewed by expert developers before being
deployed. Evaluation on SWE-bench Lite places the work alongside [[Dataset/swe-bench]] and
[[DefinedTerm/software-issue-resolution]].
