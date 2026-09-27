---
title: "AI Teammate Lifecycle Engineering（ATLE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/ai-teammate-lifecycle-engineering.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている、エージェントに永続的な記憶と長期的なコンテキストを与え、ステートレスで一回限りの請負人から、タスクをまたいで学び成長する永続的なチームメイトへと進化させるためのエンジニアリング活動。"
---

AI Teammate Lifecycle Engineering（ATLE）は、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で提案されている構造化されたエンジニアリング活動の 1 つであり、同論文では「SE for Agents」という括りのもとで [[DefinedTerm/ai-teammate-infrastructure-engineering]]（ATIE）と対になっている。その目的として述べられているのは、エージェントが記憶を保持し、時間とともに学習できるようにすること、つまりエージェントを、あらゆるタスクをゼロから始める「一回限りの請負人」から、組織の知識を保持する「生涯のパートナー」へと移行させることである。

## 用法

同論文は ATLE の基盤を永続的な記憶に置いている。プロジェクトの履歴と意思決定ログについての長期記憶を組み込まれたエージェントは、コーチが同じ指導を繰り返し与えなくても、タスクをまたいで連続性を維持する。そして、[[SoftwareApplication/devin]] が用いる DeepWiki を、エージェントがタスクをまたいで自らのドキュメントと意思決定ログを構築・参照する初期の例として挙げている。ATLE はプロアクティブなメンテナンスも対象とする。永続的な記憶とコードベースへのアクセスを持つエージェントを、計算資源が遊休しているサイクルにスケジュールし、技術的負債を洗い出したり、ドキュメントの欠落を特定したり、リファクタリングを提案したりさせ、そうした提案を新たな [[DefinedTerm/briefingscript]] として起票して、人間のレビューを受ける標準のワークフローに乗せるというものである。同論文の ATLE に関する研究ロードマップは、プロジェクトの履歴、意思決定ログ、アーキテクチャ上の根拠を保持する仕組み（継続学習の手法と、グラフ、ベクトルストア、意思決定記録といった外部記憶構造の両方で、コンテキストウィンドウのあふれを避けるための SE 固有の圧縮を伴うもの）、チームの気を高優先度の開発からそらすことなくプロアクティブなメンテナンス作業をスケジュールし、その価値を評価するための研究、そして、エージェント型 SE が長年の原則の背後にあるコストモデルをどう変えるかについての — 逸話ではなく — 実証的・経済的なモデル（たとえば、コードの重複がエージェントにとっては一貫して更新しやすいものになること）を求めている。

## 関連用語

[[DefinedTerm/ai-teammate-infrastructure-engineering]], [[DefinedTerm/agent-execution-environment]], [[DefinedTerm/structured-agentic-software-engineering]]
