---
title: "cxdb"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, エージェントアーキテクチャ, コンテキストエンジニアリング]
translated_from: ".wikicommit/entity/en/SoftwareApplication/cxdb.md"
source_commit: "26a416de0f4a7992cb9f84fad31d68262aaf5c2a"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "StrongDM の AI コンテキストストア。エージェントの会話履歴とツール出力をイミュータブルな DAG に保持するシステムであり、人間によるコードレビューなしで作業するという同社チームの説明とあわせて、従来型の多言語コードベースとして公開された。"
  applicationCategory: "AI コンテキストストア"
  author: "[[Organization/strongdm]]"
---

cxdb は [[Organization/strongdm]] の AI コンテキストストアであり、会話履歴とツール出力をイミュータブルな DAG に保存するシステムである。このチームが採用している [[DefinedTerm/software-factory]] の体制についての最初の説明とあわせて公開された。同時に公開されたもう一方の [[SoftwareApplication/attractor]] とは異なり、cxdb は従来型のコードベースであり、Rust 16,000 行、Go 9,500 行、TypeScript 6,700 行からなる。

## 機能

cxdb について明らかになっているのは、そのインターフェースではなく、保存するものの形である。すなわち、エージェントの作業の永続的な記録（会話履歴と、エージェントが呼び出したツールの出力）が、その場で上書きされるのではなく、イミュータブルな有向非巡回グラフに保持される。記事の著者は、これを自身の LLM ツールにおける SQLite のロギング機構に似ているが、はるかに洗練されたものだと述べている。これは文書化された比較ではなく、著者の印象である。この比較は [[BlogPosting/how-strongdms-ai-team-build-serious-software-without-even-looking-at-the-code]] で示されている。バージョンは記録されていない。

## 採用とエコシステム

cxdb は、人間によるコードレビューなしで作業していると説明する同じチームによって公開されたものであり、保存するのは会話履歴とツール出力である。出典はその体制の中での cxdb の役割を述べておらず、ここでも何らかの役割を想定していない。構築したチーム以外での採用は記録されていない。エージェントセッションの永続的な状態については、より一般的に [[DefinedTerm/checkpoint-and-resume]] と [[DefinedTerm/context-engineering]] で論じられている。
