---
title: "重要なお知らせ：Gemini CLI から Antigravity CLI への移行"
type: "schema:BlogPosting"
lang: ja
tags: [エージェント, コーディングツール, CLI]
translated_from: .wikicommit/entity/en/BlogPosting/transitioning-gemini-cli-to-antigravity-cli.md
source_commit: "9b65710f8033cfb0f6c3388db1436c4e823817a3"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Google がターミナル向けコーディングエージェントを Google Antigravity に統合するという発表。Antigravity CLI が一般提供となり、Gemini CLI の個人ユーザーはそちらに移行する一方、エンタープライズライセンスでの Gemini CLI の利用は継続される。"
  author: ["Dmitry Lyalin", "Taylor Mullen"]
  datePublished: "2026-05-19"
  publisher: "[[Organization/google]]"
---

この記事は、Google がターミナルエージェントの取り組みを、同社が最上位のエージェントファースト開発プラットフォームと呼ぶ [[SoftwareApplication/google-antigravity]] に統合することを発表している。[[SoftwareApplication/antigravity-cli]] は記事の公開日にすべての人が利用可能となり、[[SoftwareApplication/gemini-cli]] の個人ユーザーはそちらに移行することになる。記事は詳細について Google の I/O 2026 のアップデートを参照するよう読者に案内している。

挙げられている理由は、開発者の働き方の変化である。記事によれば、Gemini CLI はターミナルがエージェント型タスクの強力なインターフェースになりうることを証明したが、今やユーザーは複雑な作業を分担するために互いに通信する複数のエージェントを必要としており、そのためにはターミナルツールがワークフローの他の部分と 1 つのバックエンドを共有する必要がある。Google の対応は、2 つの製品を維持するのではなく、同社が「今日のマルチエージェントの現実」と呼ぶものに向けて作られた単一の製品に集中することである。

## 要点

- Gemini CLI は前年のリリース以来、数百万人のユーザーコミュニティ、10 万を超える GitHub スター、6,000 件のマージ済みプルリクエスト、数百人のコントリビューターへと成長したと説明されている。これらは Google 自身の数字である。
- Antigravity CLI はローンチ時点では Gemini CLI と 1 対 1 の機能同等性を持たないが、記事が最も重要な機能と呼ぶものは維持する。すなわち Agent Skills、フック、サブエージェント、そして Antigravity プラグインとなる拡張機能である。
- 3 つの改善点が主張されている。CLI が Go で構築されていることによる実行の高速化、ターミナルセッションをロックせずに複数のエージェントがバックグラウンドで動作する非同期ワークフロー、そして Antigravity 2.0 デスクトップアプリケーションとのエージェントハーネスの共有により、コアエージェントの改善がすべての利用面に届くことである。
- 2026 年 6 月 18 日に、Gemini CLI と Gemini Code Assist の IDE 拡張機能は、Google AI Pro および Ultra の契約者と、個人向け Gemini Code Assist の無料ユーザーからのリクエストの処理を停止する。Gemini Code Assist for GitHub は同日から GitHub Organization への新規インストールの受け付けを停止し、その後数週間のうちにリクエストの処理も終了する。
- エンタープライズ向けのアクセスは変わらない。Gemini Code Assist Standard または Enterprise ライセンスのもとで Gemini CLI や IDE 拡張機能を使っている組織、あるいは Google Cloud 経由で Gemini Code Assist for GitHub を使っている組織は引き続き利用でき、Gemini CLI は有料の Gemini および Gemini Enterprise Agent Platform の API キーを通じて引き続き利用可能である。
- 移行は技術ドキュメントによって支援され、動画によるウォークスルーも予定されている。フィードバックは Antigravity CLI のコミュニティフォーラムで受け付けている。

## 背景

この記事はベンダー自身による製品発表であるため、変更の理由やユーザーが得るものについての説明は、外部の評価ではなく Google による位置づけである。記事が発表しているのは製品の統合であって、全員に対する提供終了ではない。Gemini CLI はエンタープライズ顧客向けに継続され、変わるのは個人ユーザーが Google の 2 つのターミナルエージェントのどちらで提供を受けるかである。
