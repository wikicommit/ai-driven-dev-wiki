---
title: "Agents CLI"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, エージェントツーリング, デプロイ]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/agents-cli.md"
source_commit: "9b65710f8033cfb0f6c3388db1436c4e823817a3"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Google Cloud 上のエージェント開発ライフサイクルのためのコマンドラインツール。人間が入力するだけでなく、AI コーディングアシスタントが操作することを前提に作られている。スキャフォールディング、評価、インフラストラクチャのプロビジョニング、デプロイ、公開を 1 つのインターフェースでカバーする。"
  applicationCategory: "エージェント開発 CLI"
  featureList: "デプロイ先を指定したプロジェクトのスキャフォールディング、コーディング環境に注入される同梱スキル、正解データセットに対する評価の実行と実行間の比較、インフラストラクチャのプロビジョニング、Agent Runtime・Cloud Run・GKE へのデプロイ、Gemini Enterprise への公開、エージェント駆動モードと人間駆動モード"
  author: "[[Organization/google]]"
---

Agents CLI は、Google Cloud 上のエージェント開発ライフサイクルをカバーするコマンドラインツールであり、Agent Platform、Cloud Run、エージェント間連携にまたがる単一のプログラマティックなインターフェースとして提示されている。従来の CLI と異なるのは、想定される操作者である。このツールは AI コーディングエージェント向けに特化して設計されたと説明されており、その例として Gemini CLI、Claude Code、Cursor が挙げられている。その目的は、こうしたアシスタントがドキュメントから各要素の組み合わせ方を推測するに任せるのではなく、クラウドスタックへの直接的で機械可読な経路を与えることだとされている。

この設計の理由として挙げられているのは、コンテキストのコストである。コーディングアシスタントがばらばらのクラウドコンポーネントをどう組み合わせるかを推測しなければならない場合、その結果は終わりのないループとトークンの浪費になると説明されている。このツールの答えは、1 つのセットアップコマンドで同梱スキルをコーディング環境に注入し、標準に準拠したプロジェクトを直接スキャフォールディングするのに必要な API リファレンスを供給することである。

## 機能

- `uvx google-agents-cli setup` でインストールとセットアップを行い、このコマンドが同梱スキルをコーディング環境に注入する。
- 選択したデプロイ先を指定してプロジェクトをスキャフォールディングする。無人での利用向けに自動のデフォルト設定も用意されている。
- 正解データセットに対して評価ハーネスを実行し、2 回の実行間で軌跡のスコアリングとメトリクスを比較する。
- 本番インフラストラクチャをプロビジョニングし、Infrastructure as Code を注入して CI/CD パイプラインを構築する。
- Agent Runtime、Cloud Run、GKE のいずれかにデプロイし、デプロイしたエージェントを配布のために Gemini Enterprise に登録する。
- 同じコマンド群の上に 2 つのモードを提供する。コーディングアシスタントによる利用に最適化された Agent Mode と、開発者がターミナルやスクリプトでコマンドを直接実行し、決定論的に実行するための Human Mode である。

## 採用とエコシステム

2026 年 8 月、Google は Agents CLI を、スキルと MCP サーバーをパッケージ化するためのベンダー中立なフォーマットである [[DefinedTerm/agent-plugins]] をサポートする最初の 2 製品の 1 つに挙げた（[[BlogPosting/agent-plugins-package-your-skills-tools-and-more]]）。この発表では、Agents CLI はエージェントの構築、評価、デプロイ、オブザーバビリティ、公開に関する Google のエキスパートスキルをパッケージ化し、あらゆる AI コーディングエージェント — Antigravity、Gemini CLI、Claude Code、Cursor が挙げられている — をエージェント構築とエージェント運用のエキスパートに変えるものと説明されている。これらのスキルはもともと配布可能であったが、今や Google だけのものではないフォーマットで配布可能になったということである。

このツールは [[SoftwareApplication/gemini-enterprise-agent-platform]] のスタックを置き換えるのではなくその上に位置し、公開ステップでは Gemini Enterprise を配布先とする。AI コーディングエージェントが操作するように設計されており、それらのためのスキルを CLI 自体に同梱して提供する。ここでまとめた内容はツールの開発チーム自身による発表に基づくものであり、ツールの範囲とコマンド体系を示すものではあっても、実際に使ってみた独立した経験を示すものではない。
