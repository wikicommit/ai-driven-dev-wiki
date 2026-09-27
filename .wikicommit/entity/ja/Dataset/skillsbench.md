---
title: "SkillsBench"
type: "schema:Dataset"
lang: ja
tags: [エージェントスキル, ベンチマーク, 評価]
translated_from: ".wikicommit/entity/en/Dataset/skillsbench.md"
source_commit: "e3a247123c2e2c5a1d19244743218b709c140afd"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Agent Skills が LLM エージェントの役に立つかどうかを測定するためのベンチマーク。複数のドメインにまたがるタスクで構成され、各タスクにはキュレーションされたスキルと決定論的な検証器が組み合わされている。"
---

SkillsBench は、[[ScholarlyArticle/skillsbench-benchmarking-how-well-agent-skills-work-across-diverse-tasks]] で導入されたベンチマークであり、[[DefinedTerm/agent-skills]]（推論時に LLM エージェントを拡張する、手続き的知識の構造化されたパッケージ）が、専門知識を多く要するエージェント型の作業で実際にどれほど役立つかを測定する。

## 内容

論文に記述されている現時点のベンチマークの構成は、8 つのドメインにまたがる 87 のタスクである。各タスクにはキュレーションされたスキルと決定論的な検証器が組み合わされており、同じタスクをスキルありとスキルなしの両方で実行し、どちらの条件でも同じ方法で採点できるようになっている。

## 用途

[[ScholarlyArticle/skillsbench-benchmarking-how-well-agent-skills-work-across-diverse-tasks]] は、87 のタスクを、条件をそろえたスキルなしとキュレーション済みスキルありの 2 条件で、18 のモデルとハーネスの構成について実行している。その報告によれば、キュレーションされたスキルは平均合格率を 33.9% から 50.5% に引き上げ、構成ごとの向上幅は +4.1 から +25.7 パーセントポイントであった。また、モジュールが 3 つ以下の焦点を絞ったスキルは、より大きな、あるいは網羅的なバンドルを上回り、スキルを持つ小さなモデルはスキルを持たない大きなモデルに匹敵しうるという。
