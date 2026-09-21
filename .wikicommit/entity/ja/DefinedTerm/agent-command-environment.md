---
title: "Agent Command Environment（ACE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-command-environment.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）における人間の「エージェントコーチ」のために提案されたワークベンチ。コード中心の編集ではなく人間の認知に最適化されたコマンドセンターであり、意図の仕様化、並列で進むエージェント作業のオーケストレーション、証拠に裏づけられた結果のレビューを支える。"
---

Agent Command Environment（ACE）は、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] が
[[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として提案する、目的別に作られた 2 つの
ワークベンチの一方であり、もう一方はエージェントのための [[DefinedTerm/agent-execution-environment]]（AEE）である。
ACE は人間の「エージェントコーチ」のためのコマンドセンターであり、コード中心の編集ではなく人間の認知に最適化された
ワークベンチとして、エージェントの活動とそれに伴うコストを完全に可観測にする。

## 用法

論文は ACE を、1 人の開発者が多数のエージェントと働く 1 対 N の協働と、人間のチームが AI チームメイトの共有フリートを
統率する N 対 N の協働の双方を支えるものとして説明している。ここはコーチが [[DefinedTerm/briefingscript]] を書き起こして
反復し、[[DefinedTerm/loopscript]] を定義し、[[DefinedTerm/merge-readiness-pack]] のような構造化された証拠バンドルを
レビューする場である。またこの環境は、エージェントが判断を人間の専門家にエスカレーションする必要が生じたときに
[[DefinedTerm/consultation-request-pack]] をルーティングし、提示し、記録する。論文は ACE について、今日の標準的な開発
ツールには欠けているケイパビリティが必要だと述べている。規律ある N バージョンプログラミングの支援（複数のエージェント
生成解から、開発者がコンポーネントを可視化し、比較し、混ぜ合わせられるようにすること）、単純なテキスト差分を超える
プログラム理解のためのビュー、戦略的なエージェントチーム管理（ケイパビリティとコストに応じてエージェントを編成し、
評価し、再訓練し、降格させ、退役させること）、そしてコーチが外科手術的なコード変更のために従来型の IDE ビューへ
「飛び込み」、その後コーチングのワークフローへ戻れることである。さらに論文は、高レベルのオーケストレーションや
メンターシップのタスクに対する補完的なインタラクションのモダリティとして音声を提案し、発話がタイピングより速くなり
うるという証拠と、音声支援によるデバッグがコンテキストスイッチを減らしうるという証拠を挙げ、音声ベースのエージェント
操作の実現可能性を示す既存ツールとして Talon Voice と VSCode 向けの Cursorless を名指ししている。

## 関連用語

[[DefinedTerm/agent-execution-environment]], [[DefinedTerm/structured-agentic-software-engineering]]
