---
title: "Harness-as-a-Service"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/harness-as-a-service.md"
source_commit: "c6bf44a9d0262400c75a0abf7dee6a8fbb53ff80"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "エージェントを、生の LLM 補完 API の上に直接ではなく、ハーネスのランタイム（ループ、ツール、コンテキスト管理、フック、サンドボックスのプリミティブ）の上に構築するという捉え方（Viv Trivedy によるとされる）。"
---

Harness-as-a-Service（HaaS）は、Viv Trivedy によるとされる捉え方であり、エージェントの構築方法の転換を指す。補完を返す LLM API の上に構築することから、ランタイムを返すハーネス API の上に構築することへの転換である。この捉え方のもとでは、ハーネスのフレームワークがエージェントループ、ツール呼び出し、コンテキスト管理、フック、サンドボックスのプリミティブを最初から提供し、構築者はループ、ツール呼び出し、会話の状態、承認フローを一から組み立てるのではなく、システムプロンプト、ツール、コンテキスト、サブエージェントという 4 つの柱に沿ってそれらをカスタマイズする。

## 用法

ソースは、この方向を示す例として Claude Agent SDK、Codex SDK、OpenAI Agents SDK を挙げている。そして、この転換こそがエージェントの設計の反復を扱いやすくするものだと位置づけている。何かがうまくいかなくなるたびにエージェントを一から作り直すのではなく、すでにうまく整理された設定面を調整することになるからである。

## 適用される場面

これが当てはまるのは、ループ、ツールの実行、コンテキスト管理のニーズをハーネスのフレームワークがすでにカバーしており、差別化のための作業がドメイン固有のプロンプトとツールの設計に残される、エージェントベースの新しいプロダクトやワークフローを構築する場合である。ソースは、いずれにせよ不完全な最初のバージョンから始めるべきだという Viv Trivedy の主張、「good agent building is an exercise in iteration. You can't do iterations if you don't have a v0.1」（良いエージェント構築とは反復の営みである。v0.1 がなければ反復はできない）を引用し、ハーネスが完全に整うまでこのパターンの採用を遅らせるべきではない理由としている。

## 関連用語

[[DefinedTerm/harness-engineering]]
