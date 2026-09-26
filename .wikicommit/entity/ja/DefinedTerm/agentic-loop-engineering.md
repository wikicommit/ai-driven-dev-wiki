---
title: "Agentic Loop Engineering（ALE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agentic-loop-engineering.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案された、エージェントがタスクをどのように実行するかを統制するためのエンジニアリング活動。タスク分解、並列化、求められる厳密さ、証拠に基づく受け入れ基準を宣言的な LoopScript として定義するもので、DevOps の実践に根ざしている。"
---

Agentic Loop Engineering（ALE）は、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で提案された、構造化されたエンジニアリング活動の 1 つである。同論文は ALE を、DevOps コミュニティが切り拓いた原則に深く根ざしたものと説明している。ALE は、エージェントの作業を不透明なブラックボックスのプロセスから、規律があり、監査可能で、再現可能なワークフローへと変え、[[DefinedTerm/plan-do-assess-review]]（PDAR）ループのような単純な反復サイクルを超えるものだという。

## 使われ方

同論文は、ワークフローの定義を [[DefinedTerm/agent-command-environment]]（ACE）内の人間のコーチに割り当て、エージェントはそれを [[DefinedTerm/agent-execution-environment]]（AEE）内で実行するとしている。この活動の成果物は [[DefinedTerm/loopscript]] である。その目的として掲げられているのは、エージェントがどのように協働する（あるいは単独で作業する）か、その協働のパターン、そしてエージェントが自らのツール群をどう使うかを定義することであり、これはエージェントがタスクの「重要度」を自力では推し量れないためである。同論文がこの活動について示す研究ロードマップは、次のものを求めている。タスク分解、並列実行、レビューのチェックポイント、エスカレーションのルール、証拠要件を記述する宣言的な LoopScript 言語（ビジネスプロセスや DevOps の自動化を土台としつつ、コード、テスト、リスク、人間によるレビューとのより強い結び付きを持つもの）。ループ全体をやり直すことなく、コーチがワークフローを一時停止したり、ブランチの向きを変えたり、コンテキストを追加したり、価値の低い作業を止めたりできる対話の仕組み。そして、[[DefinedTerm/merge-readiness-pack]] における十分な証拠の基準と、エージェントの探索を導くための、より情報量の多いツールからのフィードバック（構造化されたコンパイラ診断、テストの失敗、静的解析の指摘など）である。

## 関連用語

[[DefinedTerm/loopscript]]、[[DefinedTerm/plan-do-assess-review]]、[[DefinedTerm/structured-agentic-software-engineering]]
