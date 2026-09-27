---
title: "Kiro"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール, 仕様駆動開発]
translated_from: ".wikicommit/entity/en/SoftwareApplication/kiro.md"
source_commit: "4b83a0390f0437f8f63f9399a1db3e12e1ace784"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Amazon のエージェント型 AI 開発ツール。コード生成を始める前に、要件、設計、タスク作成の各段階へとユーザーを導く。"
  applicationCategory: "仕様駆動の AI 開発ツール、AI IDE"
  author: "Amazon Web Services"
  featureList: "コード生成前の要件・設計・タスク作成の段階的なフェーズ、.kiro/steering/ 配下の Steering ルールファイル（デフォルトで product.md、tech.md、structure.md を生成）"
---

Kiro は Amazon Web Services のエージェント型 AI 開発ツールであり、コーディングのセッションを、コード生成を始める前に
要件の把握、設計、タスク作成という段階に分けて進める。構造化された要件の把握と反復的な改善を重視し、AI が実装に
取りかかる前に明確なコンテキストを持っているようにする。この明示的な段階分けは、一度も指定されていない要件を AI が
推測で補うことを防ぐためのものであり、[[DefinedTerm/spec-driven-development]] がより一般的な形で取り組んでいるのと同じ
問題である。

## 機能

[[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] は Kiro を [[DefinedTerm/ai-ide]] として扱い、開発者が
[[DefinedTerm/ai-ide-rules]] を定義できる 5 つの AI IDE の 1 つとしている。Kiro はその仕組みを別の名前で呼ぶ唯一の
ツールである。そのルールは **Steering** と呼ばれ、`.kiro/steering/` 配下に置かれる。デフォルトではそこに
`product.md`、`tech.md`、`structure.md` の 3 つのファイルが生成され、ユーザーはそれに追加できる。同研究は、公式の
変更履歴に基づき Kiro のリリース日を 2025 年 7 月 14 日と記録している。同研究は、`product.md` が扱うのは研究対象で
ある開発上の制約ではなくビジネス要件と製品機能であるという理由で、このファイルを自らの分析から除外した。

## 採用状況とエコシステム

仕様駆動開発ツールに関する 2026 年の実務者向けサーベイ（[[ScholarlyArticle/from-code-to-contract]]）は、Kiro を
[[SoftwareApplication/github-spec-kit]] および [[SoftwareApplication/tessl]] と並ぶ、AI 支援型 SDD ツールキットの
代表的な 3 つのうちの 1 つに分類している。

Jimmy Song のオンラインハンドブック『智能体构建指南』のある章は、この実践の代表的な実装の筆頭に Kiro を挙げ、2025 年
7 月からプレビュー版が提供されている AWS のスタンドアロンの AI IDE であり、そのフローは Requirements → Design → Tasks
と進むと説明している。このツールに対する同章の評価は、ここに収録している記述の中で最も辛辣であり、何の測定にも
裏付けられていない判断として述べられている。同章はこの構成を直感的だが煩雑であり、単発のタスクに向いていると評している。

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] は、Kiro を、
[[DefinedTerm/product-requirement-prompt]]（PRP）を軸に構築された [[DefinedTerm/plan-do-assess-review]] パターンを
すでに実践している業界のツールとして引用している。PRP は通常、Goal & Why、What & Success Criteria、All Needed
Context、Implementation Blueprint、Validation Loop の 5 つのセクションで構成される。

ルール分類の研究では、調査対象の実務者 99 人のうち 37 人が Kiro を挙げた。同研究が調べた 5 つの AI IDE の中では
Cursor（57）に次ぐ 2 位であり、回答者が挙げたツール全体で見ると、VS Code と Copilot の組み合わせ（51）に次ぎ、
Antigravity（34）、Trae（24）、Windsurf（23）、Qoder（16）を上回る。マイニングの側面では、同研究の 83 プロジェクトの
うち 25 を占め、Cursor に次いで 2 番目に大きな割合となっている。
