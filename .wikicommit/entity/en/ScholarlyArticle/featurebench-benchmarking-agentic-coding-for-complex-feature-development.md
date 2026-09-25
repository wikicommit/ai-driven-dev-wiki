---
title: "FeatureBench: Benchmarking Agentic Coding for Complex Feature Development"
type: "schema:ScholarlyArticle"
lang: en
tags: [benchmarks, evaluation, coding-agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2602.10975'
    hash: sha256:41a29ebab57dc2c90294974e352929b6c0d4706053fdba87e2ee97ba915b22f2
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An ICLR 2026 paper that introduces FeatureBench, an execution-based benchmark for feature-level agentic coding built by a test-driven pipeline that derives tasks automatically from Python repositories, and reports that frontier agents resolve only a small fraction of its tasks."
  author: ["Qixing Zhou", "Jiacheng Zhang", "Haiyang Wang", "Rui Hao", "Jiahe Wang", "Minghao Han", "Yuxue Yang", "Shuzhe Wu", "Feiyang Pan", "Lue Fan", "Dandan Tu", "Zhaoxiang Zhang"]
  abstract: "Existing agentic coding benchmarks cover a limited task scope, such as bug fixing within a single pull request, and often rely on non-executable evaluations or lack an automated way to keep evaluation coverage updated. FeatureBench evaluates agentic coding performance in end-to-end, feature-oriented software development, combining an execution-based evaluation protocol with a scalable test-driven method that automatically derives tasks from code repositories. By tracing from unit tests along a dependency graph, it identifies feature-level tasks spanning multiple commits and PRs while ensuring other features keep working after separation. The first version contains 200 evaluation tasks and 3825 executable environments from 24 open-source repositories; Claude Opus 4.5, which achieves a 74.4% resolved rate on SWE-bench, succeeds on only 11.0% of tasks."
  keywords: ["agentic coding", "benchmark", "feature development", "execution-based evaluation"]
---

This paper, published as a conference paper at ICLR 2026 by authors at the Institute of
Automation of the Chinese Academy of Sciences and Huawei Technologies, introduces
[[Dataset/featurebench]], a benchmark for coding agents that targets feature development rather
than bug fixing. The authors' motivation is that benchmarks such as [[Dataset/swe-bench]] are
dominated by bug-fixing issues — they put feature requests at only about 18–22% of SWE-bench
instances — and that pull-request-based collection methods cannot capture complete features, which
often span several PRs scattered across a project's history and are frequently untagged.

Each task gives the agent a high-level description, explicit interface definitions (import paths,
function signatures and expected behavior), a blacklist of URLs, and a Docker environment, and
requires a directly callable implementation, so that a correct solution passes the associated
fail-to-pass and pass-to-pass tests. Tasks come in two difficulty levels: Level 1, extending an
existing codebase from which the feature has been removed, and Level 2, implementing the same
functionality from scratch without the repository. The collection pipeline runs a repository's
tests, uses Python's tracing facility to build a function-level dependency graph, has an LLM pick
out the objects each test targets, traverses the graph to extract the target feature's code while
keeping what pass-to-pass tests exercise, and then verifies that the stripped codebase passes the
pass-to-pass tests, fails the fail-to-pass tests, and passes everything once the patch is
reapplied. The only manual step is specifying each repository's installation commands.

The paper evaluates seven scaffold–model combinations, including [[SoftwareApplication/openhands]],
[[SoftwareApplication/gemini-cli]], [[SoftwareApplication/claude-code]] and
[[SoftwareApplication/openai-codex]] with frontier models, and finds that even the strongest
configurations resolve only a small share of the full set.

## Key Points

- On the 200-task full set, Claude Code with Claude Opus 4.5 resolves 11.0% of tasks and Codex with
  GPT-5.1-Codex (medium reasoning) resolves 12.5%.
- On a subset restricted to repositories shared with SWE-bench, Claude Opus 4.5 resolves 5.2% of
  tasks, compared with a 74.40% resolved rate the paper lists for it on SWE-bench Verified.
- Passed rates (the average fraction of fail-to-pass tests passed) are much higher than resolved
  rates, which the authors read as agents often producing seemingly plausible solutions that are
  still far from solving the problem.
- Every evaluated model consumes more than one million input tokens per task on average, which the
  authors describe as extremely low efficiency given the low resolved rates.
- Removing the interface specifications from the prompts markedly lowers success on the Lite set,
  while giving agents the ground-truth unit tests raises both resolved and passed rates sharply.
- Raising OpenHands' step limit from 50 to 100 gives notable gains for two models, with marginal
  improvement beyond that.
- In a failure analysis of Claude Opus 4.5, NameError dominates, which the authors attribute to
  difficulty re-establishing references across files, and they also report a tendency to guess or
  hallucinate interfaces defined in other files instead of reading them.
- The from-scratch Level 2 setting is harder than the incremental Level 1 setting.
- A senior engineer's manual revision of the Lite-set prompts produced performance highly consistent
  with the automatically generated originals, which the authors take as support for the pipeline's
  reliability.

## Notes

The pipeline currently targets Python repositories. The authors argue that because tasks can be
generated continually from new commits, the benchmark can be kept updated to mitigate data leakage,
and that its verifiable environments could also be useful for agent training. They observe that
task performance depends far more on the amount of code required than on the commit date of the
task, while cautioning that data leakage risk may grow as agents increasingly take part in feature
development.
