---
title: "Merge-Readiness Pack（MRP）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/merge-readiness-pack.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている、エージェントがタスクの完了時に提出する構造化された証拠の束。機能的完全性、健全な検証、SE の衛生、根拠、監査可能性の 5 つの基準にわたって、現在のエージェントの出力と真にマージ可能な貢献との間の隔たりを埋める。"
---

Merge-Readiness Pack（MRP）とは、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）がエージェントの作業の目標とする成果物として提案するものであり、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で導入された。同論文は、人間のレビュアーが何十もの生のプルリクエストを監査するのではなく、エージェントの作業が信頼に足ることを証明する 1 つの構造化された MRP の監査にレビューを集中させるべきだと論じている。

## 用法

同論文は、MRP が証拠を示さなければならない 5 つの基準を定めている。**機能的完全性（Functional Completeness）**：機能が完成しており、現実的なシナリオで仕様どおりに振る舞うことの証明（たとえばエンドツーエンドテストの結果）であり、狭い範囲のテストにしか通らない表面的ないし部分的な修正をエージェントが生み出しがちな傾向に対処する。**健全な検証（Sound Verification）**：テストに通ったというログだけでなく、エージェント自身のテスト計画と、それが生成した新たなテストケースであり、検証の戦略そのものが健全であることを証明する。**模範的な SE の衛生（Exemplary SE Hygiene）**：静的解析、lint、複雑度チェッカーのレポートであり、コードがクリーンで読みやすく、技術的負債を最小限に抑えていることを示す。**明確な根拠とコミュニケーション（Clear Rationale and Communication）**：PR の説明に相当する人間が読める要約であり、エージェントのしばしば冗長な推論の軌跡を、アプローチとトレードオフの説明へとまとめ上げる。**完全な監査可能性（Full Auditability）**：「凍結された」監査証跡 — 使用された [[DefinedTerm/briefingscript]]/[[DefinedTerm/mentorscript]]、ツール、エージェントの軌跡そのものへのバージョン付きリンク — であり、結果を確実に再現できることを保証する。こうして生じる情報の密度に対処するため、同論文は MRP が「段階的開示（progressive disclosure）」をサポートしなければならないと述べている。これにより、レビュアーはテストログや実行トレースのような個別の証拠を掘り下げる前に、高水準の要約を見ることができる。人間は MRP に対して [[DefinedTerm/version-controlled-resolution]] で応答する。

## 関連用語

[[DefinedTerm/version-controlled-resolution]]、[[DefinedTerm/agentic-guidance-engineering]]、[[DefinedTerm/consultation-request-pack]]
