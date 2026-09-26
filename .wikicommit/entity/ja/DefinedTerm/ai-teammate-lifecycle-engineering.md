---
title: "AI Teammate Lifecycle Engineering（ATLE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
translated_from: ".wikicommit/entity/en/DefinedTerm/ai-teammate-lifecycle-engineering.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Structured Agentic Software Engineering（SASE）で提唱されている、エージェントに永続的なメモリと長期的なコンテキストを与えるためのエンジニアリング活動。エージェントを、ステートレスな単発の請負人から、タスクをまたいで学び成長する永続的なチームメイトへと進化させる。"
---

AI Teammate Lifecycle Engineering（ATLE）は、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で提唱されている構造化されたエンジニアリング活動の 1 つであり、同論文では「SE for Agents」という括りのもとで [[DefinedTerm/ai-teammate-infrastructure-engineering]]（ATIE）と対になっている。その目的は、エージェントがメモリを保持し、時間をかけて学習できるようにすることで、あらゆるタスクをゼロから始める「単発の請負人」から、組織の知識を保持する「生涯のパートナー」へとエージェントを移行させることだとされている。

## 用法

同論文は ATLE の基盤を永続的なメモリに置いている。これは、プロジェクトの履歴と意思決定ログの長期記憶を組み込んだエージェントが、コーチが同じ指導を繰り返し与えなくてもタスクをまたいで継続性を保つというものであり、エージェントがタスクをまたいで自らのドキュメントと意思決定ログを構築・参照する初期の例として、[[SoftwareApplication/devin]] が使う DeepWiki を挙げている。ATLE はプロアクティブな保守も対象とする。永続的なメモリとコードベースへのアクセスを持つエージェントを計算資源のアイドル時間にスケジュールし、技術的負債を走査させたり、ドキュメントの欠落を特定させたり、リファクタリングを提案させたりするもので、そうした提案は新たな [[DefinedTerm/briefingscript]] として登録され、人間によるレビューのための標準ワークフローに入る。同論文の ATLE に関する研究ロードマップは、プロジェクトの履歴、意思決定ログ、アーキテクチャ上の根拠を保持する仕組み（継続学習の手法と、グラフ、ベクトルストア、意思決定記録といった外部メモリ構造の両方を含み、コンテキストウィンドウのあふれを避けるための SE に特化した圧縮を伴うもの）、チームをより優先度の高い開発から逸らすことなくプロアクティブな保守作業をスケジュールし、その価値を評価する方法の研究、そして、エージェント型 SE が長年の原則の背後にあるコストモデルをどのように変えるかについての、逸話ではなく実証的・経済的なモデル（例：コードの重複は、エージェントにとっては一貫して更新するのが容易になる）を求めている。

## 関連用語

[[DefinedTerm/ai-teammate-infrastructure-engineering]]、[[DefinedTerm/agent-execution-environment]]、[[DefinedTerm/structured-agentic-software-engineering]]
