---
title: "ランタイム監視としてのコードレビュー"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント, コードレビュー, 人間による監督]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/code-review-as-runtime-monitoring.md"
source_commit: "8d7644d8b85a563c829192e2cb8492577074f87c"
translated_at: "2026-09-22"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "[[ScholarlyArticle/trustworthy-ai-software-engineers]] において Aleti、Hoda、Ray、Chen が提案した、人間と AI からなるソフトウェアエンジニアリングチームにおけるコードレビューを、マージ前の検査を越えて継続的なランタイムの活動へと拡張する構想。デプロイされたコードは暫定的なものとして扱われ、AI エージェントが本番環境でのその振る舞いを監視する。"
---

ランタイム監視としてのコードレビューは、[[ScholarlyArticle/trustworthy-ai-software-engineers]] で提案されたもので、人間と
AI からなるソフトウェアエンジニアリングチームにおけるコードレビューを、コードがマージされた時点で終わらないように捉え直す。
この提案のもとでは、デプロイされたコードは最終的なものではなく暫定的なものとして扱われる。AI エージェントが本番環境での
システムの振る舞いを継続的に監視し、実行トレース、リソース使用量、セキュリティのシグナル、期待される振る舞いからの逸脱を
評価することで、信頼性は 1 回のマージ前の検査によってではなく、持続的な振る舞いの検証によって確立される。

## 適用される場面

論文はこの転換を、人間と AI からなるチームにおいてコードレビューがボトルネックになっていることへの応答として動機づけている。
AI が生成する成果物の量は大幅に増加し、網羅的な手作業でのマージ前検査を非現実的にする一方、AI が生成した出力の不透明さは、
その正しさについて推論することをより難しくする。この構想は、AI エージェントと監視機構がシステムの運用ライフサイクルの内部に
組み込まれ、マージ時点の静的なコードだけでなくデプロイ後の実行時の振る舞いを追跡することを前提としている。論文はこれを、
2026 年のビジョン論文における提案として——レビューは「時間的に分散し、適応的で、システムの運用と密に結合したもの」になり、
開発とデプロイの境界を溶かすと述べている——提示しているのであって、すでに実装されたり実証的に評価されたりした実践としてでは
ない。

## 関連用語

[[ScholarlyArticle/trustworthy-ai-software-engineers]]、[[DefinedTerm/evidence-centric-inspection]]、[[DefinedTerm/agentic-engineer]]
