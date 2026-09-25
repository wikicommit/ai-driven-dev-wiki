---
title: "SWE-bench-java-verified"
type: "schema:Dataset"
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
  description: "A Java version of the SWE-bench GitHub issue resolving benchmark, consisting of 91 manually verified issue instances from 6 open-source Java repositories, released with a Docker-based evaluation environment and a leaderboard."
---

SWE-bench-java-verified is a benchmark for resolving real GitHub issues in Java projects, built by
following the construction workflow of [[Dataset/swe-bench]] as a first step toward multilingual
issue resolving evaluation. It is introduced in
[[ScholarlyArticle/swe-bench-java-a-github-issue-resolving-benchmark-for-java]], whose authors
released it publicly together with a Docker-based evaluation environment and a leaderboard that they
said would be maintained and updated.

## Contents

Each instance is a GitHub issue with the repository state it was raised against; a model must
produce a patch, and an issue counts as resolved only if all the given test cases pass. During
construction, each qualifying pull request's details were crawled, including its patch, base commit,
test patch, issue statement, environment setup commit and fail-to-pass tests. The benchmark holds 91 issues across 6
repositories, concentrated in FasterXML/jackson-databind (49 issues) with the fewest in apache/dubbo
(4), and spans data serialization, web services, data formats and container tools. The repositories
use Maven or Gradle as their build tool, range from about 57,000 to 457,000 lines of code, and the
issue descriptions average about 2,500 characters.

## Provenance

The repositories were drawn from popular Java repositories on GitHub and from repositories in
[[Dataset/defects4j]], narrowed from 70 candidates to 19. From 1,979 crawled issue instances, the
authors kept those whose repository compiled under a determined runtime environment (build tool, JDK
version and compilation commands), then those with at least one fail-to-pass test and no
pass-to-fail test, leaving 137. Ten developers experienced in Java then screened these following the
SWE-bench Verified annotation guidelines, rating issue clarity, test coverage and major flaws, and
only instances meeting all three criteria were retained, giving the final 91.

## Use

The introducing paper evaluates [[SoftwareApplication/swe-agent]] with GPT-4o, GPT-4o-mini,
DeepSeek-V2, DeepSeek-Coder-V2 and Doubao-pro on the benchmark, reporting resolved rates between
1.10% and 9.89%, and notes that its SWE-agent setup did not configure the runtime environment for
all issues.
