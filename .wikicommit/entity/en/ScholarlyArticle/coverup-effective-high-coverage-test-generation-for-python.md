---
title: "CoverUp: Effective High Coverage Test Generation for Python"
type: "schema:ScholarlyArticle"
lang: en
tags: [test-generation, code-coverage, execution-feedback, tool-calling]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2403.16218'
    hash: sha256:7560162f33f5e1719147eb43eadda90851e6b2c5087573dd9a5c6f5de4623b1e
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paper from the University of Massachusetts Amherst, published in Proc. ACM Softw. Eng. (FSE 2025), proposing CoverUp, which drives LLM generation of high-coverage Python regression tests by combining coverage analysis, code context and feedback in prompts. It reports per-module median line+branch coverage of 80% against CodaMosa's 47%, and overall line+branch coverage of 89% against MuTAP's 77%."
  author: ["Juan Altmayer Pizzorno", "Emery D. Berger"]
  datePublished: "2025-07"
  keywords: ["test generation", "regression testing", "large language models", "code coverage"]
---

The paper starts from the observation that manually writing tests is labor-intensive enough that developers often skip it, and that test generation tools — which generally assume the code under test is correct and generate regression tests from it — still struggle to reach high coverage. Its key insight is that LLMs can reason about code and coverage information at the same time. [[SoftwareApplication/coverup]] measures the coverage of the existing test suite, splits the code lacking coverage into segments, and prompts the LLM with each segment, the lines and branches that do not execute, and generated import statements. It offers the LLM a `get_info` tool function to request definitions of names in the excerpt, executes the returned tests, and continues the chat — reporting errors or the coverage still missing — when the tests fail or do not raise coverage.

The evaluation uses OpenAI's GPT-4o on three benchmark suites: CM, about 100,000 lines across 425 modules from CodaMosa's evaluation, on which the search-based generator Pynguin struggles; PY, modules on which Pynguin already performs well; and MT, HumanEval-derived functions used by MuTAP. Baselines are CodaMosa, a hybrid search/LLM test generator that re-seeds Pynguin's search with LLM-generated tests when it stalls, and MuTAP, a mutation-testing and LLM-based generator, each in its original Codex version and an adapted GPT-4o version.

## Key Points

- On the CM suite CoverUp achieves 64% line, 49% branch and 60% line+branch coverage overall, against 54%/34%/49% for CodaMosa (Codex) and 51%/29%/45% for CodaMosa (GPT-4o); per module its median line+branch coverage is 80% against 55% and 47%, a difference the authors report as statistically significant.
- On the MT suite CoverUp reaches 89% overall line+branch coverage against at most 78% for the MuTAP variants; per-module medians are 100% for most tools, which the authors attribute to MT's self-contained, typically type-annotated functions being much easier than CM's.
- On the PY suite, where Pynguin already does well, CoverUp reaches 100% median per-module coverage and near-100% overall coverage.
- An ablated, LLM-only version with nearly the same prompt but no coverage information, computed imports, tool function or continued chat reaches only 34% overall and 39% median per-module line+branch coverage on CM, which the authors take as showing that CoverUp's performance is not just due to the LLM.
- About 40% of successful tests came from continuing the chat: 60.3% of successes followed the first prompt, 27.2% the second and 12.5% the third.
- Removing error fixing cost 14–37% on the various coverage metrics, removing code context 7–16%, and removing coverage information up to 2%; without coverage information the prompt produced over 50% more test functions (11,222 vs. 7,366), and fewer and fewer of them improved coverage in successive runs.
- On CM, CoverUp ran about 18 times faster than CodaMosa (GPT-4o) — 4 versus 71 hours — while using about 48% more tokens; the authors caution that CoverUp is parallel and asynchronous while CodaMosa is sequential and runs for a configurable 10 minutes per module.

## Notes

The authors describe CoverUp as developed concurrently with several other LLM-based test generators, first posted on GitHub in August 2023, and distinguish it from prior LLM approaches by prompting on segments lacking coverage and by continuing the dialogue when tests fail or do not improve coverage. They could compare with SymPrompt only coarsely, since its implementation and exact benchmark subset are not publicly available. Threats they list include benchmark selection, missing prerequisite modules in CodaMosa's original environment that they deliberately left uninstalled to replicate its conditions, and dependence on the LLM's ability to follow prompts. They also observe that CodaMosa's GPT-4o variant slightly trailed its Codex original, taking this as evidence that a newer model does not necessarily perform better. A replication package and the tool itself are publicly released.
