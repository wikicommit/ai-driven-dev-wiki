---
title: "Symphony"
type: "schema:SoftwareApplication"
lang: ja
tags: [オーケストレーション, マルチエージェント, Issue トラッキング, エージェンティックコーディング]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/symphony.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "エージェントではなく、なされるべき作業を管理するという原則の上に構築された OpenAI の実験的なオーケストレータ。カンバンボードを Todo のチケットについてポーリングし、隔離されたワークスペースでの実装を経てそれらを動かし、人間のレビューへ引き渡す。"
  applicationCategory: "DeveloperApplication"
  author: "[[Organization/openai]]"
  operatingSystem: ""
  softwareVersion: ""
  license: ""
---

Symphony は OpenAI の実験的なオーケストレータであり、エンジニアリングプレビューと銘打たれている。[[BlogPosting/survey-of-development-workflows-in-the-coding-agent-era]] が報告するその構成上の概念は、「エージェントではなく、なされるべき作業（Issue）を管理する」ことである。オーケストレーションの抽象度を、エージェントを指揮することから、Issue トラッカーを通じてタスクを管理することへと引き上げる。

## 概要

Linear のようなカンバンボードを継続的にポーリングし、Todo にあるチケットを検出し、自律的にそれらを In Progress へ移し、検証の完了時に Human Review へ移す。サーベイはこれを、この分野を巡る紹介のなかで最も抽象度の高いオーケストレーションとして提示し、著者自身のアイデア駆動のワークフローがこれに似ていると注記している。

## 機能

4つの能力が挙げられている。物理的なワークスペースの隔離——タスクごとに独立したワークスペースが生成され、そこへ [[SoftwareApplication/codex]] が配備される。`WORKFLOW.md` ファイルを通じた policy-as-code。Elixir の上に構築された OTP ベースの自己修復とリトライ。そして複数の SSH ワーカーにまたがるリモートの分散実行である。

## 沿革

サーベイはこれが依然として実験的なプロトタイプであることを明示している。Symphony が既定では強力なガードレールなしに動作することを記録し、採用の絶対的な前提条件として、ハーネスエンジニアリング——決定的なテスト、リンタ、CI に基づく自動検証——がコードベースにすでに適切に備わっていることを挙げている。
