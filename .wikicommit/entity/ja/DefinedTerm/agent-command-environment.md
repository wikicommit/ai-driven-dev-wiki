---
title: "Agent Command Environment（ACE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-command-environment.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）において、人間の「Agent Coach」のために提案されたワークベンチ。人間の認知に最適化されたコマンドセンターであり、意図の指定、並列するエージェント作業のオーケストレーション、根拠に裏づけられた成果のレビューを支援する。"
---

Agent Command Environment（ACE）は、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] が [[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として提案する 2 つの専用ワークベンチの 1 つであり、エージェント向けの [[DefinedTerm/agent-execution-environment]]（AEE）と対をなす。ACE は人間の「Agent Coach」のためのコマンドセンターであり、コード中心の編集ではなく人間の認知に最適化されたワークベンチとして、エージェントの活動とそれに伴うコストを完全に可観測にする。

## 用法

論文によれば、ACE は、1 人の開発者が多数のエージェントと協働する 1 対 N の協働と、人間のチームが AI チームメイトの共有フリートを調整する N 対 N の協働の両方を支援する。コーチはここで [[DefinedTerm/briefingscript]] を作成・改訂し、[[DefinedTerm/loopscript]] を定義し、[[DefinedTerm/merge-readiness-pack]] のような構造化されたエビデンス一式をレビューする。また、エージェントが判断を人間の専門家にエスカレーションする必要があるときには、この環境が [[DefinedTerm/consultation-request-pack]] をルーティングし、提示し、記録する。論文は、ACE には今日の標準的な開発ツールに欠けている機能が必要だとする。すなわち、規律ある N バージョンプログラミングの支援（エージェントが生成した複数の解のコンポーネントを、開発者が可視化し、比較し、組み合わせられるようにすること）、単純なテキスト差分を超えたプログラム理解のためのビュー、戦略的なエージェントチーム管理（能力とコストに応じてエージェントを編成、評価、再訓練、降格、または引退させること）、そしてコーチが従来の IDE ビューに「飛び込んで」ピンポイントのコード変更を行い、その後コーチングのワークフローに戻れる機能である。さらに、高レベルのオーケストレーションやメンタリングのタスクを補完するインタラクション手段として音声を提案している。その根拠として、音声はタイピングより速くなりうること、音声支援によるデバッグはコンテキストスイッチを減らしうることを示すエビデンスを引き、音声ベースのエージェント操作が実現可能であることを示す既存のツールとして Talon Voice と Cursorless for VSCode を挙げている。

## 関連用語

[[DefinedTerm/agent-execution-environment]]、[[DefinedTerm/structured-agentic-software-engineering]]
