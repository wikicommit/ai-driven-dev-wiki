---
title: "SkillsBench：多様なタスクにおける Agent Skills の有効性のベンチマーク"
type: "schema:ScholarlyArticle"
lang: ja
tags: [エージェントスキル, ベンチマーク, 評価]
review_status: pending
translated_from: ".wikicommit/entity/en/ScholarlyArticle/skillsbench-benchmarking-how-well-agent-skills-work-across-diverse-tasks.md"
source_commit: "e3a247123c2e2c5a1d19244743218b709c140afd"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Agent Skills が LLM エージェントの役に立っているかどうかを、Skills なしとキュレーションされた Skills ありの対応する条件でタスクを実行して測定するベンチマーク SkillsBench を提示し、キュレーションされた Skills が平均合格率を引き上げると報告する arXiv 論文。"
  datePublished: "2026-02-13"
  keywords: ["エージェントスキル", "ベンチマーク", "対応のある評価", "LLM エージェント"]
---

本論文は [[DefinedTerm/agent-skills]] を、推論時に大規模言語モデルのエージェントを拡張する、手続き的知識の構造化されたパッケージとして説明する。そして、急速に普及しているにもかかわらず、それが実際に役立っているかを測定する標準的な方法が存在しないと指摘している。

このギャップを埋めるために、本論文は [[Dataset/skillsbench]] を提示する。これは、現時点で 8 つのドメインにわたる 87 のタスクを収録したベンチマークで、各タスクにはキュレーションされた Skills と決定論的な検証器が組み合わされている。本論文の最新の集計評価では、18 のモデルとハーネスの構成について、87 のタスクすべてを Skills なしとキュレーションされた Skills ありの対応する条件で実行している。著者らはこの対応のある評価を、専門知識を多く要するエージェント型の作業における Skill の有効性を厳密に測定するための基盤として提示している。

## 要点

- 評価した 18 のモデルとハーネスの構成全体で、キュレーションされた Skills により平均合格率は 33.9% から 50.5% に上昇した。これは 16.6 パーセントポイントの増加（正規化した向上幅では 25.5%）である。
- 向上幅は構成によって異なり、+4.1 から +25.7 パーセントポイントの範囲にわたる。
- モジュールが 3 つ以下の焦点を絞った Skills は、より大きな、あるいは網羅的なバンドルを上回る。
- Skills を備えた小規模なモデルは、Skills を持たない大規模なモデルに匹敵しうる。
- 著者らは、SkillsBench が対応のある評価、すなわち同じタスクを Skills ありとなしで実行することを、Skill の有効性を測定するための基盤として確立すると論じている。

## 補足

本論文は 2026 年 2 月 13 日に arXiv に初めて投稿され、最後に改訂されたのは 2026 年 6 月 14 日（第 4 版）である。著者は 77 名で、分類は Artificial Intelligence（cs.AI）である。
