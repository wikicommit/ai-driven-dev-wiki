---
title: "ProjectDev"
type: "schema:Dataset"
lang: en
tags: [benchmarks, evaluation, code-generation, multi-agent]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2406.11912'
    hash: sha256:0bb6ae4b557525a907cd35ba8c21dc61c06135078855bd330d09e93218f0e09d
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A collection of 14 software development tasks, each a prompt plus a list of requirements, compiled by the authors of AgileCoder to evaluate whether multi-agent systems can generate complete, executable multi-file programs."
---

ProjectDev is a set of 14 representative software development tasks that are more intricate than
competitive programming problems, compiled by the authors of
[[ScholarlyArticle/agilecoder-dynamic-collaborative-agents-for-software-development-based-on-agile-methodology]]
to evaluate multi-agent software development systems. Each task asks the system under test to
generate a comprehensive codebase of multiple executable files, and the authors present it as a
better fit for assessing such systems than HumanEval and MBPP.

## Contents

Each task consists of a short prompt — for example "Create a snake game" — and a detailed list of
requirements grouped under headings such as game board, collision handling, scoring or error
handling. The tasks cover diverse areas, including mini-games (snake, brick breaker, 2048, Flappy
Bird, tank battle, Caro), data and CRUD applications built on Streamlit, pandas or SQLite, a custom
press-release generator, a video player, a YouTube video downloader, a QR code generator and
detector, a to-do list app and a calculator.

## Provenance

The authors describe collecting the tasks themselves to address the gap between code-generation
benchmarks and real-world software development, and state that the dataset will be released
publicly, in contrast to MetaGPT's SoftwareDev and ChatDev's SRDD, which they say are not publicly
available.

## Use

In the AgileCoder paper, each method is run three times per task and the resulting programs are
assessed manually by developers with at least two years of Python experience: a program that runs
is scored by the percentage of the task's requirements it meets, and the number of programs that
fail to run is counted as errors. On this basis the paper reports higher executability for
[[SoftwareApplication/agilecoder]] than for [[SoftwareApplication/chatdev]] and
[[SoftwareApplication/metagpt]].
