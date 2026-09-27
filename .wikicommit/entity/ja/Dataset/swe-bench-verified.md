---
title: "SWE-Bench Verified"
type: "schema:Dataset"
lang: ja
tags: []
translated_from: ".wikicommit/entity/en/Dataset/swe-bench-verified.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "SWE-Bench の一部のタスクが曖昧または仕様不足であるという懸念に対処するため、OpenAI が SWE-Bench の著者らと共同で公開した、人手で検証された 500 タスクからなる SWE-Bench のサブセット。"
  creator: "OpenAI"
  url: "https://openai.com/index/introducing-swe-bench-verified/"
---

SWE-Bench Verified は、[[Dataset/swe-bench]] から人手で検証された 500 タスクからなるサブセットであり、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で論じられている。元の SWE-Bench の一部のタスクが曖昧または仕様不足であるという懸念に対処するために OpenAI によって公開されたもので、その選定にあたっては OpenAI が SWE-Bench の著者ら自身と直接協力した。

## 内容

このサブセットは、SWE-Bench から抽出され、仕様が十分で解決可能であると人手で検証された 500 のタスクを収めている。

## 来歴

SWE-Bench Verified は、OpenAI が SWE-Bench の著者らと共同で導入した。[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] によれば、OpenAI はその後、このベンチマークがデータ汚染にますますさらされていると警告し、より信頼性の高い評価として代わりに [[Dataset/swe-bench-pro]] を推奨した。

## 利用

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] は、エージェント型コーディングのベンチマークにおける急速な進歩を示す例として、このサブセットでの結果を引用している。2024 年 8 月の公開時点で GPT-4o が解決したタスクは 33% だったのに対し、2025 年半ばには、トップクラスのエージェント型ソリューションが 70% を超えるタスクを解決していた。
