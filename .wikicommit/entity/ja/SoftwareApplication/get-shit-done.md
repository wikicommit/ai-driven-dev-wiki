---
title: "Get Shit Done"
type: "schema:SoftwareApplication"
lang: ja
tags: [コンテキストエンジニアリング, 仕様駆動開発, エージェンティックコーディング, フレームワーク]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/get-shit-done.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "Claude Code とともに使うための、メタプロンプティング、コンテキストエンジニアリング、仕様駆動開発からなる軽量なシステム。それ自身のプラットフォームとしてではなく、エージェントの上に重なるコマンドと規約の層として動作する。"
  applicationCategory: "DeveloperApplication"
  author: ""
  operatingSystem: ""
  softwareVersion: ""
  license: ""
---

Get Shit Done——略して GSD——は、[[SoftwareApplication/claude-code]] とともに使うための、メタプロンプティング、[[DefinedTerm/context-engineering]]、[[DefinedTerm/spec-driven-development]] からなる軽量なシステムとして自らを提示する。自身のプラットフォームを定義するのではなく、エージェントの上に重なるコマンドと規約の層として動作し、モデルへ供給されるコンテキストを構造化すること、そして広い要求を仕様と実行可能なステップへ変えることに焦点を置く。

## 概要

[[ScholarlyArticle/from-prompt-to-process]] の6次元のタクソノミーにおいて、GSD は何よりもコンテキストで重みを持ち、仕様は部分的でしかない。仕様・コンテキスト・役割・実行・検証・移植性にわたって 1, 2, 0, 1, 0, 0 を記録している——12点満点中4点であり、検討された6つのフレームワークのうち最低であり、3つの異なる次元でゼロを記録した唯一のものである。

## 機能

その際立った一手は、コンテキストの組み立てを明示的なエンジニアリングのタスクとして扱うこと——エージェントが動く前に、何を、どの順序で、どういう枠づけのもとで読むべきかを決めること——である。論文はこれを、仕様駆動開発の文献で論じられる接地（grounding）の関心事に近いものと位置づけている。

## 沿革

述べられている限界は結合と揮発性である。GSD は特定のエージェントに強く結合しているため、その移植性は [[SoftwareApplication/spec-kit]] や [[SoftwareApplication/openspec]] のそれより限られており、有効性はチームが採用するプロンプトの規約の品質に依存する。論文はまた、リポジトリが新しい組織への保守の移管を示していることに触れ、これを最近のコミュニティのフレームワークに典型的な揮発性の一例として提示している。
