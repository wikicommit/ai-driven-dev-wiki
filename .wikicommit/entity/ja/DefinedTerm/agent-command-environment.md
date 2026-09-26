---
title: "Agent Command Environment（ACE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-command-environment.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）において、人間の「Agent Coach」のために提案されたワークベンチ。人間の認知に最適化されたコマンドセンターであり、意図の指定、エージェントによる並列作業のオーケストレーション、エビデンスに裏付けられた結果のレビューを支援する。"
---

Agent Command Environment（ACE）は、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] が [[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として提案する 2 つの専用ワークベンチの 1 つであり、エージェント向けの [[DefinedTerm/agent-execution-environment]]（AEE）と対をなす。ACE は人間の「Agent Coach」のためのコマンドセンターであり、コード中心の編集ではなく人間の認知に最適化されたワークベンチとして、エージェントの活動とそれに伴うコストを完全に可観測にする。

## 用法

論文は ACE を、1 人の開発者が多数のエージェントと協働する 1 対 N の協働と、人間のチームが AI チームメイトの共有フリートを調整する N 対 N の協働の両方を支援するものとして説明している。ACE は、コーチが [[DefinedTerm/briefingscript]] を作成・改訂し、[[DefinedTerm/loopscript]] を定義し、[[DefinedTerm/merge-readiness-pack]] のような構造化されたエビデンスバンドルをレビューする場である。また、エージェントが判断を人間の専門家にエスカレーションする必要がある場合には、ACE が [[DefinedTerm/consultation-request-pack]] をルーティングし、提示し、記録する。論文によれば、ACE には現在の標準的な開発ツールに欠けている機能が必要である。すなわち、規律ある N バージョンプログラミングの支援（複数のエージェントが生成した解の構成要素を開発者が可視化・比較・組み合わせられること）、単純なテキスト差分を超えるプログラム理解のためのビュー、戦略的なエージェントチーム管理（能力とコストに基づいてエージェントを編成・評価・再訓練・降格・引退させること）、そしてコーチが外科的なコード変更のために従来の IDE ビューへ「飛び込み」、その後コーチングのワークフローに戻れる能力である。さらに論文は、高レベルのオーケストレーションやメンタリングの作業を補完するインタラクション手段として音声を提案している。その根拠として、発話はタイピングより速くなりうること、音声支援によるデバッグはコンテキストスイッチを減らしうることを示すエビデンスを挙げ、音声によるエージェントとのインタラクションの実現可能性を示す既存ツールとして Talon Voice と Cursorless for VSCode を挙げている。

## 関連用語

[[DefinedTerm/agent-execution-environment]]、[[DefinedTerm/structured-agentic-software-engineering]]
