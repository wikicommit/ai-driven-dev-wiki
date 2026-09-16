---
title: "The New Software Lifecycle"
type: "schema:BlogPosting"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/new-sdlc-vibe-coding/'
    hash: sha256:2b7eef861936103711a0ad32f7cb0b06602f71701457350ca6e1e37687c85c0e
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A commentary on a Google whitepaper the author co-wrote, picking out the ideas the author considers most consequential: the model-plus-harness framing, static-versus-dynamic context as a cost lever, output versus trajectory evaluation, and how each SDLC phase's bottleneck changes under AI assistance."
  author: "Addy Osmani"
  datePublished: "2026-06-16"
---

This post highlights the parts the author considers most important from "The New SDLC With Vibe Coding," a Google whitepaper he co-wrote with Shubham Saboo and Sokratis Kartakis. Rather than summarizing the whole paper, it picks out ideas the author keeps returning to: that an agent is roughly 10% model and 90% harness, that the boundary between static and dynamic context is a financial lever as much as a technical one, that verification (not AI use itself) is what separates vibe coding from agentic engineering, and that each phase of the software lifecycle compresses unevenly under AI assistance.

## Key Points

- The paper's rough split of an agent into "10% model, 90% harness" is cited alongside two public benchmark results: one team moved a coding agent from outside the Terminal Bench 2.0 top 30 into the top 5 by changing only the harness, and a separate LangChain experiment added 13.7 points on the same benchmark by changing only the system prompt, tools, and middleware — in both cases with the same underlying model.
- The paper sorts agent context into six types (instructions, knowledge, memory, examples, tools, guardrails) and splits them into static context (loaded every turn: system instructions, rule files, global memory — reliable but expensive) versus dynamic context (loaded on demand: skills, tool results, RAG documents — cheaper per turn), and recommends treating that boundary as an architectural decision reviewed like code.
- The paper distinguishes output evaluation (is the final result correct) from [[DefinedTerm/trajectory-evaluation]] (was the path taken — the tool calls and reasoning — sound), and the post argues both are needed since a result that looks right but skipped its checks is more dangerous than one that's obviously broken.
- Citing a METR study, the post reports experienced developers went about 19% slower on some tasks with AI assistance once time spent checking and fixing is counted, alongside separate survey estimates of a 25-39% productivity gain — both of which it treats as true simultaneously, summarizing that AI turns implementation from writing into reviewing.
- The paper models total cost of ownership as two diverging curves: vibe coding starts with low upfront cost but accumulates a "prompting tax," token burn, maintenance tax, and security cleanup cost, while agentic engineering costs more upfront but flattens out; the post describes the crossover point, after which vibe coding is illustrated as costing 3 to 10 times more per feature, as illustrative rather than a measured constant.
- It reports adoption figures from the paper: as of early 2026, 85% of professional developers use AI coding agents regularly, 51% daily, and roughly 41% of new code is AI-generated.
- It names Google's Agents CLI as an example of the same terminal coding-agent workflow being extended to build, evaluate, and deploy a persistent, permission-scoped production agent, coordinating with other agents over MCP (for tools) and A2A (for handing off work).
- It attributes a conductor/orchestrator distinction to the paper: the conductor is real-time, in-IDE, and good for unfamiliar code; the orchestrator is asynchronous, goal-delegated, and good for well-specified work like migrations or test generation.

## Context

The post is explicitly a personal selection from a paper the author co-wrote rather than a summary of it, and states plainly that it omits the paper's opening material (definitions of agents and vibe coding) on the grounds that readers of the blog already know it. The METR study finding and the adoption percentages are attributed to the whitepaper or to studies it cites rather than presented as the author's own findings; the two harness benchmark results (Terminal Bench top-30-to-top-5, the LangChain +13.7-point result) are public numbers the post itself adds to illustrate the paper's 90%-harness claim, rather than figures the post states the paper itself contains.
