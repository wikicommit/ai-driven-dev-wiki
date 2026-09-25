---
title: "Defects4J"
type: "schema:Dataset"
lang: en
tags: [program-repair, benchmark, java]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2403.17134'
    hash: sha256:aafce2ddc1642de21ae7f1c9a81dae3d270cea048a82a78f1d2819b04e881cc1
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A widely used benchmark of 835 real-world bugs from 17 Java projects for evaluating automated program repair techniques, split into 395 bugs from 6 projects in version 1.2 and another 440 bugs and 11 projects added in version 2."
---

Defects4J is a dataset of real-world bugs from Java projects that is widely used as a benchmark for evaluating [[DefinedTerm/automated-program-repair]] techniques. The account here comes from [[ScholarlyArticle/repairagent-an-autonomous-llm-based-agent-for-program-repair]], which evaluates on the entire dataset.

## Contents

The dataset consists of 835 real-world bugs from 17 Java projects: 395 bugs from 6 projects in Defects4J v1.2, and another 440 bugs and 11 projects added in Defects4J v2. Each bug comes with at least one failing test case. The projects include Chart, Cli, Closure, Codec, Collections, Compress, Csv, Gson, JacksonCore, JacksonDatabind, JacksonXml, Jsoup, JxPath, Lang, Math, Mockito and Time, with Closure the largest at 174 bugs. The RepairAgent authors report that its ground-truth fixes add and remove 2.9 and 9.3 lines on average and modify 381 tokens on average.

## Use

[[ScholarlyArticle/repairagent-an-autonomous-llm-based-agent-for-program-repair]] fixes 164 of the 835 bugs correctly and compares against ChatRepair, ITER and SelfAPR, using patches provided by those approaches' authors. To assess generalizability and the potential influence of data leakage — the model it used, GPT-3.5, may have seen parts of these Java projects during training — that paper additionally evaluates on the newer GitBug-Java dataset of bugs fixed in 2023. Separately, it lists as a limitation that Defects4J's guarantee of at least one failing test case per bug may not hold in real-world usage, leaving evaluation on bugs without such tests to future work.
