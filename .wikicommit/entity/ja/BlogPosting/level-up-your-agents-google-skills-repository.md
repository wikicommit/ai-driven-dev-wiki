---
title: "エージェントをレベルアップする：Google 公式 Skills リポジトリの発表"
type: "schema:BlogPosting"
lang: ja
tags: [エージェントスキル, コンテキストエンジニアリング, Google Cloud]
review_status: pending
translated_from: ".wikicommit/entity/en/BlogPosting/level-up-your-agents-google-skills-repository.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "Google Cloud Next 2026 における Google 公式の Agent Skills リポジトリの発表。Google Cloud 製品、Well-Architected の柱、オンボーディングのレシピを扱う13個のスキルとともに公開された。"
  author: "Megan O'Keefe"
  datePublished: "2026-04-23"
  publisher: "[[Organization/google]]"
---

Google Cloud Next 2026 の初日に公開された本記事は、`github.com/google/skills` にある Google 公式の [[DefinedTerm/agent-skills]] リポジトリを発表するものである。その枠づけとなる問題はグラウンディングである。実践者が Google Cloud 製品を使って構築するためにエージェンティックなツールに向かうなかで、それらの技術についての正確で最新の情報をモデルが持っていることをどう保証するのか、というものだ。

本記事は [[DefinedTerm/model-context-protocol]] を、その一つの答えとして——ただし明示されたコストを伴うものとして——扱う。Google は自社の開発者向けドキュメント用に MCP サーバーを提供しているが、本記事は MCP サーバーを多用すると「コンテキストの肥大化」を招くと論じる。膨大な量のコンテキストがコンテキストウィンドウに読み込まれ、モデルを混乱させ、トークンコストを積み上げてしまうのだ。スキルはその補完として提示される。エージェントに追加の凝縮された専門知識を装備させる方法である。

## 要点

- **本記事によるスキルの定義**は、Agent Skills のサイトから引かれた「エージェントに新しい能力と専門知識を与えるための、シンプルでオープンな形式」というものである。本記事自身の言い換えでは、スキルとは特定の技術やタスクについてのコンパクトでエージェントを第一に据えたドキュメントであり、Markdown で書かれ、リファレンスファイル、コードスニペット、その他のアセットを含めることができる。
- **コンテキスト肥大化への対抗機構として述べられているのは**、オンデマンドの読み込みである。エージェントは必要になったときにのみスキルの情報を読み込む。
- **リポジトリは13個のスキルとともに公開された。** 3つのグループからなる。AlloyDB、BigQuery、Cloud Run、Cloud SQL、Firebase、Gemini API、Google Kubernetes Engine の製品スキル。セキュリティ、信頼性、コスト最適化を扱う3つの Well-Architected の柱のスキル。そして Google Cloud のオンボーディング、認証、ネットワークの可観測性についての「レシピ」スキルである。
- **インストールはエージェント非依存である。** `npx skills install github.com/google/skills` によって任意のエージェントにインストールでき、[[SoftwareApplication/google-antigravity]]、[[SoftwareApplication/gemini-cli]]、およびサードパーティのエージェントが名指しされている。
- 今後数週間から数か月のうちに、さらなるスキルがリポジトリに追加される予定だと述べられている。

## 背景

これは評価ではなくベンダーによる発表である。コンテキストの肥大化についての主張も、スキルがそれを軽減するという主張も、自社製品のローンチに向けた Google 自身の枠づけであり、測定は示されていない。正確に記録されているのは、リポジトリの初期内容とインストール方法であり、いずれも公開日時点のものである。
