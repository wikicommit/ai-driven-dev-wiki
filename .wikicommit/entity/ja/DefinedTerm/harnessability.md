---
title: "ハーネサビリティ"
type: "schema:DefinedTerm"
lang: ja
aliases: ["Harnessability", "ハーネス適合性"]
tags: [ハーネスエンジニアリング, コーディングエージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/harnessability.md"
source_commit: "5a469d929e172ff921cd501cb6f2c1e9edd4c65b"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "コードベースがコーディングエージェントのためにハーネスを適用しやすい度合い。強い型付け、明確なモジュール境界、詳細を抽象化するフレームワークといった性質によって、構築可能なガイドとセンサーが得られるかどうかを指す。"
---

ハーネサビリティ（harnessability）とは、コードベースがコーディングエージェントのためのハーネスの適用にどれだけ向いているかの度合いであり、[[BlogPosting/harness-engineering-for-coding-agent-users]] で用いられている用語である。同記事の要点は、ハーネスの制御がコードベース自体の性質に依存するということである。強い型付けの言語で書かれたコードベースには型チェックが自然にセンサーとして備わり、明確に定義可能なモジュール境界はアーキテクチャ上の制約ルールを可能にし、Spring のようなフレームワークはエージェントが気にする必要のない詳細を抽象化して、暗黙のうちにその成功の可能性を高める。そうした性質がなければ、対応する制御は構築できない。

## 使われ方

同記事はこの考えを、著者が同僚の Ned Letcher によるものとする用語、**アンビエントアフォーダンス（ambient affordances）** と結びつけている。これは「環境それ自体の構造的な性質であって、その中で動作するエージェントにとって環境を読み取り可能で、移動可能で、扱いやすいものにするもの（structural properties of the environment itself that make it legible, navigable, and tractable to agents operating within it）」である。同記事はまた、ハーネサビリティと複雑さは、ハーネスが調整する対象 — 保守性、アーキテクチャの適合性、振る舞い — によって異なるとも述べている。

ハーネサビリティの現れ方は、グリーンフィールドのシステムとレガシーシステムとで異なる。グリーンフィールドのチームは最初からそれを組み込むことができる。技術やアーキテクチャの選択が、コードベースをどれだけ統御しやすくするかを決めるからである。レガシーのチーム、とりわけ多くの技術的負債を抱えたアプリケーションを持つチームは、同記事の言葉を借りれば「ハーネスは、それが最も必要とされるところで最も構築が難しい（the harness is most needed where it is hardest to build）」という、より困難な問題に直面する。

## 関連用語

- [[DefinedTerm/guides-and-sensors]]
- [[DefinedTerm/harness-templates]]
- [[DefinedTerm/harness-engineering]]
