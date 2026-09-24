---
title: "Harness-as-a-Service"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/harness-as-a-service.md"
source_commit: "0426e7f2036ea739db9b2cbdbaaed396066f6d6c"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "エージェントを生の LLM 補完 API の上に直接構築するのではなく、ハーネスのランタイム（ループ、ツール、コンテキスト管理、フック、サンドボックスのプリミティブ）の上に構築するという捉え方（Viv Trivedy によるものとされる）。"
---

Harness-as-a-Service（HaaS）は、Viv Trivedy によるものとされる捉え方であり、エージェントの構築方法の転換を表す。すなわち、補完（completion）を返す LLM API の上に構築することから、ランタイムを返すハーネス API の上に構築することへの転換である。この捉え方のもとでは、ハーネスフレームワークがエージェントループ、ツール呼び出し、コンテキスト管理、フック、サンドボックスのプリミティブを最初から提供し、構築者はループ、ツール呼び出し、会話状態、承認フローをゼロから組み立てるのではなく、システムプロンプト、ツール、コンテキスト、サブエージェントという 4 つの柱に沿ってそれらをカスタマイズする。

## 用法

出典は、この方向を指し示す例として Claude Agent SDK、Codex SDK、OpenAI Agents SDK を挙げている。そしてこの転換こそが、エージェントの設計を反復的に改善することを扱いやすいものにすると位置づける。構築者は、何か問題が起きるたびにエージェントを一から作り直すのではなく、すでによく整理された設定面を調整することになるからである。

## 適用される場面

ハーネスフレームワークがループ、ツール実行、コンテキスト管理の要件をすでにカバーしており、差別化のための作業がドメイン固有のプロンプトとツールの設計に委ねられるような、エージェントベースの新しいプロダクトやワークフローの構築に当てはまる。出典は、それでも不完全な最初のバージョンから始めるべきだという Viv Trivedy の主張――「良いエージェント構築とは反復の営みである。v0.1 がなければ反復はできない」――を引用し、ハーネスが完全に練り上げられるまでこのパターンの採用を遅らせない理由としている。

## 関連用語

[[DefinedTerm/harness-engineering]]
