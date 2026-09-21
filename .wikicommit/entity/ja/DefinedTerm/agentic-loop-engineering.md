---
title: "Agentic Loop Engineering（ALE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agentic-loop-engineering.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）が提唱する、エージェントによるタスク実行のあり方を規定するためのエンジニアリング活動。タスクの分解、並列化、求められる厳密さ、そして証拠に基づく受け入れ基準を、宣言的な LoopScript として定義するもので、DevOps の実践に根ざしている。"
---

Agentic Loop Engineering（ALE）は、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] が [[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として提唱する、構造化されたエンジニアリング活動の 1 つである。論文は ALE を、DevOps コミュニティが切り拓いた原則に深く根ざしたものとして説明しており、エージェントの作業を不透明なブラックボックスの過程から、規律ある、監査可能で再現可能なワークフローへと変えるものであって、[[DefinedTerm/plan-do-assess-review]]（PDAR）ループのような単純な反復サイクルを超えていくものだとしている。

## 用法

論文は、ワークフローの定義を [[DefinedTerm/agent-command-environment]]（ACE）の中にいる人間のコーチに割り当て、エージェントはそれを [[DefinedTerm/agent-execution-environment]]（AEE）の中で実行するものとしている。その成果物が [[DefinedTerm/loopscript]] である。掲げられている目的は、エージェント同士が（あるいは単独で）どう働くか、その協働のパターン、そしてツール群とどう関わるかを定義することにある。エージェントはタスクの「賭け金の大きさ」を自力で推し量ることができないからである。この活動について論文が示す研究ロードマップが求めているのは、タスクの分解、並列実行、レビューのチェックポイント、エスカレーションの規則、証拠の要件を捉える宣言的な LoopScript 言語であり、それはビジネスプロセスと DevOps の自動化を土台としつつ、コード・テスト・リスク・人間のレビューとのより強い結び付きを持つものである。加えて、コーチがループ全体をやり直すことなくワークフローを一時停止し、分岐の向きを変え、文脈を追加し、価値の低い作業を止められるようにする対話の仕組みと、[[DefinedTerm/merge-readiness-pack]] において十分とされる証拠の基準、さらにはエージェントの探索を導くための、より情報量の多いツールからのフィードバック（構造化されたコンパイラの診断、テストの失敗、静的解析の指摘）も求めている。

## 関連用語

[[DefinedTerm/loopscript]]、[[DefinedTerm/plan-do-assess-review]]、[[DefinedTerm/structured-agentic-software-engineering]]
