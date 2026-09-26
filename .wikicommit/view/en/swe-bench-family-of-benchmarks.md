---
title: "The SWE-bench family of benchmarks"
lang: en
kind: comparison
review_status: pending
generated_at: "2026-09-26"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"
derived_from:
  - path: .wikicommit/entity/en/Dataset/swe-bench-verified.md
    source_commit: 1241f6026eea3b9fe7666601cd9fbf68d202989f
  - path: .wikicommit/entity/en/Dataset/swe-bench-lite-s.md
    source_commit: 3bb09ff875f75497dbb9ad4d6786745fc33ecce5
  - path: .wikicommit/entity/en/Dataset/swe-bench-plus.md
    source_commit: 90f235c19401779128f2c36166ba9e641fa1393d
  - path: .wikicommit/entity/en/Dataset/swe-bench.md
    source_commit: 5f7f82373c0c701c9f1496f49d73d49ed72e6dfe
  - path: .wikicommit/entity/en/Dataset/multi-swe-bench.md
    source_commit: 3bb09ff875f75497dbb9ad4d6786745fc33ecce5
  - path: .wikicommit/entity/en/Dataset/swe-bench-pro.md
    source_commit: 3bb09ff875f75497dbb9ad4d6786745fc33ecce5
  - path: .wikicommit/entity/en/ScholarlyArticle/swe-bench-plus-enhanced-coding-benchmark-for-llms.md
    source_commit: 90f235c19401779128f2c36166ba9e641fa1393d
  - path: .wikicommit/entity/en/Dataset/swe-bench-java-verified.md
    source_commit: 0905902793f108bf59d40f17ccaecab6d323e38b
  - path: .wikicommit/entity/en/ScholarlyArticle/swe-bench-java-a-github-issue-resolving-benchmark-for-java.md
    source_commit: 0905902793f108bf59d40f17ccaecab6d323e38b
  - path: .wikicommit/entity/en/ScholarlyArticle/swe-bench-multimodal-do-ai-systems-generalize-to-visual-software-domains.md
    source_commit: 90f235c19401779128f2c36166ba9e641fa1393d
  - path: .wikicommit/entity/en/Dataset/swe-bench-multimodal.md
    source_commit: 90f235c19401779128f2c36166ba9e641fa1393d
  - path: .wikicommit/entity/en/ScholarlyArticle/swe-bench-can-language-models-resolve-real-world-github-issues.md
    source_commit: c30b98db983bd016bce35703f3ae928b84c5f04c
  - path: .wikicommit/entity/en/ScholarlyArticle/multi-swe-bench-a-multilingual-benchmark-for-issue-resolving.md
    source_commit: 3bb09ff875f75497dbb9ad4d6786745fc33ecce5
  - path: .wikicommit/entity/en/ScholarlyArticle/swe-bench-pro-can-ai-agents-solve-long-horizon-software-engineering-tasks.md
    source_commit: 3bb09ff875f75497dbb9ad4d6786745fc33ecce5
  - path: .wikicommit/entity/en/DefinedTerm/solution-leakage.md
    source_commit: 90f235c19401779128f2c36166ba9e641fa1393d
  - path: .wikicommit/entity/en/DefinedTerm/agentless.md
    source_commit: abe7dbaa9cb573068b927bda52cc565d6ba058e6
  - path: .wikicommit/entity/en/ScholarlyArticle/agentless-demystifying-llm-based-software-engineering-agents.md
    source_commit: 3bb09ff875f75497dbb9ad4d6786745fc33ecce5
  - path: .wikicommit/entity/en/Dataset/multi-swe-rl.md
    source_commit: 3bb09ff875f75497dbb9ad4d6786745fc33ecce5
  - path: .wikicommit/entity/en/ScholarlyArticle/masai-modular-architecture-for-software-engineering-ai-agents.md
    source_commit: 0905902793f108bf59d40f17ccaecab6d323e38b
  - path: .wikicommit/entity/en/ScholarlyArticle/specrover-code-intent-extraction-via-llms.md
    source_commit: 0905902793f108bf59d40f17ccaecab6d323e38b
  - path: .wikicommit/entity/en/ScholarlyArticle/agentic-software-engineering-foundational-pillars.md
    source_commit: 1241f6026eea3b9fe7666601cd9fbf68d202989f
  - path: .wikicommit/entity/en/ScholarlyArticle/marscode-agent-ai-native-automated-bug-fixing.md
    source_commit: 90f235c19401779128f2c36166ba9e641fa1393d
  - path: .wikicommit/entity/en/ScholarlyArticle/featurebench-benchmarking-agentic-coding-for-complex-feature-development.md
    source_commit: afa0bb4898215e961bafe4ec6d65cb547006eeb2
  - path: .wikicommit/entity/en/ScholarlyArticle/lingmaagent-improving-automated-issue-resolution.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/ScholarlyArticle/human-in-the-loop-software-development-agents.md
    source_commit: 90f235c19401779128f2c36166ba9e641fa1393d
  - path: .wikicommit/entity/en/ScholarlyArticle/context-as-a-tool-context-management-for-long-horizon-swe-agents.md
    source_commit: 48d80cbbb1b1176580f1d3e42bed65bbe89633ce
  - path: .wikicommit/entity/en/DefinedTerm/observation-masking.md
    source_commit: 48d80cbbb1b1176580f1d3e42bed65bbe89633ce
  - path: .wikicommit/entity/en/ScholarlyArticle/swe-agent-agent-computer-interfaces-enable-automated-software-engineering.md
    source_commit: 3bb09ff875f75497dbb9ad4d6786745fc33ecce5
  - path: .wikicommit/entity/en/SoftwareApplication/swe-agent.md
    source_commit: abe7dbaa9cb573068b927bda52cc565d6ba058e6
  - path: .wikicommit/entity/en/ScholarlyArticle/the-complexity-trap.md
    source_commit: 48d80cbbb1b1176580f1d3e42bed65bbe89633ce
  - path: .wikicommit/entity/en/BlogPosting/deepswe-training-a-fully-open-sourced-state-of-the-art-coding-agent-by-scaling-rl.md
    source_commit: 4438c05fa3a3f4ca959d0a98e469711dd675b69b
  - path: .wikicommit/entity/en/ScholarlyArticle/agentic-ai-in-the-software-development-lifecycle.md
    source_commit: 09becb4eb728528ea1c24b3c450ca9da552891a4
  - path: .wikicommit/entity/en/SoftwareApplication/marscode-agent.md
    source_commit: 90f235c19401779128f2c36166ba9e641fa1393d
  - path: .wikicommit/entity/en/Dataset/swe-compass.md
    source_commit: 561693fc9b2da392d0f7caec54c8c1643a4c1acc
  - path: .wikicommit/entity/en/Dataset/featurebench.md
    source_commit: afa0bb4898215e961bafe4ec6d65cb547006eeb2
  - path: .wikicommit/entity/en/SoftwareApplication/openhands.md
    source_commit: 4ba44ea0f67d038b3c885e47996bbdfb6c1e55a6
  - path: .wikicommit/entity/en/Organization/cognition.md
    source_commit: 20326ae2b2d3074fa7e5e75e7d6a666eb50f9daf
  - path: .wikicommit/entity/en/ScholarlyArticle/autocoderover-autonomous-program-improvement.md
    source_commit: c30b98db983bd016bce35703f3ae928b84c5f04c
  - path: .wikicommit/entity/en/ScholarlyArticle/ai-agentic-programming-survey.md
    source_commit: 1241f6026eea3b9fe7666601cd9fbf68d202989f
  - path: .wikicommit/entity/en/SoftwareApplication/autocoderover.md
    source_commit: c30b98db983bd016bce35703f3ae928b84c5f04c
  - path: .wikicommit/entity/en/BlogPosting/quantifying-infrastructure-noise-in-agentic-coding-evals.md
    source_commit: f948f309cb907fd940528e22bdf1a82e1e673130
  - path: .wikicommit/entity/en/DefinedTerm/context-as-a-tool.md
    source_commit: 48d80cbbb1b1176580f1d3e42bed65bbe89633ce
  - path: .wikicommit/entity/en/DefinedTerm/critic-model.md
    source_commit: 066a83f8808c1d613f191302234db9602ef3885a
  - path: .wikicommit/entity/en/ScholarlyArticle/swe-pruner-self-adaptive-context-pruning-for-coding-agents.md
    source_commit: e3a247123c2e2c5a1d19244743218b709c140afd
  - path: .wikicommit/entity/en/ScholarlyArticle/spec-kit-agents-context-grounded-agentic-workflows.md
    source_commit: 092317147ed2180d6b547e3a503ffdfc626121c5
  - path: .wikicommit/entity/en/Dataset/swe-review-bench.md
    source_commit: cebf43107fcc80ba464fe278c5b12e158d6d81f2
  - path: .wikicommit/entity/en/BlogPosting/one-year-of-openhands-a-journey-of-open-source-ai-development.md
    source_commit: 4ba44ea0f67d038b3c885e47996bbdfb6c1e55a6
  - path: .wikicommit/entity/en/ScholarlyArticle/agent-skills-for-large-language-models.md
    source_commit: e3a247123c2e2c5a1d19244743218b709c140afd
  - path: .wikicommit/entity/en/BlogPosting/introducing-devin.md
    source_commit: 20326ae2b2d3074fa7e5e75e7d6a666eb50f9daf
  - path: .wikicommit/entity/en/BlogPosting/openhands-context-condensation-for-more-efficient-ai-agents.md
    source_commit: 8d00ef0c934fe43a35ec4b3f4c9b5e7be0396fb1
  - path: .wikicommit/entity/en/ScholarlyArticle/survey-on-agent-system-and-harness-design.md
    source_commit: 23acf239019dbf782b4365d4b7b30b659e3d60c1
  - path: .wikicommit/entity/en/SoftwareApplication/mini-swe-agent.md
    source_commit: 2dde03e70d40180419b38bfd339ee1be7c0efcfa
  - path: .wikicommit/entity/en/DefinedTerm/infrastructure-noise.md
    source_commit: f948f309cb907fd940528e22bdf1a82e1e673130
  - path: .wikicommit/entity/en/Dataset/repocompliancebench.md
    source_commit: 2beeb6175d891dfb85ba85571ebde76abc6677c2
  - path: .wikicommit/entity/en/ScholarlyArticle/openhands-an-open-platform-for-ai-software-developers-as-generalist-agents.md
    source_commit: 3bb09ff875f75497dbb9ad4d6786745fc33ecce5
  - path: .wikicommit/entity/en/ScholarlyArticle/magentic-ui.md
    source_commit: fed0100a95b9cbca3a6a11c43d68e28bc873bdea
  - path: .wikicommit/entity/en/BlogPosting/writing-effective-tools-for-agents.md
    source_commit: 3e04896e3fde39929a8aec85eca2e5b6eed44b4e
  - path: .wikicommit/entity/en/BlogPosting/agent-driven-development-in-copilot-applied-science.md
    source_commit: ec1aed6cc815a0de19917c1c3fa9646b24090b11
  - path: .wikicommit/entity/en/BlogPosting/stop-using-init-for-agents-md.md
    source_commit: 908ab492691e9fcd622bfa73c6c2fd839716bea1
  - path: .wikicommit/entity/en/BlogPosting/learning-to-verify-ai-generated-code.md
    source_commit: 066a83f8808c1d613f191302234db9602ef3885a
  - path: .wikicommit/entity/en/BlogPosting/how-were-making-github-copilot-smarter-with-fewer-tools.md
    source_commit: fc6f8839ef49b4ad99a056d9f2d3011a9e22d960
  - path: .wikicommit/entity/en/DefinedTerm/generate-review-revise-loop.md
    source_commit: cebf43107fcc80ba464fe278c5b12e158d6d81f2
  - path: .wikicommit/entity/en/BlogPosting/devstral.md
    source_commit: 0787ce032ea72845b53b3574598bea1bcb64f761
  - path: .wikicommit/entity/en/ScholarlyArticle/loopsbench-from-harness-engineering-to-loop-engineering-in-coding-agent-evaluation.md
    source_commit: afa0bb4898215e961bafe4ec6d65cb547006eeb2
  - path: .wikicommit/entity/en/ScholarlyArticle/tracelab.md
    source_commit: 4f24561db04e0d1d4e76ad45ceeafcc734f1123b
  - path: .wikicommit/entity/en/ScholarlyArticle/swe-review.md
    source_commit: cebf43107fcc80ba464fe278c5b12e158d6d81f2
  - path: .wikicommit/entity/en/ScholarlyArticle/vibe-coding-practice-performance-productivity-and-risk-a-state-of-the-art-review.md
    source_commit: 2beeb6175d891dfb85ba85571ebde76abc6677c2
  - path: .wikicommit/entity/en/BlogPosting/demystifying-evals-for-ai-agents.md
    source_commit: 02f7d23719e4ec300fc997d58e966c19037dfd22
  - path: .wikicommit/entity/en/BlogPosting/introducing-devstral-2-and-mistral-vibe-cli.md
    source_commit: 0787ce032ea72845b53b3574598bea1bcb64f761
  - path: .wikicommit/entity/en/ScholarlyArticle/agentic-software-restructuring-paradigm.md
    source_commit: 0ea12caf5df433486d9ab0e30d7c6a7b7cf57315
  - path: .wikicommit/entity/en/ScholarlyArticle/harness-engineering-anatomy-architecture-and-evolution-of-coding-agents.md
    source_commit: 2dde03e70d40180419b38bfd339ee1be7c0efcfa
  - path: .wikicommit/entity/en/ScholarlyArticle/coding-benchmarks-are-misaligned-with-agentic-software-engineering.md
    source_commit: 23acf239019dbf782b4365d4b7b30b659e3d60c1
  - path: .wikicommit/entity/en/DefinedTerm/software-issue-resolution.md
    source_commit: 7c488ab4f260fd3eaef2b747c30cbac61c788ca2
  - path: .wikicommit/entity/en/ScholarlyArticle/the-semi-executable-stack.md
    source_commit: 09becb4eb728528ea1c24b3c450ca9da552891a4
  - path: .wikicommit/entity/en/ScholarlyArticle/advances-and-frontiers-of-llm-based-issue-resolution.md
    source_commit: 2b5f014fc7cc03f207d83ea499c4a231c110d0fe
  - path: .wikicommit/entity/en/ScholarlyArticle/building-effective-ai-coding-agents-for-the-terminal.md
    source_commit: 3aafc96f266b62b417b9f97d5751eb5fdfe8fce0
  - path: .wikicommit/entity/en/BlogPosting/building-effective-agents.md
    source_commit: 3e04896e3fde39929a8aec85eca2e5b6eed44b4e
  - path: .wikicommit/entity/en/DefinedTerm/tool-use-design-pattern.md
    source_commit: 365b166bc72ad4ec07cef9322a261ed16ae7b35b
---

[[Dataset/swe-bench]] turned real GitHub issues into an evaluation for language models and coding
agents, and a number of later datasets reuse its format while changing something about it. This page
sets those datasets side by side, draws out what each one changes, and collects what the rest of the
wiki records about how the family is used, built on and criticised. It does not rank the benchmarks.

## What they share

Every dataset here keeps the same basic task: an instance gives a codebase together with an issue to
resolve, and the system under evaluation produces a patch. [[DefinedTerm/software-issue-resolution]]
is the name the wiki uses for that task, and
[[ScholarlyArticle/advances-and-frontiers-of-llm-based-issue-resolution]] states it formally: an
instance `I = (D, C, T)` holds an issue description, a codebase and tests, only the description and
codebase are observable while resolving, and the patch is evaluated by running the tests. Its
aggregate metric is the Resolved Rate, the mean of per-instance binary outcomes; the benchmark's own
site reports **% Resolved** for each member of the family it hosts.

For most of the datasets, tests decide whether the patch counts. [[Dataset/swe-bench]] checks
correctness with unit tests and continuous integration; [[Dataset/swe-bench-multimodal]] uses
fail-to-pass and pass-to-pass tests from the corresponding pull request; and
[[Dataset/swe-bench-java-verified]] counts an issue as resolved only if all the given test cases
pass. [[Dataset/swe-bench-plus]] states that each of its instances follows the SWE-bench format, and
was collected with SWE-bench's own open-source scripts. The pages for [[Dataset/swe-bench-verified]],
[[Dataset/swe-bench-lite-s]], [[Dataset/swe-bench-pro]] and [[Dataset/multi-swe-bench]] do not
describe how patches are checked.

## Side by side

The first eight rows are datasets with their own page in this wiki. The last three are members the
benchmark's own site lists, recorded on the [[Dataset/swe-bench]] page, without pages of their own.

| Dataset | Size as its page gives it | Language | Who built it | What it changes relative to SWE-bench |
|---|---|---|---|---|
| [[Dataset/swe-bench]] | 2,294 problems from 12 Python repositories | Python | The authors of [[ScholarlyArticle/swe-bench-can-language-models-resolve-real-world-github-issues]] | — (the original) |
| [[Dataset/swe-bench-verified]] | 500 tasks | Python | OpenAI, with the SWE-bench authors | A human-validated subset, addressing tasks that were ambiguous or underspecified |
| [[Dataset/swe-bench-lite-s]] | Not stated | Not stated on its page | The authors of the [[DefinedTerm/agentless]] paper | A manually filtered version of SWE-bench Lite, for more rigorous comparison |
| [[Dataset/swe-bench-plus]] | 548 tasks | Python (the SWE-bench projects except Django) | The authors of [[ScholarlyArticle/swe-bench-plus-enhanced-coding-benchmark-for-llms]] | Issues created after the evaluated models' training cut-offs, screened for solutions in the issue text |
| [[Dataset/swe-bench-pro]] | 1,865 problems from 41 repositories | Not stated on its page | The authors of [[ScholarlyArticle/swe-bench-pro-can-ai-agents-solve-long-horizon-software-engineering-tasks]] | Long-horizon, enterprise-level tasks, with partitions that are not publicly accessible |
| [[Dataset/multi-swe-bench]] | 1,632 instances | Java, TypeScript, JavaScript, Go, Rust, C, C++ | The authors of [[ScholarlyArticle/multi-swe-bench-a-multilingual-benchmark-for-issue-resolving]] | Languages beyond Python |
| [[Dataset/swe-bench-java-verified]] | 91 issues from 6 repositories | Java | The authors of [[ScholarlyArticle/swe-bench-java-a-github-issue-resolving-benchmark-for-java]] | A Java version, screened with the SWE-bench Verified annotation guidelines |
| [[Dataset/swe-bench-multimodal]] | 619 instances from 17 repositories (paper); 480 (benchmark site) | JavaScript / TypeScript | The authors of [[ScholarlyArticle/swe-bench-multimodal-do-ai-systems-generalize-to-visual-software-domains]] | Every task contains visual content |
| SWE-bench Lite | 300 instances | Python | Listed on the SWE-bench site | A subset curated for less costly evaluation |
| SWE-bench Multilingual | 300 instances from 42 repositories | 9 programming languages | Listed on the SWE-bench site | Tasks across several languages |
| Bash Only | The same 500 instances as Verified | Python | Listed on the SWE-bench site | The default view of the Verified leaderboard, in which every model runs in the same [[SoftwareApplication/mini-swe-agent]] environment |

One size is given differently by different sources: for [[Dataset/swe-bench-multimodal]], the
introducing paper reports 619 task instances (its abstract states 617), split into a 517-instance
test set and a 102-instance development set, while the benchmark's site lists 480 instances. For
SWE-bench Lite, [[ScholarlyArticle/masai-modular-architecture-for-software-engineering-ai-agents]]
adds that its 300 issues come from 11 Python repositories.

## Order of appearance

The pages give dates for several members, which puts them in this order:

- **October 2023** — the SWE-bench paper is first submitted, on 10 October 2023.
- **March 2024** — SWE-bench Lite is released, according to the benchmark's site.
- **June 2024** — the site records SWE-bench being Docker-ized for easier evaluation.
- **July 2024** — the Agentless paper, which constructs [[Dataset/swe-bench-lite-s]], is first
  submitted on 1 July 2024.
- **August 2024** — [[Dataset/swe-bench-verified]] is announced as a collaboration with
  [[Organization/openai]].
- **October 2024** — [[Dataset/swe-bench-multimodal]] is introduced, according to the site.
- **April 2025** — the Multi-SWE-bench paper is submitted on 3 April 2025.
- **September 2025** — the SWE-Bench Pro paper is first submitted on 21 September 2025.

[[Dataset/swe-bench-plus]] collects issues created from 2023-11-01 to 2024-08-22; its page gives no
release date. [[Dataset/swe-bench-java-verified]]'s page gives none either.

## Where they differ

The variants answer different complaints about the original, and they fall into roughly four groups
by which complaint they take up.

### Whether a task is well specified

[[Dataset/swe-bench-verified]] was released to address concerns that some SWE-bench tasks were
ambiguous or underspecified; its 500 tasks were validated by humans as well-specified and solvable.
[[Dataset/swe-bench-lite-s]] deals with the same kind of problem through its authors' own
classification: the Agentless authors manually classified the problems in SWE-bench Lite and
excluded issues whose ground-truth patch is exact and issues whose descriptions were insufficient or
misleading. [[Dataset/swe-bench-java-verified]] carries the Verified approach into Java: ten
developers experienced in Java rated issue clarity, test coverage and major flaws following the
SWE-bench Verified guidelines, and only instances meeting all three criteria were kept, taking 137
candidates down to 91. [[Dataset/swe-bench-pro]] states that all of its tasks are human-verified and
augmented with sufficient context to ensure resolvability.

Other pages record how much underspecification remains a factor on the older sets. Of the 207
SWE-bench Lite issues [[ScholarlyArticle/specrover-code-intent-extraction-via-llms]] left unresolved,
it counts 107 with ambiguous issue descriptions.

### Whether the answer is already available to the model

Two different leaks are at issue here. [[DefinedTerm/solution-leakage]] is the name the SWE-Bench+
authors give to an instance whose issue report or comments already spell out the fix; because
SWE-bench gives both to the model as input (the comments as `hints_text`), a model can copy the fix
rather than work it out. The other concern is that issues predating a model's training cut-off may
have been seen in training; the SWE-Bench+ paper states that 94% of SWE-bench's issues and pull
requests were created before the cut-offs of the models it considers.

[[Dataset/swe-bench-plus]] addresses both at once: it takes issues created from 2023-11-01 to
2024-08-22, starting a month after the latest cut-off among the models its authors used, and checks
every instance by hand to remove those with clear solution details in the issue report.
[[Dataset/swe-bench-pro]] addresses exposure differently, by withholding: of its 41 repositories, 11
form a public set, 12 a held-out set and 18 a commercial set of proprietary repositories, and
problems in the held-out and commercial sets are not publicly accessible. Its authors describe it as
contamination-resistant.

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] describes a progression from
SWE-Bench to SWE-Bench Verified, addressing tasks that were ambiguous or underspecified, and then to
SWE-Bench Pro, which OpenAI recommended after warning that SWE-Bench Verified was increasingly exposed
to data contamination.

The variants do not all find contamination to matter in the same way. The SWE-bench Multimodal
paper reports a temporal analysis that found no evidence that solutions leaked into the models'
training data gave an advantage on its test set. [[Dataset/featurebench]]'s paper observes that task
performance depends far more on the amount of code required than on a task's commit date. Several
system papers raise the concern about their own results:
[[ScholarlyArticle/lingmaagent-improving-automated-issue-resolution]] names the possibility that the
models it used saw parts of the test repositories in training, and SpecRover checks for memorization
by counting patches syntactically identical to the ground truth, finding 9 of its 93 resolved Lite
issues. The DeepSWE post, [[BlogPosting/deepswe-training-a-fully-open-sourced-state-of-the-art-coding-agent-by-scaling-rl]],
filtered its training tasks to exclude repositories that also appear in SWE-Bench-Verified to avoid
contamination.

### Which languages and domains are covered

The original is restricted to Python repositories. [[Dataset/multi-swe-bench]] covers seven other
languages, and its introducing paper motivates it by saying that existing benchmarks, SWE-bench among
them, focus almost exclusively on Python. [[Dataset/swe-bench-java-verified]] is presented by its
authors as a first step toward multilingual issue-resolving evaluation; its paper argues that
SWE-bench's Python focus confines it to fields such as data processing and artificial intelligence,
leaving out web, mobile and system programming, and says the authors plan to add Go, Rust, C and C++.
That paper's project links point to multi-swe-bench.github.io and a Hugging Face dataset named
Daoguang/Multi-SWE-bench. The benchmark's site also lists a SWE-bench Multilingual set covering 9
languages.

[[Dataset/swe-bench-multimodal]] changes both language and domain: its tasks come from user-facing
JavaScript libraries, every task has visual content in its problem statement or tests, and it was
built to ask whether systems developed for the Python-only SWE-bench generalize to other languages
and to problems that have to be understood visually. Its paper notes that only 5.6% of SWE-bench's
tasks contain an image. A subset of 69 of its tasks is checked with pixel-level visual testing that
compares rendered screenshots.

Moving off Python exposed how tightly some systems had been fitted to the original. The Multimodal
paper reports that AutoCodeRover and Moatless rely on Python-specific program analysis and were not
benchmarked, and that Agentless needed a JavaScript parser written from scratch; it attributes
Agentless's weak results there to a localization module designed around Python.

### What kind and size of task

[[Dataset/swe-bench-pro]] is the variant built around the size of the task: its introducing paper
describes its problems as long-horizon ones that may take a professional engineer hours to days,
often patching multiple files with substantial modifications, from repositories spanning business
applications, B2B services and developer tools. By comparison, the survey cited on the SWE-bench page
characterizes SWE-bench's own mix as 65% function-level tasks, 25% module-level and under 10%
project-level. [[ScholarlyArticle/ai-agentic-programming-survey]], using SWE-Bench as a case study,
reports that commonly used coding benchmarks are heavily biased toward Python and typically evaluate
small, self-contained, or function- and module-level problems. The Multimodal paper's annotators
estimated its tasks take longer to solve than SWE-bench tasks, with reference solutions editing more
files, functions and lines.

Task kind is a separate axis from size. The FeatureBench paper,
[[ScholarlyArticle/featurebench-benchmarking-agentic-coding-for-complex-feature-development]], puts
feature requests at only about 18–22% of SWE-bench instances and argues that pull-request-based
collection cannot capture features that span several pull requests.

## How the curation was done

The variants also differ in how their instances were chosen:

- **Human validation**: [[Dataset/swe-bench-verified]] (validated by humans as well-specified and
  solvable).
- **Manual verification by annotators**: [[Dataset/multi-swe-bench]] (1,632 instances annotated from
  2,456 candidates by 68 expert annotators, offered by its authors as the reason it can provide an
  accurate and reliable evaluation), [[Dataset/swe-bench-java-verified]] (ten Java developers).
- **Manual inspection by the authors themselves**: [[Dataset/swe-bench-lite-s]],
  [[Dataset/swe-bench-plus]] (every instance, for solution details), and
  [[Dataset/swe-bench-multimodal]] (every remaining instance, removing 24 judged impossible).
- **Stated as human-verified and augmented with context**: [[Dataset/swe-bench-pro]].

Several variants also changed the collection pipeline itself. [[Dataset/swe-bench-plus]] reused
SWE-bench's attribute and execution filters. The SWE-bench-java paper reports fixing a bug in the
original SWE-bench collection script, which sometimes took the wrong base commit by ignoring branch
differences. [[Dataset/swe-bench-multimodal]] added Node.js and Chrome support to SWE-bench's Docker
setup and removed tests whose results were inconsistent across repeated runs.
[[Dataset/multi-swe-bench]]'s authors open-source their whole data production pipeline, with the
stated aim that the community keep extending the dataset, and pair the benchmark with
[[Dataset/multi-swe-rl]], a community effort releasing 4,723 instances across seven languages as
reinforcement-learning training data.

## What the variants report about the original

Several of these pages record findings about SWE-bench that go beyond the complaint each variant was
built around. The SWE-Bench+ paper reports that, of 251 SWE-Agent+GPT-4 patches that passed all tests
on the full SWE-bench, 32.67% were solution leaks; filtering suspicious patches drops that system's
resolution rate from 12.47% to 3.97% in its abstract (its section 2.2 gives 5.49%). It also
identified instances with the solution in the issue in SWE-bench Lite (18) and SWE-bench Verified
(37), and reports suspicious fixes reducing SWE-Agent+GPT-4's rates from 18% to 9.33% on Lite and
from 22.4% to 10.0% on Verified — so human validation for specification quality, as the Verified page
describes it, did not on its own remove solution leakage.

Filtering for one defect did not remove the other, either. On SWE-Bench+, solution leakage no longer
appears but weak tests persist: about 67.72% of instances marked resolved did not truly resolve the
issue, and the systems' validated resolution rates are far below their reported SWE-bench figures.
The SWE-bench page cites the same line of findings through
[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]]: 29.6% of "plausible" fixes
introduced regressions or were incorrect on retesting, and passing tests alone does not establish
that a patch is merge-ready.

A system paper reached a related measurement from the other side. SpecRover's authors inspected the
93 SWE-bench Lite patches it resolved and found 56 (60.2%) semantically equivalent to the developers'
patches, with 29 of the remaining 37 modifying the same methods as the ground truth.

## How the rest of the wiki reads the family

Pages beyond the variants themselves take up the family in five ways.

### As a measurement whose score depends on more than the model

- [[BlogPosting/quantifying-infrastructure-noise-in-agentic-coding-evals]] and
  [[DefinedTerm/infrastructure-noise]] report a crossover experiment on SWE-bench, varying available
  RAM up to 5x across 227 problems, that moved the score by 1.54 percentage points — the same
  monotonic effect as on Terminal-Bench 2.0 at a smaller magnitude, which the term's page attributes
  to SWE-bench's tasks being less resource-intensive.
- [[ScholarlyArticle/survey-on-agent-system-and-harness-design]] compiles SWE-bench Verified
  leaderboard data showing that, within one model, harness choice moves Claude 3.5 Sonnet from 33.6%
  with SWE-agent to 53.6% with PatchPilot, and cautions that the table is observational rather than a
  controlled experiment.
- [[ScholarlyArticle/coding-benchmarks-are-misaligned-with-agentic-software-engineering]] describes
  SWE-bench, among others, as producing a single number from a single model, harness and environment,
  with no signal at the level of individual components.
- [[ScholarlyArticle/agentic-ai-in-the-software-development-lifecycle]] compiles a SWE-bench Verified
  timeline from vendor reports and papers, rising from 1.96% in October 2023 to 78.4% in April 2026,
  and reads the gain as dominated by scaffolding rather than raw model capability; it marks its
  figures as approximate.
- [[ScholarlyArticle/harness-engineering-anatomy-architecture-and-evolution-of-coding-agents]]
  distinguishes an evaluation harness such as SWE-bench's, which wraps an agent rather than a model,
  from an agent harness.
- [[BlogPosting/devstral]] separates comparisons made under the same scaffold from comparisons with
  models evaluated under any scaffold.

### As a benchmark whose scores need qualifying

- [[ScholarlyArticle/advances-and-frontiers-of-llm-based-issue-resolution]] reports that agent
  success rates are frequently inflated by solution leakage, ambiguous issue descriptions and weak
  test suites, that the field is shifting toward automated validation by model-based consensus
  because manual cleanup is too costly at scale, and that contamination threatens reliability as
  benchmarks approach saturation. It also frames SWE-bench as a departure from software
  *generation* toward maintenance and evolution.
- [[ScholarlyArticle/vibe-coding-practice-performance-productivity-and-risk-a-state-of-the-art-review]]
  reads the climb on SWE-Bench Verified as qualified by lower scores on contamination-resistant and
  independently run evaluations.
- [[ScholarlyArticle/human-in-the-loop-software-development-agents]] argues that evaluating
  functional correctness should go beyond passing unit tests.
- [[BlogPosting/demystifying-evals-for-ai-agents]] gives SWE-bench Verified as an example of the
  deterministic, test-based grading that is natural for coding agents.

### As the substrate for a different benchmark

- [[Dataset/swe-review-bench]] derives its instances from the 500 issues of
  [[Dataset/swe-bench-verified]], which supplies the executable tests its metrics depend on.
- [[Dataset/repocompliancebench]] reuses SWE-bench's issue-to-patch substrate and contamination
  discipline, but measures compliance with contribution rules rather than repair quality.
- [[Dataset/featurebench]] is introduced as a harder, feature-focused counterpart to SWE-bench; on a
  subset restricted to repositories shared with SWE-bench, its paper reports Claude Opus 4.5
  resolving 5.2% of tasks, against the 74.40% it lists for that model on SWE-bench Verified.
- [[Dataset/swe-compass]] positions itself against [[Dataset/swe-bench-verified]],
  [[Dataset/swe-bench-pro]] and [[Dataset/multi-swe-bench]], on the grounds that they cover fewer
  languages and, in most cases, only bug fixing.
- [[ScholarlyArticle/loopsbench-from-harness-engineering-to-loop-engineering-in-coding-agent-evaluation]]
  argues that SWE-bench and its variants remain terminal — judged by final task success — and builds
  [[Dataset/loopsbench]] around dependency structure instead.
- [[ScholarlyArticle/tracelab]] says capability benchmarks such as SWE-bench contain relatively few
  narrowly scoped tasks, and so do not capture what shapes the cost of serving coding agents.

### As a source of training signal

[[DefinedTerm/critic-model]] and [[BlogPosting/learning-to-verify-ai-generated-code]] record that
earlier critic models were trained on SWE-bench and SWE-Gym, where unit tests supply verified rewards;
OpenHands reports that a critic trained only on benchmark-style data scored an AUC of about
0.45–0.48 on production outcomes. [[Dataset/multi-swe-rl]] releases issue-resolving instances as
reinforcement-learning training data, and the DeepSWE post casts software-engineering tasks as
reinforcement-learning environments, excluding repositories that appear in SWE-Bench-Verified.

### As a name used in passing

Some pages use SWE-bench only as a reference point. The OpenHands paper,
[[ScholarlyArticle/openhands-an-open-platform-for-ai-software-developers-as-generalist-agents]],
names it as an example of the software-engineering tasks the platform incorporates;
[[SoftwareApplication/openhands]] and
[[BlogPosting/one-year-of-openhands-a-journey-of-open-source-ai-development]] list accuracy on
benchmarks such as SWE-Bench among the project's aims. [[ScholarlyArticle/the-semi-executable-stack]]
places agentic-coding benchmarks such as SWE-bench mainly in its rings 1–3.
[[BlogPosting/building-effective-agents]] names a coding agent for SWE-bench tasks as one of
Anthropic's own examples. [[ScholarlyArticle/magentic-ui]] lists SWE-Bench-style tasks among those
it struggles with. [[ScholarlyArticle/agent-skills-for-large-language-models]] covers benchmark
progress on SWE-bench in its deployment axis. [[ScholarlyArticle/building-effective-ai-coding-agents-for-the-terminal]]
names SWE-bench evaluation as future work. [[SoftwareApplication/swe-agent]]'s repository presents
SWE-bench alongside the team's related projects, and the benchmark's own site groups
[[SoftwareApplication/swe-agent]], mini-SWE-agent, SWE-smith, SWE-ReX and a SWE-bench CLI with the
benchmarks as one family.

## Which member each result is reported on

The pages report results on different members, and the member is part of what a figure means. The
table lists where each page's reported result was measured, in that page's own terms; figures from
different rows are not measured under the same conditions, and several pages say so themselves.

| Member | Pages reporting results on it |
|---|---|
| SWE-bench (full) | The introducing paper (Claude 2 at 1.96%); [[ScholarlyArticle/swe-agent-agent-computer-interfaces-enable-automated-software-engineering]] (12.5% pass@1); [[BlogPosting/introducing-devin]] and [[Organization/cognition]] (13.86%, on a random 25% subset, unassisted, against assisted baselines); SpecRover (19.31%); the SWE-Bench+ audit; an ETH Zurich study described in [[BlogPosting/stop-using-init-for-agents-md]]; the infrastructure-noise crossover experiment |
| SWE-bench Lite | [[ScholarlyArticle/autocoderover-autonomous-program-improvement]] and [[SoftwareApplication/autocoderover]] (19%); [[ScholarlyArticle/agentless-demystifying-llm-based-software-engineering-agents]] (32.00%); MASAI (28.33%); [[ScholarlyArticle/marscode-agent-ai-native-automated-bug-fixing]] and [[SoftwareApplication/marscode-agent]] (34%); LingmaAgent (21.33% with GPT-4 Turbo, 38.33% with Claude 3.5 Sonnet and execution feedback); SpecRover (31.00%); [[ScholarlyArticle/spec-kit-agents-context-grounded-agentic-workflows]] (58.2% with hooks, 56.5% without) |
| SWE-bench Verified | HULA (31% of issues passing all unit tests); [[ScholarlyArticle/context-as-a-tool-context-management-for-long-horizon-swe-agents]] and [[DefinedTerm/context-as-a-tool]] (57.6%); [[ScholarlyArticle/the-complexity-trap]] and [[DefinedTerm/observation-masking]]; DeepSWE (42.2% Pass@1); [[BlogPosting/openhands-context-condensation-for-more-efficient-ai-agents]] (a subset, 54% against 53%); [[ScholarlyArticle/swe-pruner-self-adaptive-context-pruning-for-coding-agents]]; [[BlogPosting/how-were-making-github-copilot-smarter-with-fewer-tools]]; [[BlogPosting/writing-effective-tools-for-agents]] and [[DefinedTerm/tool-use-design-pattern]]; [[BlogPosting/learning-to-verify-ai-generated-code]] (a mixed-outcome subset); [[ScholarlyArticle/swe-review]] and [[DefinedTerm/generate-review-revise-loop]]; [[BlogPosting/devstral]] (46.8%); [[BlogPosting/introducing-devstral-2-and-mistral-vibe-cli]] (72.2% and 68.0%); Agentless's v1.5 runs; AutoCodeRover-v2 (46.2%); [[SoftwareApplication/mini-swe-agent]]; [[ScholarlyArticle/agentic-software-restructuring-paradigm]]; compiled timelines and tables in the SDLC and harness surveys |
| SWE-Bench Pro | [[BlogPosting/agent-driven-development-in-copilot-applied-science]] (trajectory analysis rather than a score) |
| Multi-SWE-bench, SWE-bench-java-verified, SWE-bench Multimodal, SWE-Bench+ | Only their own introducing papers |

Several of these pages carry their own caveat about the figure. The Devstral and Devstral 2 posts'
figures are Mistral's own; [[SoftwareApplication/mini-swe-agent]]'s page notes that the figures it
cites are self-reported, on different models and dates; the AutoCodeRover paper compares against
SWE-agent's reported efficacy rather than a run of its own; SpecRover's baselines are the figures
other tools reported; and MASAI's authors note that SWE-bench Lite's issues are limited to those that
can be validated with tests and are all in English, and that some compared methods used extra inputs
such as hints text.
