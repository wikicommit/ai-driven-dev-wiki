---
title: "The SWE-bench family of benchmarks"
lang: en
kind: comparison
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
derived_from:
  - path: .wikicommit/entity/en/Dataset/swe-bench.md
    source_commit: c30b98db983bd016bce35703f3ae928b84c5f04c
  - path: .wikicommit/entity/en/Dataset/swe-bench-verified.md
    source_commit: 1241f6026eea3b9fe7666601cd9fbf68d202989f
  - path: .wikicommit/entity/en/Dataset/swe-bench-pro.md
    source_commit: 3bb09ff875f75497dbb9ad4d6786745fc33ecce5
  - path: .wikicommit/entity/en/Dataset/swe-bench-lite-s.md
    source_commit: 3bb09ff875f75497dbb9ad4d6786745fc33ecce5
  - path: .wikicommit/entity/en/Dataset/swe-bench-plus.md
    source_commit: 90f235c19401779128f2c36166ba9e641fa1393d
  - path: .wikicommit/entity/en/Dataset/multi-swe-bench.md
    source_commit: 3bb09ff875f75497dbb9ad4d6786745fc33ecce5
  - path: .wikicommit/entity/en/Dataset/swe-bench-java-verified.md
    source_commit: 0905902793f108bf59d40f17ccaecab6d323e38b
  - path: .wikicommit/entity/en/Dataset/swe-bench-multimodal.md
    source_commit: 90f235c19401779128f2c36166ba9e641fa1393d
  - path: .wikicommit/entity/en/DefinedTerm/solution-leakage.md
    source_commit: 90f235c19401779128f2c36166ba9e641fa1393d
  - path: .wikicommit/entity/en/ScholarlyArticle/swe-bench-plus-enhanced-coding-benchmark-for-llms.md
    source_commit: 90f235c19401779128f2c36166ba9e641fa1393d
---

[[Dataset/swe-bench]] turned real GitHub issues into an evaluation for language models and coding
agents, and several later datasets reuse its format while changing something about it. This page
sets eight of them side by side — SWE-bench itself and seven variants — and draws out what each
one changes. It does not rank them.

## What they share

Every dataset here keeps the same basic task: an instance gives a codebase together with an issue
to resolve, and the system under evaluation produces a patch. For most of them, tests decide
whether the patch counts: [[Dataset/swe-bench]] checks correctness with unit tests and continuous integration,
[[Dataset/swe-bench-multimodal]] uses fail-to-pass and pass-to-pass tests from the corresponding
pull request, and [[Dataset/swe-bench-java-verified]] counts an issue as resolved only if all the
given test cases pass. [[Dataset/swe-bench-plus]] states that each of its instances follows the
SWE-bench format, and was collected with SWE-bench's own open-source scripts. The pages for
[[Dataset/swe-bench-verified]], [[Dataset/swe-bench-lite-s]], [[Dataset/swe-bench-pro]] and
[[Dataset/multi-swe-bench]] do not describe how patches are checked.

## Side by side

| Dataset | Size as its page gives it | Language | Who built it | What it changes relative to SWE-bench |
|---|---|---|---|---|
| [[Dataset/swe-bench]] | 2,294 problems from 12 Python repositories | Python | The authors of [[ScholarlyArticle/swe-bench-can-language-models-resolve-real-world-github-issues]] | — (the original) |
| [[Dataset/swe-bench-verified]] | 500 tasks | Python | OpenAI, with the SWE-bench authors | A human-validated subset, addressing tasks that were ambiguous or underspecified |
| [[Dataset/swe-bench-lite-s]] | Not stated | Not stated on its page | The authors of the [[DefinedTerm/agentless]] paper | A manually filtered version of SWE-bench Lite, for more rigorous comparison |
| [[Dataset/swe-bench-plus]] | 548 tasks | Python (the SWE-bench projects except Django) | The authors of [[ScholarlyArticle/swe-bench-plus-enhanced-coding-benchmark-for-llms]] | Issues created after the evaluated models' training cut-offs, screened for solutions in the issue text |
| [[Dataset/swe-bench-pro]] | 1,865 problems from 41 repositories | Not stated on its page | The authors of [[ScholarlyArticle/swe-bench-pro-can-ai-agents-solve-long-horizon-software-engineering-tasks]] | Long-horizon, enterprise-level tasks, with partitions that are not publicly accessible |
| [[Dataset/multi-swe-bench]] | 1,632 instances | Java, TypeScript, JavaScript, Go, Rust, C, C++ | The authors of [[ScholarlyArticle/multi-swe-bench-a-multilingual-benchmark-for-issue-resolving]] | Languages beyond Python |
| [[Dataset/swe-bench-java-verified]] | 91 issues from 6 repositories | Java | The authors of [[ScholarlyArticle/swe-bench-java-a-github-issue-resolving-benchmark-for-java]] | A Java version, screened with the SWE-bench Verified annotation guidelines |
| [[Dataset/swe-bench-multimodal]] | 619 instances from 17 repositories | JavaScript / TypeScript | The authors of [[ScholarlyArticle/swe-bench-multimodal-do-ai-systems-generalize-to-visual-software-domains]] | Every task contains visual content |

## Where they differ

The variants answer different complaints about the original, and they fall into roughly four
groups by which complaint they take up.

### Whether a task is well specified

[[Dataset/swe-bench-verified]] was released to address concerns that some SWE-bench tasks were
ambiguous or underspecified; its 500 tasks were validated by humans as well-specified and solvable.
[[Dataset/swe-bench-lite-s]] deals with the same kind of problem through its authors' own
classification of which tasks to exclude: the Agentless authors manually classified the problems in SWE-bench Lite and excluded issues whose
ground-truth patch is exact and issues whose descriptions were insufficient
or misleading. [[Dataset/swe-bench-java-verified]] carries the Verified approach into Java: ten
developers experienced in Java rated issue clarity, test coverage and major flaws following the
SWE-bench Verified guidelines, and only instances meeting all three criteria were kept, taking 137
candidates down to 91.

### Whether the answer is already available to the model

Two different leaks are at issue here. [[DefinedTerm/solution-leakage]] is the name the SWE-Bench+
authors give to an instance whose issue report or comments already spell out the fix; because
SWE-bench gives both to the model as input, a model can copy the fix rather than work it out.
The other concern is that issues predating a model's training cut-off may have been seen in
training; the SWE-Bench+ paper states that 94% of SWE-bench's issues and pull requests were created
before the cut-offs of the models it considers.

[[Dataset/swe-bench-plus]] addresses both at once: it takes issues created from 2023-11-01 to
2024-08-22, starting a month after the latest cut-off among the models its authors used, and
checks every instance by hand to remove those with clear solution details in the issue report.
[[Dataset/swe-bench-pro]] addresses exposure differently, by withholding: of its 41 repositories,
11 form a public set, 12 a held-out set and 18 a commercial set of proprietary repositories, and
problems in the held-out and commercial sets are not publicly accessible. Its authors describe it
as contamination-resistant.

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]], as cited on the SWE-bench,
Verified and Pro pages, describes a progression from SWE-Bench to SWE-Bench Verified, addressing
tasks that were ambiguous or underspecified, and then to SWE-Bench Pro, which OpenAI recommended
after warning that SWE-Bench Verified was increasingly exposed to data contamination.

### Which languages and domains are covered

The original is restricted to Python repositories. [[Dataset/multi-swe-bench]] covers seven other
languages, and its introducing paper motivates it by saying that existing benchmarks, SWE-bench
among them, focus almost exclusively on Python. [[Dataset/swe-bench-java-verified]] is presented
by its authors as a first step toward multilingual issue resolving evaluation.
[[Dataset/swe-bench-multimodal]] changes both language and domain: its tasks come from user-facing
JavaScript libraries, every task has visual content in its problem statement or tests, and it was
built to ask whether systems developed for the Python-only SWE-bench generalize to other languages
and to problems that have to be understood visually. A subset of 69 of its tasks is checked with
pixel-level visual testing that compares rendered screenshots.

### How large a task is

[[Dataset/swe-bench-pro]] is the variant that changes the size of the task: its introducing paper
describes its problems as long-horizon ones that may take a professional engineer hours to days,
often patching multiple files with substantial modifications, from repositories spanning business
applications, B2B services and developer tools. By comparison, the survey cited on the SWE-bench page characterizes
SWE-bench's own mix as 65% function-level tasks, 25% module-level and under 10% project-level.

## How the curation was done

The variants also differ in how their instances were chosen:

- **Human validation**: [[Dataset/swe-bench-verified]] (validated by humans as well-specified and
  solvable).
- **Manual verification by annotators**: [[Dataset/multi-swe-bench]] (1,632 instances annotated from 2,456 candidates by 68 expert
  annotators, offered by its authors as the reason it can provide an accurate and reliable
  evaluation), [[Dataset/swe-bench-java-verified]] (ten Java developers).
- **Manual inspection by the authors themselves**: [[Dataset/swe-bench-lite-s]],
  [[Dataset/swe-bench-plus]] (every instance, for solution details), and
  [[Dataset/swe-bench-multimodal]] (every remaining instance, removing 24 judged impossible).
- **Stated as human-verified and augmented with context**: [[Dataset/swe-bench-pro]].

[[Dataset/multi-swe-bench]]'s authors additionally open-source their whole data production
pipeline, with the stated aim that the community keep extending the dataset.

## What the variants report about the original

Several of these pages record findings about SWE-bench that go beyond the complaint each variant
was built around. The SWE-Bench+ paper reports that, of 251 SWE-Agent+GPT-4 patches that passed
all tests on the full SWE-bench, 32.67% were solution leaks; filtering suspicious patches drops
that system's resolution rate from 12.47% to 3.97% in its abstract (its section 2.2 gives 5.49%).
It also identified instances with the solution in the issue in SWE-bench Lite (18) and SWE-bench
Verified (37) — so human validation for specification quality, as the Verified page describes it,
did not on its own remove solution leakage.

Filtering for one defect did not remove the other, either. On SWE-Bench+, solution leakage no
longer appears but weak tests persist: about 67.72% of instances marked resolved did not truly
resolve the issue, and the systems' validated resolution rates are far below their reported
SWE-bench figures. The SWE-bench page cites the same line of findings through
[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]]: passing tests alone does
not establish that a patch is merge-ready.

