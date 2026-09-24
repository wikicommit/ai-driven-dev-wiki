---
title: "On the Impact of AGENTS.md Files on the Efficiency of AI Coding Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, context-engineering, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2601.20404'
    hash: sha256:a73a7d48c7792ddb34e456bd8a12088273326af22933553ee5bf51dfcf545cc2
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paired experiment running OpenAI Codex on 124 pull-request tasks from 10 GitHub repositories with and without the repository's root AGENTS.md file, finding lower median runtime and output token use when the file is present."
  author: ["Jai Lal Lulla", "Seyedmoein Mohsenimofidi", "Matthias Galster", "Jie M. Zhang", "Sebastian Baltes", "Christoph Treude"]
  abstract: "The paper studies how AGENTS.md files affect the runtime and token consumption of AI coding agents working on GitHub pull requests. It executes an agent on 124 pull requests from 10 repositories under two conditions, with and without an AGENTS.md file, and finds that the file's presence is associated with lower median runtime and reduced output token consumption while task completion behaviour remains comparable."
  keywords: ["AI coding agents", "AGENTS.md", "pull requests", "efficiency"]
---

This paper isolates one question about [[DefinedTerm/agents-md]] files — the repository-level instruction files developers write as "READMEs for agents" — namely whether their presence makes an [[DefinedTerm/ai-coding-agent]] more efficient. The authors observe that earlier empirical work has characterized the structure, content and evolution of such agent context files, but that none had isolated the effect of adding an AGENTS.md file on agent efficiency while holding the task, the repository and the agent architecture constant. They define efficiency as the computational resources an agent needs to complete a development task, operationalized as token usage and wall-clock time to completion.

The agent is [[SoftwareApplication/openai-codex]], run through the Codex CLI with the gpt-5.2-codex model; the authors chose it because it is designed for software engineering tasks and because AGENTS.md was first used with Codex before becoming an open format. Starting from a corpus of repositories sampled in prior work on agent instruction files, they kept only repositories with a single AGENTS.md at the root (89 of 132), then used an LLM (gpt-oss-120b) with manual verification to keep only files containing conventions and best practices, architecture and project structure, or a project description — leaving 26 repositories. From 10 of these, chosen at random, they took up to 15 merged pull requests each: small code-only changes of at most 100 lines across at most five files, created and merged after the repository introduced its AGENTS.md. For each, the repository was reset to its pre-merge state, an issue-style task description was generated from the diff and file tree, and the agent was asked to recreate the change twice in isolated Docker containers — once with the AGENTS.md from that commit and once with it removed.

The authors frame the result as initial empirical evidence that repository-level instruction files have measurable operational effects on autonomous coding agents, positioning AGENTS.md as a practical mechanism for shaping agent behaviour, and set out a research roadmap for extending the study.

## Key Points

- Across 124 pull requests, the median wall-clock time to completion fell from 98.57 s without AGENTS.md to 70.34 s with it (28.64%), and the mean from 162.94 s to 129.91 s (20.27%); the difference is statistically significant under a Wilcoxon signed-rank test.
- Because the mean and median time reductions are closely aligned, the authors read the speed-up as a general shift toward faster completion rather than an effect of a few extreme runs.
- Median output tokens fell from 2,925 to 2,440 (16.58%) and mean output tokens from 5,744.81 to 4,591.46 (20.08%), also a statistically significant difference.
- The larger reduction in mean than in median output tokens leads the authors to conclude that AGENTS.md mainly cuts token use in a small number of very high-cost runs rather than uniformly across tasks.
- Input and cached input tokens declined slightly on average (by 9.73% and 9.97%), but their medians were essentially unchanged or slightly higher with AGENTS.md, as was the median of total tokens.
- A manual check of 50 randomly sampled tasks found that the agent's outputs were non-empty, non-trivial code changes consistent with the intended task, so the efficiency differences are not explained by aborted runs or random edits — though the authors stress this is not a full correctness evaluation.
- The authors speculate, without having tested it, that some of the gain arises because AGENTS.md files describe repository structure and conventions up front, reducing the exploratory navigation an agent would otherwise need; they propose analysing execution traces to check this.

## Notes

The authors acknowledge that the study covers a sampled subset of repositories, pull requests and agent configurations, and that effects may still depend on agent stochasticity, the specific agent framework and model, and the selected tasks. Their roadmap proposes replicating the study across more repositories, larger and more diverse pull requests and other agent systems and model families; relaxing the size and scope constraints to cover larger refactorings and multi-module changes; evaluating correctness and alignment with developer intent rather than efficiency alone; and examining how properties of the files themselves — specificity, organization, inclusion of workflow guidance — relate to agent outcomes, rather than treating AGENTS.md as simply present or absent.

The paper was published in the proceedings of the Journal Ahead Workshop (JAWs) 2026 at ICSE, held in Rio de Janeiro. The version extracted here is arXiv:2601.20404v2 [cs.SE], stamped 30 March 2026. Its authors are affiliated with Singapore Management University, Heidelberg University, the University of Bamberg and King's College London.
