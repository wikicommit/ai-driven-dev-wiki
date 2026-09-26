---
title: "ハーネステンプレート"
type: "schema:DefinedTerm"
lang: ja
tags: [ハーネスエンジニアリング, コーディングエージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/harness-templates.md"
source_commit: "5a469d929e172ff921cd501cb6f2c1e9edd4c65b"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Birgitta Böckeler が提案する、サービステンプレートの将来ありうる発展形。組織でよく使われるサービストポロジーの 1 つについて、その構造、規約、技術スタックにコーディングエージェントを結びつけるガイドとセンサーの束。"
---

ハーネステンプレート（harness templates）とは、[[BlogPosting/harness-engineering-for-coding-agent-users]] でなされた提案において、「コーディングエージェントを、あるトポロジーの構造、規約、技術スタックにつなぎとめる（leash a coding agent to the structure, conventions and tech stack of a topology）」[[DefinedTerm/guides-and-sensors]]（ガイドとセンサー）の束である。同記事の出発点は、ほとんどの企業には必要なものの大半をカバーする少数の共通サービストポロジー — API を通じてデータを公開するビジネスサービス、イベント処理サービス、データダッシュボード — があり、成熟したエンジニアリング組織はそれらをすでにサービステンプレートとして体系化していることが多い、という観察である。同記事は、これらがハーネステンプレートへと発展するかもしれないこと、そしてチームが技術スタックや構造を、それらに対してすでにどのハーネスが利用可能かによって部分的に選ぶようになるかもしれないことを示唆している。

## 使われ方

同記事はこの考えを Ashby の最小有効多様性の法則（Law of Requisite Variety）によって裏づけている。同記事の要約によれば、この法則は、調整器は自らが統御するシステムと少なくとも同じだけの多様性を持たなければならず、自らがモデルを持つものしか調整できない、というものである。LLM ベースのコーディングエージェントはほとんど何でも生成できるが、1 つのトポロジーに絞り込むことでその空間が狭まり、包括的なハーネスがより実現可能になる — 「多様性を削減する一手（a variety-reduction move）」である。

## 適用される場面

これは起こる「かもしれない」ものとして示された推測的な提案であり、報告された実践ではない。組織がすでに少数の繰り返し現れるトポロジーを持っていることを前提としている。著者は、ハーネステンプレートもサービステンプレートと同じ問題 — インスタンス化されたコピーが上流の改善と同期しなくなること、そしてバージョン管理やコントリビューションの難しさ — に直面すると予想しており、非決定論的なガイドとセンサーはテストがより難しいため、問題はさらに悪化する可能性があるとしている。

## 関連用語

- [[DefinedTerm/guides-and-sensors]]
- [[DefinedTerm/harnessability]]
- [[DefinedTerm/harness-engineering]]
