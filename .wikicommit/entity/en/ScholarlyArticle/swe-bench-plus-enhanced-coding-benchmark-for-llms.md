---
title: "SWE-Bench+: Enhanced Coding Benchmark for LLMs"
type: "schema:ScholarlyArticle"
lang: en
tags: [benchmarks, evaluation, coding-agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2410.06992'
    hash: sha256:fe195596f421247a319f0f69aac6b6ee2f3a71dd78fb639db9df2b33dbb063e7
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An empirical study of the quality of the SWE-bench benchmark, which finds that many patches counted as successful rely on solutions given in the issue or pass only because of weak tests, and which introduces SWE-Bench+, a refined dataset built to avoid these problems."
  author: ["Reem Aleithan", "Haoran Xue", "Mohammad Mahdi Mohajer", "Elijah Nnorom", "Gias Uddin", "Song Wang"]
  abstract: "The authors present an empirical analysis of the SWE-bench dataset, manually screening instances that SWE-Agent+GPT-4 resolved by comparing the model-generated patches with the actual pull requests. They find that 32.67% of the successful patches involve cheating because the solutions were directly provided in the issue report or its comments, which they call solution leakage, and that 31.08% are suspicious patches due to weak test cases; filtering these out drops the resolution rate of SWE-Agent+GPT-4 from 12.47% to 3.97%. The same issues exist in SWE-bench Lite and SWE-bench Verified, and over 94% of issues were created before the LLMs' knowledge cutoff dates. They build SWE-Bench+ from GitHub issues created after the training cutoff dates and without solutions in their reports or comments, on which the evaluated models' resolution rates drop significantly."
---

This preprint from York University asks whether LLM-based systems are actually resolving the issues
in [[Dataset/swe-bench]]. During the study SWE-Agent with GPT-4 was at the top of the
SWE-bench online leaderboard, the other top approaches being either closed-source commercial tools
or not verified by the SWE-bench team for reproducibility. The authors took the instances it was
reported to have resolved, kept the 251 whose evaluation logs confirmed that all tests passed, and
had three authors independently compare each generated patch with the developers' gold patch,
reviewing the issue reports, tests and discussions.

They sort the patches into six patterns. Four make a fix suspicious: solution leak, where the fix is
spelled out in the issue description or its comments, both of which are given to the model as input;
incorrect fixes that still pass the tests; fixes that change different files or functions from the
gold patch; and incomplete fixes. Two count as correct: fixes that differ from the gold patch but
resolve the issue, and fixes more comprehensive than it. The paper traces the suspicious patterns to
two root causes in the benchmark, [[DefinedTerm/solution-leakage]] and weak test cases, and raises a
third concern that most issues predate the models' training cut-off dates.

In response the authors build [[Dataset/swe-bench-plus]], collected with SWE-bench's own methodology
from issues created after the models' cut-off dates and manually screened for solutions in the issue
report, and re-evaluate four systems on it. They also argue that benchmarks should be read alongside
cost, proposing an effectiveness-aware cost per resolved issue.

## Key Points

- Of the 251 SWE-Agent+GPT-4 patches that passed all tests on the full SWE-bench, 32.67% were solution leaks, 12.75% incorrect fixes, 3.59% changed different files or functions, and 14.74% were incomplete; 30.27% were correct but different from the gold patch and 5.98% more comprehensive than it.
- The authors attribute incorrect, incomplete and wrong-location fixes that still pass to weak tests that cannot verify a patch's correctness.
- Counting only correct fixes, the paper reports SWE-Agent+GPT-4's resolution rate on the full SWE-bench falling from 12.47% to 3.97% in its abstract and overview, while its section 2.2 gives 5.49%.
- In SWE-bench Lite and SWE-bench Verified the authors identified 18 and 37 instances with the solution in the issue or its discussion, and report that suspicious fixes reduce SWE-Agent+GPT-4's resolution rates from 18% to 9.33% on Lite and from 22.4% to 10.0% on Verified.
- The paper states that 94% of SWE-bench's issues and pull requests were created before the training cut-off dates of the LLMs it considers, raising a potential data leakage concern.
- On SWE-Bench+, solution leakage no longer appears, but weak tests persist: on average about 67.72% of the instances marked resolved did not truly resolve the issue, most often because the model failed to locate the buggy file or lines.
- After validating patches on SWE-Bench+, the reported resolution rates are 0.73% for SWE-RAG+GPT-4, 0.55% for SWE-RAG+GPT-3.5, 0.55% for SWE-Agent+GPT-4 and 3.83% for AutoCodeRover+GPT-4o.
- The authors recommend that future work report the financial cost of approaches alongside their accuracy.

## Notes

The study is limited to patches from specific systems — mainly SWE-Agent with GPT-4 — and relies
on manual comparison with gold patches, with disagreements resolved by discussion among the
authors. The paper is a preprint under review, and some of its figures are stated inconsistently
between sections, as noted above for the full-SWE-bench resolution rate. The authors call for
further work on test-case robustness in SWE-Bench+ and suggest similar studies of other benchmarks
such as HumanEval. The concern about issues predating training cut-offs relates to
[[DefinedTerm/data-contamination]], and the study examines patches produced by
[[SoftwareApplication/swe-agent]] and [[SoftwareApplication/autocoderover]].
