---
title: "addyosmani/agent-skills"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェントスキル, エンジニアリング実践, エージェンティックコーディング, オープンソース]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/addyosmani-agent-skills.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "開発ライフサイクル全体にわたるシニアエンジニアリングのワークフロー、品質ゲート、検証要件を符号化したオープンソースのエージェントスキル24点のパック。スラッシュコマンド、専門家ペルソナ、そして十数種のエージェントハーネス向けのセットアップ経路を備える。"
  applicationCategory: "DeveloperApplication"
  author: "[[Person/addy-osmani]]"
  operatingSystem: ""
  softwareVersion: ""
  license: "MIT"
---

`addyosmani/agent-skills` は [[DefinedTerm/agent-skills]] のオープンソースのリポジトリであり、自らを「AI コーディングエージェントのためのプロダクション水準のエンジニアリングスキル」と記述している。掲げられた目的は、シニアエンジニアが用いるワークフロー、品質ゲート、ベストプラクティスを符号化し、エージェントが開発のあらゆる段階でそれらに一貫して従うようパッケージ化することである。問題についての診断は率直である。AI コーディングエージェントは既定で最短経路を取り、それはしばしば仕様、テスト、セキュリティレビュー、そしてソフトウェアを信頼できるものにする実践を飛ばすことを意味する。

## 概要

このパックは6段階のライフサイクル——Define、Plan、Build、Verify、Review、Ship——を軸に構成され、8つのスラッシュコマンドがそこへ対応づけられる。`/spec`（「コードの前に仕様を」）、`/plan`（「小さく原子的なタスクに」）、`/build`（「一度に1スライス」）、`/test`（「テストは証拠である」）、`/review`（「コードの健全性を高める」）、`/webperf`（「最適化の前に測れ」）、`/code-simplify`（「賢さより明快さ」）、そして `/ship`（「速いほうが安全」）である。スキルはエージェントが何をしているかからも自動的に起動する——API を設計していれば API 設計のスキルが、UI を構築していればフロントエンドのスキルが起動する。

`/build auto` モードが取り除くのは検証ではなく、タスク*と*タスクの*あいだ*の人間のステップである。計画は一度承認され、その後は生成と実装が一度の走行で行われる。各タスクは依然としてテスト駆動であり個別にコミットされ、失敗や危険なステップでは実行が一時停止する。

## 機能

リポジトリには24のスキル——23のライフサイクルスキルに、パックの使い方についてのメタスキル1つ——に加えて、4つの専門家エージェントのペルソナ（Senior Staff Engineer 水準のコードレビュアー、テストエンジニア、セキュリティ監査者、Web パフォーマンス監査者）、7つの補足のリファレンスチェックリスト、セッションのライフサイクルフック、そしてツールごとのセットアップ文書が含まれる。

スキルそのものについて、4つの設計上の選択が述べられている。**散文ではなくプロセス**——スキルはリファレンス文書ではなく、ステップ、チェックポイント、終了基準を備えたワークフローである。**合理化への対抗**——すべてのスキルは、エージェントがステップを飛ばすために使う言い訳の表を——挙げられている例は「テストは後で追加します」——文書化された反論とともに携える。**検証は交渉の余地がない**——すべてのスキルは、テストの成功、ビルドの出力、実行時のデータといった証拠の要件で終わり、「『合っていそう』では決して十分でない」。**[[DefinedTerm/progressive-disclosure]]**——`SKILL.md` が入口であり、補助のリファレンスは必要なときにのみ読み込まれ、トークンの使用量を最小限に保つ。

インストールは意図的にハーネス非依存である。リポジトリは、オープンな skills CLI 経由の `npx skills add addyosmani/agent-skills` を文書化しており、これが70を超えるエージェントへインストールされると述べる。あわせて、[[SoftwareApplication/claude-code]] のプラグインマーケットプレイス経由のインストール、[[SoftwareApplication/cursor]]、Antigravity CLI、[[SoftwareApplication/gemini-cli]]、Windsurf、OpenCode、[[SoftwareApplication/github-copilot]]、[[SoftwareApplication/kiro]]、[[SoftwareApplication/codex]]、Command Code 向けのネイティブな経路も示されている。文書化されている移植性の欠落が1つある。スキル単位の `npx` インストールはそのスキルのディレクトリだけを複写し、リポジトリレベルの `references/` ディレクトリは複写しないため、リポジトリ全体を統合しない限り共有のチェックリストは利用できない。

## 沿革

リポジトリ自身の枠づけは、その内容の系譜を Google のエンジニアリング文化に置いている。スキルには『Software Engineering at Google』と Google のエンジニアリング実践ガイドの概念が織り込まれていると述べ、API 設計における Hyrum の法則、テストにおける Beyoncé ルールとテストピラミッド、コードレビューにおける変更の大きさとレビュー速度の規範、単純化における Chesterton の柵、git ワークフローにおけるトランクベース開発、CI/CD におけるフィーチャーフラグを伴う Shift Left を挙げている。このスナップショットの時点でリポジトリは 88.8k のスター、9.5k のフォーク、437 のコミットを示しており、MIT ライセンスである。他の2つのスキルパックに対して自らを位置づける比較文書へのリンクも張られている。
