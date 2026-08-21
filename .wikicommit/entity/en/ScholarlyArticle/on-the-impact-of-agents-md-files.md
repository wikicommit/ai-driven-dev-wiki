---
title: "On the Impact of AGENTS.md Files on the Efficiency of AI Coding Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, configuration, empirical-study, metrics, context-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2601.20404'
    hash: sha256:a73a7d48c7792ddb34e456bd8a12088273326af22933553ee5bf51dfcf545cc2
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A paired within-task experiment at ICSE JAWs 2026 running an AI coding agent over 124 pull requests from 10 repositories with and without the repository's own root AGENTS.md file. It reports a 28.64% lower median wall-clock runtime and 16.58% lower median output-token consumption with the file present, and is explicit that it measures efficiency only, not correctness."
  author:
    - "Jai Lal Lulla"
    - "Seyedmoein Mohsenimofidi"
    - "Matthias Galster"
    - "Jie M. Zhang"
    - "Sebastian Baltes"
    - "Christoph Treude"
  datePublished: "2026-01"
---

"On the Impact of AGENTS.md Files on the Efficiency of AI Coding Agents" is a short empirical paper by six authors across Singapore Management University, Heidelberg University, the University of Bamberg, and King's College London, presented at ICSE JAWs 2026 (Rio de Janeiro, 12–18 April 2026) and received 23 January 2026.

Its stated gap is that prior research has concentrated on interaction-level prompt engineering and agent planning strategies, "while less attention has been paid to persistent, repository-level artifacts that encode project-specific knowledge." The question it asks is narrower than whether such files improve agent output: it asks what they cost, in runtime and tokens.

The design is a **paired within-task** comparison. Each task is a real merged pull request, replayed from the repository state immediately before the merge, run twice — once with the repository's own root [[DefinedTerm/agents-md]] file as it existed at that commit, and once with that single file removed and everything else unchanged. This holds repository, task, codebase state, and agent configuration fixed and varies only the file's presence.

## Key Contributions

- **Both efficiency measures improve, and the two improve differently.** With the file present, mean wall-clock time to completion falls from 162.94s to 129.91s (20.27%) and median from 98.57s to 70.34s (**28.64%**); mean output tokens fall from 5,744.81 to 4,591.46 (20.08%) and median from 2,925 to 2,440 (**16.58%**). Both wall-clock time and output tokens are reported as statistically significant under a Wilcoxon signed-rank test at p < 0.05.
- **The shape of each effect differs, and the authors read it carefully.** For output tokens the mean improves considerably more than the median, which they take to suggest the file "primarily reduces token usage in a small number of very high-cost runs, rather than uniformly lowering token consumption across all task instances." For wall-clock time the mean and median improvements align closely, which they read as "a general shift toward faster task completion" rather than a few extreme runs.
- **Input tokens barely move, and the medians go the wrong way.** Mean input tokens fall 9.73% and cached input tokens 9.97%, but the medians are essentially unchanged or slightly *higher* — median input tokens rise by 3,978 (−3.41%) and median total tokens by 2,875 (−1.29%). Only wall-clock time and output tokens are marked statistically significant.
- **A hypothesis for the mechanism, offered as speculation.** The authors write that they "speculate that some of the efficiency gains reported in this paper arise because AGENTS.md files describe repository structure and conventions upfront, reducing the need for agents to infer project organization through exploratory navigation," and name analysing execution traces — fewer planning iterations, less exploratory navigation, fewer repeated model requests — as the way to test it.

## Notes

The setup is unusually explicit about its own constraints. The agent is OpenAI Codex on `gpt-5.2-codex`, held constant throughout. Repositories come from a prior corpus on agent-instruction-file adoption and are filtered in two stages. First, to the simplest configuration — exactly one `AGENTS.md` at the repository root — to avoid confounding from overlapping or conflicting instruction files, which yields 89 repositories from 132. Second, on the file's content, keeping only those whose root file covers conventions and best practices, architecture and project structure, or a project description, classified with a local LLM (`gpt-oss-120b` run through Ollama) and then manually verified, which leaves 26. From those, 10 were randomly sampled with up to 15 merged PRs each, giving 124 pull requests. PRs are restricted to small-scope, code-changing contributions that post-date the introduction of the instruction file, which the authors say reduces variance from large refactorings and avoids skew from documentation-only updates or version bumps. Runs happen in isolated per-repository Docker containers with no state reused between tasks.

The most important limitation is one the paper states plainly: "A comprehensive evaluation of the output quality, e.g., the semantic correctness or the functional equivalence to the merged PR, is beyond the scope of this paper." What was done instead is a manual sanity check on 50 randomly sampled PR tasks, comparing agent outputs against the human-written merged pull requests to confirm they produced non-empty, non-trivial code changes consistent with the intended task rather than aborted runs or random edits. The authors are careful that this "does not constitute a full correctness evaluation."

That boundary matters for how the result should be read alongside other evidence on context files. This study finds that a root instruction file makes an agent *cheaper and faster* on small, real tasks; it does not find that the agent does better work. The agentfiles study summarised in [[BlogPosting/skill-issue-harness-engineering-for-coding-agents]] reaches an apparently opposite conclusion on cost — reporting that agents spent more reasoning tokens processing context-file instructions without improving resolution rates — but measures a different quantity on a different task distribution, and neither study measures both cost and correctness at once. The other stated threats are agent stochasticity, dependence on the specific agent framework and model, and the restriction to small changes; the authors name replication across more repositories, larger and more diverse pull requests, and multiple agent systems and model families as future work, along with moving beyond a binary present/absent treatment to examine how a file's specificity, organization, and workflow guidance relate to outcomes.
