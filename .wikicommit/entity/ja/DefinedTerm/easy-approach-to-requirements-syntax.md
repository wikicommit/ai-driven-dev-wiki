---
title: "Easy Approach to Requirements Syntax（EARS）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["EARS"]
tags: [仕様駆動開発]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/easy-approach-to-requirements-syntax.md"
source_commit: "60f8fe534df34847178444f94322cbfa2a23ad59"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "WHEN、IF、WHILE、WHERE、SHALL といったキーワードから組み立てられる少数の固定された文型のいずれかで各要求を書く、要求工学の形式。仕様駆動開発において、AI エージェントが要求を解釈する余地を残さないために用いられる。"
---

Easy Approach to Requirements Syntax（EARS）とは、要求工学に由来する形式であり、各要求を少数の固定された文型の
いずれかで書くことで、そのトリガー、条件、そしてシステムの義務を、解釈に委ねるのではなく明示的に述べるものである。
仕様駆動開発についての実践者向けガイドは、いずれも `THE SYSTEM SHALL` 節で終わる 5 つのパターンを挙げている。
**ユビキタス**要求（"THE SYSTEM SHALL validate workspace permissions on every task operation"）、`WHEN` で始まる
**イベント駆動**要求、`WHILE` で始まる**状態駆動**要求、`IF` で始まる**望ましくない振る舞い**の要求、そして `WHERE` で
始まる**オプション**要求（"WHERE notifications are enabled, THE SYSTEM SHALL notify assignees on change"）である。

## 用法

[[DefinedTerm/spec-driven-development]] においては、AI エージェントがそこから構築を行う仕様の機能要求に用いられる。
[[BlogPosting/what-is-spec-driven-development-practitioners-guide]] は、この形式がまさにこの実践が闘っている曖昧さの
ために作られたものであるから、その場面に適していると論じる。その構造は契約書のように読め、どの文型もエージェントに
解釈の余地を残さない。同じガイドの作業例は、決済の課金エンドポイントの要求をこの方法で書いており、各要求には番号が
振られ、具体的な受け入れ例と対になっている。たとえば "WHEN the same Idempotency-Key is replayed within 24h, THE SYSTEM
SHALL return the original charge and create no new one" や "IF the amount is <= 0, THE SYSTEM SHALL reject with 422
\"amount must be positive\"" である。

Matteo Baccan による仕様駆動開発についてのイタリア語の投稿も、同様の主張をしている。同投稿は EARS を、仕様から自然言語の
曖昧さを取り除きたい人のための選択肢として提示する。"WHEN [event] THE system shall [action]" という形の構造は、各決定を
自動的にテストできる論理的な制約に結びつける。同投稿は、この構文が人工知能のために生まれたものではないことに触れたうえで、
人と人との誤解を防ぐために考案された記法が、開発者と機械とのコミュニケーションに適していることが判明したと論じている。

2 つの出典は、この形式の起源を異なる形で述べている。実践者向けガイドはこれを要求工学に由来する 30 年前の形式と呼んで
いる。Baccan の投稿は、2009 年に Rolls-Royce の Alistair Mavin が航空機エンジンの要求のために作ったものだとしている。

## 適用される場面

実践者向けガイドは、仕様の機能要求を書くためにこれを推奨している。そのワークフローでは、要求フェーズが振る舞いの一覧と、
それぞれを証明する受け入れ基準とを合わせて生み出す。ガイドの作業例では、EARS 形式の要求が、エージェントが満たさなければ
ならない具体的な受け入れ例の一覧と並べて置かれている。Baccan はこれを、この実践の必須要件ではなく、素の Markdown による
仕様からさらに一歩進めるための任意のステップとして提示している。AI エージェントとともにこれを用いることの根拠は、
測定された比較ではなく、これらの実践者による推奨にある——ガイドの著者はこれを、ほとんどどのガイドも教えていない、
最もレバレッジの高い技法と呼んでいる。
