---
title: "c-CRAB"
type: "schema:Dataset"
lang: en
tags: [code-review, evaluation, agents, coding-agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.23448'
    hash: sha256:6fa91d85c5a2b4ac6ba1428f5252e7998ba24ba42ec0924c63423d994264d7e8
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A benchmark for automated code review tools in which human review comments are converted into executable tests, so that a review is scored by whether it guides a coding agent to a fix that makes the test pass rather than by its textual similarity to the human comment."
  creator: ["Yuntong Zhang", "Zhiyuan Pan", "Imam Nur Bani Yusuf", "Haifeng Ruan", "Ridwan Shariffdeen", "Abhik Roychoudhury"]
  url: "https://github.com/c-CRAB-Benchmark"
  variableMeasured: ["pull request", "patch under review", "pull request description", "executable test", "execution environment"]
---

c-CRAB, pronounced "see-crab", is a benchmark for evaluating automated code review tools, introduced
in [[ScholarlyArticle/code-review-agent-benchmark]]. Each instance pairs a real pull request whose
patch is to be reviewed with a set of executable tests derived from the comments human reviewers
actually left on it. Every test is constructed to fail on the original patch and pass once the
corresponding issue has been resolved, so that it acts as an objective oracle for the issue its
reviewer raised. Its authors position it as the only code review dataset whose oracle is the
dynamic behaviour of the program as witnessed by tests rather than the wording of a human comment — a
claim they rest on their own survey of the benchmarks that preceded it.

## Contents

A record is one pull request instance: the patch under review, the pull request description, at least
one validated executable test, and an isolated Docker environment in which that test can be run. The
released benchmark holds 184 pull request instances carrying 234 validated review comments, an average
of 1.27 tests per instance, with an average of 418.1 modified lines per instance and 31.8 lines per
test.

The 234 tests are split into two kinds. Behavioral tests import and execute the code under test,
invoking functions with specific inputs and checking outputs or verifying exceptions; there are 42 of
these, 17.9% of the total. Structural tests inspect source code text, match patterns and check API
surfaces to determine whether the desired code change has been made; there are 192, 82.1% of the
total.

## Provenance

The benchmark is built on top of the SWE-CARE dataset, which already supplies pull request instances
with the commit metadata the pipeline needs; its authors note the curation pipeline is otherwise
dataset-agnostic and can be applied to any pull request carrying that metadata.

Curation runs in four stages. Review filtering keeps only comments expressing a specific, actionable
and objectively verifiable issue, discarding conversational material such as clarification requests,
acknowledgments and praise; this is done by an LLM classifier whose prompt was refined against a gold
set of 100 comments labelled independently by two authors. Execution environment construction builds
an isolated Docker image per pull request, generating installation scripts by detecting build tools
and inferring dependencies from specification files, and falling back to an automated coding agent to
pin accurate dependency versions where a historic project's own specification is too loose. Converting
natural-language comments to tests prompts a model with the comment, the relevant diff hunk and the
file contents before and after the fix, then runs the candidate test against both repository states
and keeps it only if it fails on the before version and passes on the after version, with an
execution-guided refinement loop feeding traces and error messages back on failure. Validation with
coding agents discards any instance where a coding agent, given the original human comment as
guidance, cannot produce a revision that makes the test pass — so that a later failure can be
attributed to the review rather than to the agent.

The pipeline is reported to reduce an initial 671 pull requests carrying 1,313 comments to 410 pull
requests and 595 comments after filtering, 339 and 481 after test conversion, and 184 and 234 after
validation. The authors used GPT-5.2 for review filtering and for comment-to-test conversion, allowing
up to three attempts with execution feedback, and Claude Code with a Sonnet-4.6 backend as the coding
agent in both validation and evaluation. To check test quality, two authors independently judged
whether each test faithfully captured its review comment on a random sample of 50 instances, reaching
84% agreement; the authors attribute the remaining disagreements to partial coverage of the comment
and occasional overfitting of tests to specific implementations.

The replication package, including source code, benchmark datasets and results, is published at
<https://github.com/c-CRAB-Benchmark>.

## Use

In the study that introduces it, c-CRAB is used to evaluate four automated review tools — one
open-source and three proprietary. That study reports pass rates between 20.1% and 32.1% against a
human pass rate of 100%, and that 97 of the 234 tests (41.5%) were passed by at least one of the four.
It further reports that pass rates vary by issue category, being highest on robustness and functional
correctness and lowest on documentation and design.

The authors are explicit about what the metric does and does not measure: the pass rate reflects the
extent to which a review tool identifies issues that human reviewers found, treating human reviews as
ground truth, and the benchmark does not evaluate additional valuable comments a tool may produce
that no human raised.
