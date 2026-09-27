---
title: "ランタイム監視としてのコードレビュー"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント, コードレビュー, 人間による監督]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/code-review-as-runtime-monitoring.md"
source_commit: "8d7644d8b85a563c829192e2cb8492577074f87c"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "[[ScholarlyArticle/trustworthy-ai-software-engineers]] において Aleti、Hoda、Ray、Chen が行った提案。人間と AI からなるソフトウェアエンジニアリングチームにおけるコードレビューを、マージ前の検査を超えて継続的なランタイムの活動へと拡張するもので、デプロイされたコードは暫定的なものとして扱われ、AI エージェントが本番環境でのその振る舞いを監視する。"
---

ランタイム監視としてのコードレビューは、[[ScholarlyArticle/trustworthy-ai-software-engineers]] で提案されたもので、人間と AI からなるソフトウェアエンジニアリングチームにおけるコードレビューを、コードがマージされた時点で終わらないものとして捉え直す。この提案のもとでは、デプロイされたコードは最終的なものではなく暫定的なものとして扱われる。AI エージェントが本番環境でのシステムの振る舞いを継続的に監視し、実行トレース、リソース使用量、セキュリティのシグナル、期待される振る舞いからの逸脱を評価する。これにより、信頼性は 1 回限りのマージ前の検査ではなく、持続的な振る舞いの検証を通じて確立される。

## 適用される場面

論文はこの転換を、人間と AI からなるチームにおいてコードレビューがボトルネックになりつつあることへの対応として動機づけている。AI が生成する成果物の量が大幅に増えることで、網羅的な手作業によるマージ前の検査は現実的でなくなり、一方で AI が生成した出力の不透明さが、その正しさについて推論することをより難しくしている。この提案は、AI エージェントと監視の仕組みがシステムの運用ライフサイクルに組み込まれ、マージ時の静的なコードだけでなく、デプロイ後の実行時の振る舞いを追跡することを前提としている。論文はこれを、実装されたり実証的に評価されたりした実践としてではなく、2026 年のビジョン論文における提案として提示している。論文は、レビューが「時間的に分散し、適応的で、システムの運用と密接に結びついた」ものになり、開発とデプロイの境界が解消されると述べている。

## 関連用語

[[ScholarlyArticle/trustworthy-ai-software-engineers]]、[[DefinedTerm/evidence-centric-inspection]]、[[DefinedTerm/agentic-engineer]]
