---
title: "Code Review Agent Benchmark"
type: "schema:ScholarlyArticle"
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
  description: "Introduces c-CRAB, a benchmark that evaluates automated code review tools by converting human review comments into executable tests, and reports that four state-of-the-art review tools together capture only about 41% of the issues human reviewers raised."
  author: ["Yuntong Zhang", "Zhiyuan Pan", "Imam Nur Bani Yusuf", "Haifeng Ruan", "Ridwan Shariffdeen", "Abhik Roychoudhury"]
  datePublished: "2026-04-07"
  keywords: ["Automated Code Review", "Benchmark", "LLM Agent"]
---

This paper argues that as AI systems generate ever larger volumes of code, the capacity of human
reviewers has not scaled with it, making review the bottleneck in the development pipeline — and that
the automated review tools proposed in response cannot currently be evaluated well. Its authors take
issue with the prevailing evaluation methods: similarity metrics such as BLEU, ROUGE, chrF and
embedding distance measure resemblance in wording rather than whether a review identifies a real
issue, so a review may name a valid problem in entirely different words and still score low;
localization metrics assess only where an issue is flagged rather than what was said about it; and
LLM-as-a-judge approaches are sensitive to prompt design and inherent randomness, making their
judgments hard to reproduce.

The paper's response is a test-based evaluation, embodied in a benchmark called
[[Dataset/c-crab]] (pronounced "see-crab"). Human review feedback is systematically converted into
executable tests that capture the underlying issue a reviewer raised, each written to fail on the
original patch and pass once the issue is resolved. To evaluate a review tool, the tool is given a
pull request and produces review comments; a separate coding agent then revises the patch using those
comments as guidance, and the revised code is executed against the curated tests. A passing test is
taken as evidence that the review identified an actionable issue corresponding to one a human raised.

The authors motivate this design with worked examples. In one, a human reviewer and a tool-generated
review raise the same indexing concern in different words, scoring 0.00 on BLEU-4 and 7.02 on
ROUGE-L while the test-based evaluation records the concern as captured. In another, a reviewer asks
for a field's type to be changed while the tool proposes only raising a length limit — an LLM judge
treats the two as raising the same concern, whereas the executable test distinguishes them because
the suggested fix does not resolve the root issue.

## Key Points

- Proposes evaluating code review comments by whether they lead to behaviorally correct fixes, rather
  than by textual similarity to human comments or by an LLM's judgment, on the argument that human
  review comments are noisy artifacts whose wording does not reliably correspond to the issue raised.
- Reports that the four evaluated tools achieve pass rates from 20.1% to 32.1% against a human pass
  rate of 100%, and that taking the union across all four, 97 of the 234 tests (41.5%) were passed by
  at least one tool.
- Argues the gap should not be read as the generated reviews being low quality. In a manual inspection
  of 92 review comments across six randomly selected pull requests, two annotators labelled 77 (84%)
  as useful, meaning they pointed out valid issues or suggested improvements.
- Reports that the distribution of issue categories differs between tools and humans: automated tools
  raise robustness and testing concerns more often than humans, while addressing design, documentation
  and maintainability substantially less often. The authors attribute the underrepresentation to those
  categories depending on conventions specific to an individual repository.
- Reports that pass rates vary by category, being highest on robustness and functional correctness —
  which the authors suggest are more localized within the patch under review — and lowest on
  documentation and design, with maintainability ranging from 7.9% to 27.0% across tools.
- Concludes that automated review tools should be viewed as complements to human reviewers rather than
  replacements, and suggests that documenting repository-specific rules in artifacts a tool can read,
  and grounding review agents in richer project context such as architecture documents, prior review
  history and naming conventions, are routes to closing the gap.
- Suggests executable tests derived from reviews may be useful beyond evaluation, as a training signal
  that rewards issue identification leading to verifiable improvements in code.

## Notes

The authors state three threats to validity. For internal validity they note that because evaluation
relies on a coding agent to revise patches, outcomes may reflect the agent's capability as well as the
review's quality; they report mitigating this by validating each benchmark instance with the original
human comment before inclusion and by using the same coding agent in both validation and evaluation.
For external validity they note that the benchmark is built from an existing dataset and that its
curation, while improving reliability, may limit how representative it is of the broader software
ecosystem — though the pipeline can be applied to new pull requests. For construct validity they note
that the filtering stage uses an LLM-based classifier that may retain borderline comments, and that
the manual analysis of the reviews involves human judgment, mitigated by having two authors perform
the labelling independently.

The paper reports that the work was partially supported by a Singapore Ministry of Education Tier 3
grant, and carries a disclaimer stating that its views are the authors' alone, do not represent the
official policies or endorsements of SonarSource, and should not be interpreted as an evaluation of
the quality of products at SonarSource.
