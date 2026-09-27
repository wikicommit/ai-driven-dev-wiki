---
title: "Merge-Readiness Pack（MRP）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/merge-readiness-pack.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている、エージェントがタスクの完了時に提出する構造化された証拠一式。機能的完全性、健全な検証、SE の衛生、根拠、監査可能性という 5 つの基準にわたって、現在のエージェントの出力と真にマージ可能な貢献との間のギャップを埋める。"
---

Merge-Readiness Pack（MRP）とは、エージェントの作業の目標となる成果物として [[DefinedTerm/structured-agentic-software-engineering]]（SASE）が提案しているアーティファクトであり、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で導入されている。論文は、人間のレビュアーが何十件もの生のプルリクエストを監査するのではなく、エージェントの作業が信頼に足ることを証明する、構造化された 1 つの MRP の監査にレビューを集中させるべきだと主張している。

## 用法

論文は、MRP が証拠を示さなければならない 5 つの基準を定義している。

- **Functional Completeness**（機能的完全性）：機能が完成しており、現実的なシナリオにおいて仕様どおりに振る舞うことの証明（たとえばエンドツーエンドテストの結果）。狭い範囲のテストにしか合格しない、表面的または部分的な修正を生み出しがちなエージェントの傾向に対処するものである。
- **Sound Verification**（健全な検証）：合格したテストのログだけでなく、エージェント自身のテスト計画と、エージェントが生成した新しいテストケース。検証戦略そのものが健全であることを証明する。
- **Exemplary SE Hygiene**（模範的な SE の衛生）：静的解析、リンティング、複雑度チェッカーのレポート。コードがクリーンで読みやすく、技術的負債を最小限に抑えていることを示す。
- **Clear Rationale and Communication**（明確な根拠とコミュニケーション）：PR の説明に相当する、人間が読める要約。しばしば冗長になりがちなエージェントの推論の軌跡を、採用したアプローチとトレードオフの説明へと集約する。
- **Full Auditability**（完全な監査可能性）：「凍結された」監査証跡。使用された [[DefinedTerm/briefingscript]]/[[DefinedTerm/mentorscript]]、ツール、エージェントの軌跡そのものへのバージョン付きリンクであり、結果を確実に再現できることを保証する。

その結果生じる情報の密度に対処するため、論文は、MRP が「段階的開示」をサポートしなければならないと述べている。これにより、レビュアーはまず高レベルの要約を確認し、そのうえでテストログや実行トレースといった特定の証拠を掘り下げることができる。人間は MRP に対して [[DefinedTerm/version-controlled-resolution]] で応答する。

## 関連用語

[[DefinedTerm/version-controlled-resolution]], [[DefinedTerm/agentic-guidance-engineering]], [[DefinedTerm/consultation-request-pack]]
