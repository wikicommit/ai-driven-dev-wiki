---
title: "RepairAgent: An Autonomous, LLM-Based Agent for Program Repair"
type: "schema:ScholarlyArticle"
lang: en
tags: [program-repair, coding-agents, tool-calling, debugging]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2403.17134'
    hash: sha256:aafce2ddc1642de21ae7f1c9a81dae3d270cea048a82a78f1d2819b04e881cc1
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paper from the University of Stuttgart and UC Davis introducing RepairAgent, which its authors present as the first autonomous LLM-based agent for automated program repair. The LLM decides which of 14 repair-related tools to invoke, guided by a dynamically updated prompt and a finite state machine; on Defects4J it correctly fixes 164 bugs, 39 of them not fixed by prior techniques."
  author: ["Islem Bouzenia", "Premkumar Devanbu", "Michael Pradel"]
  keywords: ["automated program repair", "LLM-based agents", "tools", "Defects4J", "finite state machine"]
---

The paper situates itself in [[DefinedTerm/automated-program-repair]], where it describes the current state of the art as dominated by LLMs used either in a one-time interaction or in iterative approaches with a hard-coded feedback loop. Its criticism of the latter is that the fixed loop gives the model only the code context provided in the prompt and lets it neither gather information about the bug nor search for code that might supply ingredients for a fix — unlike human developers, who interleave understanding the bug, searching helpful code and experimenting with candidate fixes. RepairAgent instead treats the LLM as an autonomous agent that plans and executes actions by invoking tools, and the authors state that, to their knowledge, it is the first autonomous LLM-based agent for program repair.

The approach has three components. The LLM agent (GPT-3.5 in the evaluation) is queried once per cycle with a dynamic prompt whose static sections give its role, goals and guidelines — including a list of recurring fix patterns — and whose dynamic sections carry the current state, the available tools, the information gathered so far and the last command's result. The 14 tools cover reading and extracting code, searching the code base and generating a method body with another LLM call, running tests and fault localization, writing a fix, and control commands for expressing or discarding a hypothesis. A middleware parses and heuristically corrects the LLM's output, rejects exact repeats of earlier commands, runs tools in an isolated environment, and updates the prompt. A finite state machine with three states — understand the bug, collect information to fix it, and try to fix it — limits which tools are available at a given time, without enforcing a strict order.

## Key Points

- Applied to all 835 bugs in [[Dataset/defects4j]], RepairAgent produces plausible fixes for 186 bugs and correct fixes for 164 (74 in v1.2 and 90 in v2.0); of the correct fixes, 116 match the developer fix exactly and 48 are semantically consistent with it.
- ChatRepair had previously fixed 162 bugs on Defects4J; RepairAgent fixes 39 bugs that none of the three baselines (ChatRepair, ITER, SelfAPR) fixed, and does particularly well on Defects4J v2 (90 vs. 48 for ChatRepair) and on bugs needing more than a single-line fix (46 multi-line and 3 multi-file correct fixes).
- It sometimes proposes complex fixes where a simple modification would do, and so misses some single-line bugs that ChatRepair fixes; on multi-line and multi-file bugs it often edits only a subset of the required locations.
- The median cost per bug is about 270,000 tokens, about 14 US cents at GPT-3.5 pricing, with a median time of 920 seconds, 99% of it spent executing tools, mostly tests; fixed bugs consumed far fewer tokens (21,000) than unfixed ones (315,000).
- In an ablation on 100 bugs, removing the search tools halved the correct fixes (11 vs. 21) and roughly doubled the cost, removing the state machine left the agent often proposing a fix without collecting information, and keeping gathered information for only one cycle led it to repeat commands; with realistic GZoltar-based fault localization instead of perfect localization it fixed 16 bugs.
- On 100 bugs sampled from GitBug-Java, all fixed in 2023 after the model's training cutoff, it correctly fixes 13, including 9 of 19 single-line bugs but only 4 of 81 multi-line or multi-file bugs; the authors conclude that it generalizes and is not strongly affected by data leakage, attributing the weaker multi-line results to GitBug-Java's more complex bugs.

## Notes

On average the agent makes 35 tool invocations per bug, the most frequent being `write_fix`, which samples up to 30 variants of a proposed patch and reverts the changes when tests fail. The authors list threats to validity including possible data leakage from GPT-3.5's training data, Defects4J's guarantee of at least one failing test case per bug, fault localization accuracy, and LLM non-determinism, and suggest human-in-the-loop use of partial fixes as future work. The implementation is built on the AutoGPT framework. They note that other LLM-based agents for software engineering tasks were proposed after an initial version of the paper was made public.
