---
title: "Superpowers"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェントスキル, ワークフロー, TDD, エージェンティックコーディング]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/superpowers.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "仕様駆動開発と TDD を単一の7段階のパイプラインへ符号化し、それをエージェントに強制するスキルフレームワーク兼開発手法。Claude Code のプラグインマーケットプレイスへ採用されている。"
  applicationCategory: "DeveloperApplication"
  author: ""
  operatingSystem: ""
  softwareVersion: ""
  license: ""
---

Superpowers は `obra/superpowers` として配布されるスキルフレームワーク兼開発手法であり、[[BlogPosting/survey-of-development-workflows-in-the-coding-agent-era]] では [[SoftwareApplication/claude-code]] のプラグインマーケットプレイスへ公式に採用されたものとして記述されている。その記述における際立った特徴は、[[DefinedTerm/spec-driven-development]] や TDD といった個別の実践を単一のパイプラインへ符号化し、手法を指針として提供するのではなくエージェントに強制することである。

## 概要

同サーベイはこれを代表的な4つのプロジェクトワークフローの1つとして提示し、その役割を、エージェントが考えずにコードへ飛び込むのを止めるガードレールとして特徴づけている。適合すると述べられているのは、SDD 型のフローの上に TDD、コードレビュー、ブランチ管理を重ねる全周期の自動化を求めるチームや個人である。4者の比較において、それは焦点が「強制される手法」であり、検証が TDD とコードレビューであり、プラグインを要するためツールへの依存度が高いワークフローである。

## 機能

パイプラインは7段階からなる。**ブレインストーミング**は要求を対話的に引き出し、ユーザーが承認するまでコードへ移らない。**git worktree** が隔離された開発ブランチとして自動的に作られ、テストのベースラインが確認される。**計画**は承認された設計を、それぞれ2〜5分のマイクロタスクへ分解し、正確なファイルパス、コードの仕様、検証の基準を明記する。**実行**はタスクごとに新しい [[DefinedTerm/subagents|サブエージェント]] を差し向け、2段階のレビューを伴う。**TDD** は厳格な red-green-refactor のサイクルを強制する。**コードレビュー**は計画に照らして作業を深刻度で分類する。**ブランチの完了**はテストスイートを検証し、マージまたはプルリクエストを提示する。

## 沿革

サーベイの時点で、リポジトリはそのワークフローの節で 82,074 スター、スキルエコシステムの節で 82,111 スターと記録されており、後者では最大級の [[DefinedTerm/agent-skills]] のコレクションの1つとして挙げられている。
