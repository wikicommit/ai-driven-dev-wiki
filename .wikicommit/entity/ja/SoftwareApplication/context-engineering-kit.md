---
title: "Context Engineering Kit"
type: "schema:SoftwareApplication"
lang: ja
tags: [コンテキストエンジニアリング, エージェンティックコーディング, 仕様駆動開発, オープンソース]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/context-engineering-kit.md"
source_commit: "1804b4f09d8e8e88510a78cca5839eb041febbe0"
translated_at: "2026-08-20"
translated_by: "claude-opus-5[1m]"

properties:
  description: "Claude Code その他のコーディングエージェント向けに、コンテキストエンジニアリングの技法をまとめたオープンソースのプラグインマーケットプレイス。リフレクション、仕様駆動開発、サブエージェントのオーケストレーション、レビュー、構造化された推論といった粒度の細かいプラグインとして構成されている。"
  applicationCategory: "エージェントプラグインマーケットプレイス"
  author: "NeoLabHQ"
  operatingSystem: ""
  softwareVersion: "3.1.0"
  license: "GPL-3.0"
---

Context Engineering Kit（CEK）は [[DefinedTerm/context-engineering]] の技法とパターンを集めたオープンソースのコレクションであり、Claude Code、OpenCode、Cursor、Antigravity その他のエージェント向けのプラグインマーケットプレイスとして配布されている。掲げられた狙いは、最小限のトークンのフットプリントでエージェントの結果の品質と予測可能性を高めることであり、メンテナたちはこれを自社の開発者が日々使っていたプロンプトに基づくもので、ベンチマークされた論文や他のプロジェクトから派生したプラグインで補ったものだと述べている。

このキットは意図的に粒度が細かい。各プラグインは自分自身のエージェント、コマンド、スキルだけを読み込むため、マーケットプレイスを追加しただけではコンテキストには何も加わらない。そのスキルは agentskills.io の仕様に従い、仕様駆動開発のプラグインは LLM の能力に合わせて調整された arc42 のドキュメント標準の上に構築されている。

## 概要

CEK を組織立てる主張は、信頼性とコストのトレードオフである。README は、変更されるファイル数が増えるにつれて完全に正確な結果が得られる確率を、各アプローチのトークンのオーバーヘッドとともに並べた比較表を提示している。アプローチはワンショットのプロンプト、`/reflect`、`/reflect` と `/memorize`、`/do-and-judge`、`/do-in-steps`、`/plan-task` と `/implement-task`、そこへ `/brainstorm` を加えたもの、さらに人間のレビューを加えたものである。示されるパターンは、ワンショットのプロンプトはスコープとともに急激に劣化し（1〜3ファイルで 60〜80%、20ファイル以上で 1〜20%）、人間のレビューを含む最も重いパイプラインは 5〜35 倍のトークンで 95〜99% を保つ、というものである。これらの数字はメンテナ自身のものであり、公開されたベンチマークではなく、実運用プロジェクトにおける1年以上の実際の開発利用に基づくと記述されている。

インストール方法はホストによって異なる。Claude Code はマーケットプレイスを追加してプラグインを個別にインストールする。Gemini CLI と Antigravity CLI はプラグインごとの選択をサポートしないため、すべてのプラグインのスキルとエージェントを1つの束としてインストールする。`npx skills` や OpenSkills を使えば Cursor、Codex、OpenCode その他へスキルをインストールできるが、README はその経路がサブエージェントを含まないため完全な体験にはならないと指摘している。

## 機能

マーケットプレイスのプラグインには次のものが含まれる。

- **Reflexion**——`/reflect`、`/memorize`、`/critique`、そしてプロンプトの中にその語が現れたとき自動的に `/reflect` を走らせるフック。README はこれらを、自己洗練とリフレクションのループについての公刊研究、およびリフレクション後のメモリ更新に関するエージェント的コンテキストエンジニアリングに根拠づけている。
- **Spec-Driven Development（SDD）**——メンテナが SADD とともに最初に使うことを勧めるプラグイン。3つの主要コマンド（`/add-task`、`/plan-task`、`/implement-task`）が専門特化したエージェントのパイプライン——`researcher`、`code-explorer`、`business-analyst`、`software-architect`、`tech-lead`、`developer`、`code-reviewer`、`tech-writer`——を駆動する。[[DefinedTerm/spec-driven-development]] を参照。
- **Subagent-Driven Development（SADD）**——サブエージェントを起動し、その出力を判定し、作業を並列に、段階的に、あるいは競わせて実行するためのコマンド群。[[DefinedTerm/subagent-driven-development]] を参照。
- **Review**——専門特化したエージェント（`bug-hunter`、`code-quality-reviewer`、`contracts-reviewer`、`historical-context-reviewer`、`security-auditor`、`test-coverage-reviewer`）を用い、影響度と確信度でフィルタするコードおよび PR のレビュー。加えて、大きな変更集合を人間のレビュアー向けに絞り込むトリアージのコマンド。
- **Test-Driven Development**、**Git**、**Domain-Driven Development**、**First Principles Framework（FPF）**、**Kaizen**、**Customaize Agent**、**Docs**、**Tech Stack**、**MCP**——テストのワークフロー、コミットと PR の作成、コード品質のルール、構造化された推論、根本原因の分析、コマンドとスキルの作成、ドキュメント、言語固有のルール、MCP サーバのセットアップを扱う。

メンテナが仕様駆動開発プラグインに実装されていると述べるパターンには、構造化された推論のテンプレート（chain of thought、tree of thoughts、問題の分解、自己批評）、コンテキストロットを防ぐためのコンテキスト隔離に向けたマルチエージェントのオーケストレーション、[[DefinedTerm/llm-as-judge]] に基づく品質ゲート、タスク固有のスキルを構築する継続的な学習、そしてクリーンな状態でのエージェント起動とファイルシステムベースのメモリを用いる信頼性パターン MAKER がある。

## 沿革

README のニュースの節は直近のリリースの流れを記録している。v2.0.0 は SDD プラグインをゼロから書き直した。v2.1.0 と v3.1.0 はコード品質の指針と専用の code-reviewer エージェントを段階的にそこへ取り込んだ。v2.2.0 は SADD を、メタ判定と判定のサブエージェントを用いた SDD の蒸留版として作り直した。そして v3.0.0 は AMP と Hermes のエージェントのサポートを追加した。リポジトリは GPL-3.0 でライセンスされ、取得時点で 1.3k のスター、138 のフォーク、395 のコミットを示していた。

[[DefinedTerm/vibe-coding]] との関係について、メンテナたちは SDD はバイブコーディングの解ではないが、そのままではバイブコーディングのように振る舞うと述べている。デフォルトでは1つのプロンプトからタスクの終わりまで走り、繰り返し確認を求めるのではなく証拠に基づく前提を置く。開発者の時間の方がモデルの時間より価値が高い、という理屈である。彼らの留保は、人間のフィードバックがなければ品質は最適に達しないということ、そして作業をより小さなタスクへ分解し、各仕様を独立にレビューすることを強く勧める、というものである。
