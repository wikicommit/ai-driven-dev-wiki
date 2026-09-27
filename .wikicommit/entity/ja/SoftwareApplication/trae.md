---
title: "Trae"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール]
translated_from: ".wikicommit/entity/en/SoftwareApplication/trae.md"
source_commit: "0ea12caf5df433486d9ab0e30d7c6a7b7cf57315"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "ByteDance による AI IDE。ルールファイルは `.trae/rules/` 以下に置かれる。AI IDE のルールに関する 2026 年のマイニングと調査による研究で調べられた 5 つのツールの 1 つ。"
  applicationCategory: "AI IDE"
  author: "ByteDance"
---

Trae は ByteDance が公開している [[DefinedTerm/ai-ide]] である。[[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] が研究対象として選んだ 5 つのツールの 1 つであり、選定の根拠は、いずれのツールもコード生成やチャットでのやり取りの際に IDE が従わなければならない [[DefinedTerm/ai-ide-rules]] をデベロッパーが明示的に定義できることであった。この研究は、ツールの公式変更履歴に基づき、そのリリース日を 2025 年 1 月 20 日としている。

## 機能

Trae のルールファイルはプロジェクト内の `.trae/rules/` 以下に置かれる。その置き場所と、ルールが生成時やチャット時に遵守されるという点を除けば、ここで用いた情報源はこの仕組みを 5 つのツールすべてに共通するものとして一般的に説明しており、Trae 自身の実装については述べていない。共通の説明については [[DefinedTerm/ai-ide-rules]] を参照。

## 採用とエコシステム

その研究の数値のうち 2 つが採用状況に関わるが、両者は異なるものを測定している。リポジトリマイニングでは、最初の検索で Trae の候補プロジェクトが 1445 件見つかったが、キーワードとルールファイルによるフィルタリングと手作業による検査を経て、AI IDE で構築されたと明示している 83 件のプロジェクトからなる最終データセットに残ったのは 6 件であった。実務者サーベイでは、回答者 99 人のうち 24 人が現在 Trae を開発に使っていると回答した。マイニングの数値は、ツールを使用しており、かつ README や説明文でその旨を述べている公開プロジェクトの数を反映しており、研究は、AI IDE を使いながらそれを明示していないプロジェクトが過小に数えられると指摘している。一方、サーベイの数値は、ルールファイルへの変更をコミットしたことのある開発者の自己申告による利用状況を反映している。
