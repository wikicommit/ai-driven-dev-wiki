---
title: "SpecRover: Code Intent Extraction via LLMs"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, code-review, verification, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2408.02232'
    hash: sha256:11a685d857df7202abc79fb94c2c9f7d605a6905b47206c856a11b12b3234adb
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A National University of Singapore paper presenting SpecRover, an LLM agent built on AutoCodeRover that infers specifications of intended behavior while resolving GitHub issues and uses a reviewer agent to vet patches and explain them, reported as resolving 31% of SWE-bench Lite."
  author: ["Haifeng Ruan", "Yuntong Zhang", "Abhik Roychoudhury"]
  abstract: "Autonomous program improvement, typically producing bug fixes and feature additions, can be accomplished by combining LLM and program analysis capabilities in an LLM agent, and since it requires a specification of intended behavior, specification inference can help produce high quality patches. The authors examine efficient, low-cost workflows for iterative specification inference within an LLM agent: given a GitHub issue, SpecRover conducts iterative code search accompanied by specification inference, inferring intent from project structure and behavior, and a reviewer agent vets the patches and provides a measure of confidence in them. Built on the open-source agent AutoCodeRover, it shows more than 50% improvement in efficacy over AutoCodeRover on the full SWE-bench of 2294 issues, at a modest cost of $0.65 per issue on SWE-bench Lite, and its explanations give the developer a better signal of when a patch can be accepted with confidence."
---

This paper starts from the problem that program repair and program improvement need some statement
of the developer's intent, but that intent is usually only available at the level of the whole
system — an issue description says how the program should behave, not how the unit function to be
changed should behave. Earlier semantic repair work extracted specifications symbolically from tests,
but the authors note that a buggy program may come without tests and that symbolic analysis has a
high entry barrier. They therefore explore the role of specifications in LLM-guided autonomous
software engineering, building on [[SoftwareApplication/autocoderover]], whose code search over
program structure they read as already capturing a coarse encoding of intent.

The result, [[SoftwareApplication/specrover]], infers several kinds of specification in sequence. A
reproducer agent writes a test reproducing the issue; a context retrieval agent explores the
codebase and, for each function it encounters, writes a natural-language summary of that function's
intended behavior in the context of the issue; a patching agent receives the buggy locations paired
with these function summaries; and a reviewer agent runs the reproducer test on the original and
patched program and judges whether the test and the patch are each correct, explaining its
decision. Patches the reviewer accepts go through the regression test suite, and when regression
tests reject every candidate, a selection agent picks the patch that best addresses the natural-
language issue and states why. The paper describes the reviewer feedback as a meta-specification that
reconciles the precise but incomplete test with the ambiguous but richer issue statement.

Evaluated on SWE-bench and its 300-issue Lite subset with Claude 3.5 Sonnet as the main model,
SpecRover reports the highest efficacy among the open-source tools it compares on both. Beyond
efficacy, the authors emphasize the precision of the patches an agent presents to a user, and the
specifications and reviewer feedback as evidence that helps a developer understand and accept a patch.

## Key Points

- SpecRover extends AutoCodeRover with two kinds of inferred specification the authors describe as unexplored by other LLM agents: function summaries of intended behavior gathered during code search, and reviewer feedback on the patch and reproducer test.
- Pairing each buggy location with a function-level specification decomposes repository-level issue solving into function-level modification tasks, the kind on which LLMs have been studied extensively.
- The reviewer agent assumes neither the generated test nor the patch is correct, so it can reject a wrong reproducer test while approving a correct patch.
- SpecRover reports resolving 19.31% (443) of the 2,294 issues in SWE-bench and 31.00% (93) of the 300 in SWE-bench Lite, at an average of $0.65 and 309 seconds per Lite issue, and 12 Lite issues that no other top-five tool resolved.
- On manual inspection, 56 of the 93 Lite patches that pass the tests (60.2%) are semantically equivalent to the developers' patches, and 29 of the remaining 37 modify the same methods as the ground truth.
- Across 119 Lite tasks with a generated reproducer test, the reviewer's accept decisions reach 64.7% accuracy, 50.0% precision and 61.9% recall; the authors state the precision is more than 1.8 times that of Agentless, the next highest.
- For 72 of 101 inspected issues (71%), the generated function specification covers intent similar to the title of the developer's pull request.
- Of the 207 unresolved Lite issues, 107 have ambiguous issue descriptions, 61 have an incorrect fix location and 39 an incorrect code modification.

## Notes

The baselines' figures are those the other tools reported, not reruns by the authors, and the
comparison is limited to open-source agents. The authors check for data memorization by counting
patches syntactically identical to the ground truth, finding 9 of the 93 resolved Lite issues. A case
study applies SpecRover to a Linux kernel buffer overflow from DARPA's AI Cyber Challenge (AIxCC),
working from a vulnerability report instead of an issue. The authors position the work within
[[DefinedTerm/automated-program-repair]] and closest to
[[ScholarlyArticle/autocoderover-autonomous-program-improvement]], and argue that agents should be
judged on precision and the signal-to-noise ratio of their output, not only efficacy. They also
report that the tool, which they call AutoCodeRover-v2, had reached 37.3% on SWE-bench Lite
and 46.2% on SWE-bench Verified at the time of acceptance in November 2024.
