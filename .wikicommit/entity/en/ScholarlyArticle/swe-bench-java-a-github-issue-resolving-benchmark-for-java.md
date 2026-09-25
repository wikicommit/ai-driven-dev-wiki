---
title: "SWE-bench-java: A GitHub Issue Resolving Benchmark for Java"
type: "schema:ScholarlyArticle"
lang: en
tags: [benchmarks, evaluation, coding-agents, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2408.14354'
    hash: sha256:35f61048ed10b99916fd70a91f8f3e3e569d8211172e3a4e66dbf2b34743c36e
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A paper introducing SWE-bench-java-verified, a Java version of the SWE-bench issue resolving benchmark with 91 manually verified issues, released with a Docker-based evaluation environment and leaderboard as a first step toward multilingual issue resolving evaluation."
  author: ["Daoguang Zan", "Zhirong Huang", "Ailun Yu", "Shaoxin Lin", "Yifan Shi", "Wei Liu", "Dong Chen", "Zongshuai Qi", "Hao Yu", "Lei Yu", "Dezhi Ran", "Muhan Zeng", "Bo Shen", "Pan Bian", "Guangtai Liang", "Bei Guan", "Pengjie Huang", "Tao Xie", "Yongji Wang", "Qianxiang Wang"]
  abstract: "GitHub issue resolving is a critical task in software engineering, and SWE-bench was released to evaluate the issue resolving capabilities of LLMs but has so far covered only Python. As a first step toward multilingual support, the authors developed a Java version of SWE-bench, SWE-bench-java-verified, and publicly released the dataset with a Docker-based evaluation environment and leaderboard, to be maintained and updated. To verify its reliability they implement SWE-agent and test several LLMs on it, and they invite contributions through pull requests or collaboration."
---

This paper extends the issue resolving benchmark [[Dataset/swe-bench]], which asks a model to
produce a patch from an issue description and the buggy repository, beyond Python. The authors
argue that SWE-bench's focus on Python limits its evaluation to fields such as data processing and
artificial intelligence, leaving out areas like web, mobile and system programming that rely on
other languages. As a first step toward a multilingual benchmark they build a Java version, choosing
Java for its popularity in industry and, over C and C++, because they believe language models are
not primarily designed to address the performance issues those languages are chosen for.

The resulting benchmark, [[Dataset/swe-bench-java-verified]], follows SWE-bench's construction
workflow in five phases: collecting candidate repositories, crawling issue instances from pull
requests, determining each issue's runtime environment, extracting fail-to-pass tests, and a
questionnaire-based manual verification following the SWE-bench Verified annotation guidelines. The
paper also describes problems found when migrating the pipeline to Java — an error in the original
SWE-bench script that sometimes crawls the wrong base commit, redundant downloads of repositories and
dependencies, and compilation breaking during incremental compilation — and how the authors addressed
them.

To check the benchmark's reliability, the authors run [[SoftwareApplication/swe-agent]] with several
models. Resolved rates are low across the board, which they read as evidence that the benchmark is
challenging and discriminates between models.

## Key Points

- The benchmark is presented as a first step toward multilingual GitHub issue resolving evaluation, starting with Java; the authors plan to add languages such as Go, Rust, C and C++.
- Construction narrowed 70 candidate repositories to 19, crawled 1,979 issue instances from them, kept 308 that compile under the determined environment, 137 with at least one fail-to-pass test and no pass-to-fail test, and after manual verification 91 issues across 6 repositories.
- Manual verification by 10 Java developers rated issue clarity, test coverage and major flaws, keeping only issues rated clear, well covered and free of major flaws.
- The authors report fixing a bug in the original SWE-bench collection script, which sometimes took the wrong base commit by ignoring branch differences, by using the git commit graph.
- With SWE-agent, resolved rates range from 1.10% (GPT-4o-mini, Doubao-pro) to 9.89% (DeepSeek-V2) of the 91 issues, with GPT-4o at 6.59% and DeepSeek-Coder-V2 at 7.69%.
- The authors observe that DeepSeek-V2 outperforms DeepSeek-Coder-V2 on the repository with the most extensive issue descriptions and the reverse on the one with the least text, which they take to suggest that more detailed task descriptions demand more natural-language understanding.

## Notes

The authors state that they implemented SWE-agent hastily, without configuring the runtime
environment for all Java issues, which affects the agent's ability to reproduce issues and may make
its results lower than its normal performance. The dataset, evaluation environment and leaderboard
are open-sourced, and the paper's project links point to multi-swe-bench.github.io and a Hugging
Face dataset named Daoguang/Multi-SWE-bench. The work is set among benchmarks for
[[DefinedTerm/software-issue-resolution]], and the paper cites the multilingual code generation
benchmarks HumanEval-X, MBXP and MultiPL-E as prior multilingual efforts outside issue resolving.
