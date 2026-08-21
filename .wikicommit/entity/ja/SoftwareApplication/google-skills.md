---
title: "google/skills"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェントスキル, Google Cloud, エージェンティックコーディング, オープンソース]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/google-skills.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "Google の製品と技術のためのエージェントスキルの公式リポジトリ。ドメインごとに整理され、エージェントハーネスをまたいでインストールでき、スキルと MCP サーバを組み合わせた製品プラグインも同梱する。"
  applicationCategory: "DeveloperApplication"
  author: "[[Organization/google]]"
  operatingSystem: ""
  softwareVersion: ""
  license: "Apache-2.0"
---

`google/skills` は、Google Cloud を含む Google の製品と技術のための [[DefinedTerm/agent-skills]] の公式リポジトリである。README には、このリポジトリが活発に開発中である旨の注記がある。インストールは単一のコマンド `npx skills add google/skills` であり、そこからすべてを入れるのではなく特定のスキルを選ぶこともできる。

## 概要

スキルは製品ラインごとではなくドメインごとにまとめられている。入門の素材は Google Cloud への認証、foundation-builder のレシピ、オンボーディングを扱う。複数製品にまたがる**ソリューション**のスキルはアーキテクチャ全体を扱う——ソリューションアーキテクチャのワークフロー、クラウドプロバイダとデータ種別をまたぐエージェンティックアナリティクス、オープンなデータレイクハウスのシステム、Google Cloud 上でのエージェントの構築とデプロイ、データサイエンスのワークフロー、双方向のマルチモーダルストリーミング、AI ワークロードの GKE 推論への移行、GKE と AlloyDB 上のエンタープライズ検索のための RAG、そして安全な n 層のサーバーレス Web アプリケーションである。さらなるグループは AI/ML（推論、デプロイ、チューニング、プロンプト管理、RAG エンジン管理、モデルレジストリ、アラートとトラブルシューティングのための Agent Platform スキル群、および Gemini API のスキルを含む）、インフラストラクチャ（主に GKE）、可観測性とコスト、Well-Architected Framework の6つの柱、セキュリティとアイデンティティ、Web とアプリのホスティング、広告、そしてアナリティクスを扱う。

## 機能

スキルの他に、リポジトリはエージェントハーネス向けにスキルと MCP サーバを組み合わせた Google 製品の**プラグイン**を同梱しており、3つについてインストール経路が文書化されている。[[SoftwareApplication/claude-code]]（`claude plugin marketplace add google/skills` の後に `claude plugin install <plugin>@google-plugins`）、[[SoftwareApplication/codex]]（`codex plugin marketplace add google/skills` の後にプラグインブラウザからインストール）、そして Antigravity CLI（プラグインのパスを指定した `agy plugin install`）である。

README はまた、Cloud Storage、Agent Development Kit、Android、Dart、Firestore、Flutter、Genkit を扱う、別リポジトリで保守されている Google のスキルコレクションも指し示している。

## 沿革

このリポジトリは Google Cloud Next 2026 で [[BlogPosting/level-up-your-agents-google-skills-repository]] において発表され、そこでは13のスキルからなる立ち上げ時のセットが記述され、以降の数週間から数か月でさらに増やすと約束されていた。上に記述したカタログは、このスナップショットの時点で存在する、かなり大きくなったセットである。そのスナップショットの時点でリポジトリは 18.6k のスター、1.5k のフォーク、265 のコミットを示し、Apache 2.0 ライセンスを掲げ、スキルの Markdown ファイルに対するバグ報告と、新しいスキルを提案する機能要望というかたちでの貢献を歓迎している。
