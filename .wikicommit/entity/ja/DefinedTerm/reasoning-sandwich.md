---
title: "推論サンドイッチ（Reasoning Sandwich）"
type: "schema:DefinedTerm"
lang: ja
tags: [推論モデル, ハーネスエンジニアリング, エージェント型コーディング]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/reasoning-sandwich.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "エージェントの作業全体にわたって推論モデルの計算量を不均等に配分するヒューリスティックに LangChain が付けた名前。計画と検証には最も高い推論設定を、その間の実装にはそれより低い設定を用いる。"
---

推論サンドイッチとは、LangChain の [[BlogPosting/improving-deep-agents-with-harness-engineering]] で名付けられたヒューリスティックであり、エージェントがタスクの各段階でどれだけの推論計算量を費やすかを決めるためのものである。開始時の計画と終了時の検証により多くを費やし、その間の実装にはより少なく費やす。`low`、`medium`、`high`、`xhigh` の推論モードを備えたモデルに対して LangChain が採った設定は、計画に `xhigh`、実装に `high`、検証に `xhigh` というものだった。

## 用法

この用語は、長時間稼働するコーディングエージェントのためのハーネス設計に由来する。そこでは推論モデルが何時間も動き続けることがあり、ハーネスは各サブタスクにどれだけの計算量を割り当てるかを決めなければならない。LangChain の考えでは、推論を増やすことは、エージェントが難しい問題を十分に理解して良い計画を立てるのに役立ち、終盤の検証で解答を提出する前に誤りを見つけるのにも役立つ。しかし同時に、トークンと時間を 2 倍以上消費しうる。Terminal Bench の制限時間のもとでは、タスク全体を `xhigh` で実行するとエージェントがタイムアウトしたためスコアは 53.9% にとどまり、`high` での 63.6% を下回った。同チームは、試行実行では推論予算の配分の仕方による大きな差は見られなかったと報告しており、サンドイッチをベースラインとして維持した。

## 適用される場面

このヒューリスティックは、推論エフォートを呼び出しごとに設定できるモデル（[[DefinedTerm/reasoning-effort]] を参照）と、時間やコストの予算が制約となるタスクを前提としている。LangChain の環境であらゆる箇所に最大限の推論を費やすことが逆効果になったのは、この予算制約のためである。これは 1 つのチームが自らのベンチマーク実行から得たヒューリスティックであり、確立されたプラクティスではない。同じ投稿は、自然な代替案として適応的推論 — Claude や Gemini のモデルのように、どれだけ推論するかをモデル自身が決める方式 — を挙げている。また、複数のモデルを用いるハーネスでは、同様のバランス調整を、大きなモデルで計画し、実装をより小さなモデルに引き渡すという形で行うこともできると示唆している。

## 関連用語

- [[DefinedTerm/reasoning-effort]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/verification-loop]]
