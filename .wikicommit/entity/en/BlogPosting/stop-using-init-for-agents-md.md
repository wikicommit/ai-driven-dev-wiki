---
title: "Stop Using /init for AGENTS.md"
type: "schema:BlogPosting"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agents-md/'
    hash: sha256:ee43d2eb32e588d7c7bbadd7d7913c23bca92a53f6a8f01113bcb23e8b12d029
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "An argument, drawing on two 2026 research papers, that auto-generated AGENTS.md files hurt agent performance and cost while human-written ones help only when they record information an agent cannot already discover by reading the codebase."
  author: "Addy Osmani"
  datePublished: "2026-02-23"
---

This post argues against running `/init` to auto-generate an [[DefinedTerm/agents-md]] file, on the grounds that auto-generated context files mostly duplicate what an agent can already discover by reading a repository, which adds cost without improving results. It contrasts two 2026 papers with opposite-seeming findings and argues the difference comes down to what the file actually contains: a human-authored file recording non-discoverable, operationally significant facts helps, while an LLM-generated codebase overview is redundant noise.

The post further argues that even a well-written, non-redundant `AGENTS.md` is a static file applied to dynamic tasks, and proposes a three-layer alternative architecture (a minimal routing "protocol" file, task-scoped persona/skill files loaded selectively, and a maintenance subagent that keeps the protocol file accurate), while noting that no major coding agent yet exposes the lifecycle hooks needed to build it.

## Key Points

- A paired experiment described in the post (Lulla et al., ICSE JAWs 2026, across 124 real GitHub pull requests) found that having an `AGENTS.md` file present reduced median wall-clock runtime by 28.64% and output token consumption by 16.58%, holding everything else constant, but the post notes this study measured only efficiency, not output correctness.
- A separate study described in the post (from ETH Zurich, across four agents on SWE-bench and a custom benchmark) found that LLM-generated context files reduced task success by 2-3% while increasing cost by over 20%, whereas developer-written files improved success by about 4% while increasing cost by up to 19%.
- The post reports that the ETH Zurich study, after stripping all existing documentation from the test repos, found that the same LLM-generated context files then improved performance by 2.7% — used to argue the auto-generated content is not useless, only redundant with documentation the agent could otherwise find itself.
- The post reports the ETH Zurich study's finding that when a developer-written file mentioned the tool `uv`, agents used it 1.6 times per task on average versus fewer than 0.01 times when it wasn't mentioned, offered as a concrete example of what belongs in the file: information the agent could not otherwise infer or guess by convention.
- An "anchoring effect" is described: mentioning a technology in `AGENTS.md`, even in passing, keeps it in the model's context on every prompt, which can bias the agent toward an outdated pattern if that technology is no longer the current convention.
- The post reports the ETH Zurich study's finding that 100% of one model's and 99% of another's auto-generated context files consisted of codebase overviews — content it argues an agent can already discover on its own.
- [[DefinedTerm/agentic-context-engineering]] (ACE, ICLR 2026) is cited as a framework that treats context as an evolving playbook maintained through a generator/reflector/curator pipeline, reported to outperform static context approaches by 12.3% on agent benchmarks.
- Results from Arize AI's own prompt-learning optimization work on Claude.md instructions are cited: a reported +5.19% accuracy improvement on a cross-repo test split and +10.87% on an in-repo split, from an automated loop that runs an agent, evaluates its output, and refines instructions from the failures.
- The post proposes a three-layer alternative to a single monolithic `AGENTS.md`: a minimal routing "protocol" file, focused persona/skill files loaded selectively by task type, and a maintenance subagent whose job is keeping the protocol file accurate as the codebase changes — while noting that no major coding agent currently exposes the lifecycle hooks needed to build this cleanly.

## Context

The post explicitly draws on two named 2026 papers (a Lulla et al. paper at ICSE JAWs, and a separate ETH Zurich study) for its efficiency and correctness claims, and states plainly that neither paper tests the hierarchical, dynamically-loaded architecture it goes on to propose. That three-layer architecture is presented not as the author's own invention but as an idea several people in the AGENTS.md discourse have independently converged on — something the post reports and organizes rather than something either paper measured.
