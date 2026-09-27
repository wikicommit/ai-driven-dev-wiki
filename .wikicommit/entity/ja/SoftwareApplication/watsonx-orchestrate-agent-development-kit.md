---
title: "IBM Watsonx Orchestrate Agent Development Kit"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, ツール利用]
translated_from: ".wikicommit/entity/en/SoftwareApplication/watsonx-orchestrate-agent-development-kit.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "ツールビルダーのペルソナ向けに作られた、IBM Watsonx Orchestrate の中でエージェントとツールを設定・デプロイ・管理するためのコマンドラインユーティリティ群と Python ベースのライブラリ。そのアルファリリースには、[[ScholarlyArticle/testing-rest-apis-as-llm-tools]] で説明されている、REST API を LLM のツールとしてテストするフレームワークが組み込まれている。"
  applicationCategory: "エージェント用ツール開発キット"
  author: "IBM"
---

IBM Watsonx Orchestrate Agent Development Kit（ADK）は、コマンドラインインターフェース（CLI）のユーティリティ群と Python ベースのライブラリからなり、ツールビルダーに、Watsonx Orchestrate の中でエージェントとツールを設定・デプロイ・管理するためのツール環境を提供する。[[ScholarlyArticle/testing-rest-apis-as-llm-tools]] は、ADK のアルファリリースの一部としてデプロイされ、特にツールビルダーのペルソナ向けに設計された REST API テストフレームワークについて説明している。

## 機能

ADK の一部として、[[ScholarlyArticle/testing-rest-apis-as-llm-tools]] のフレームワークは、ツールビルダーがエージェントと組み合わせてツールをテストできるようにする。現時点ではこのサポートは CLI を通じて提供されており、ビルダーはツールのテストケースを生成し、さらにエージェントと組み合わせてツールを評価できる。その後ビルダーは、分類されたエラーレポート（[[ScholarlyArticle/testing-rest-apis-as-llm-tools]] のエラー分類を参照）と、ツールの定義を改善するためのテンプレートベースの推奨事項を受け取る。

## 導入とエコシステム

論文の執筆時点で、ADK のテスト機能を利用するツールビルダーは、IT、人事、財務、調達、営業など、さまざまな領域にわたる 600 を超える API をツールとしてラップしていた。このテスト機能が導入される以前は、ビルダーは手作業でツールを作成し、ツールあたり 5〜6 件のテストケースしかテストしていなかった。論文は、テストの自動生成と推奨事項によってツールあたりの構築工数が約 30%（ツールあたりおよそ 2 日）削減され、これまでに合計で 1,200 人日以上が節約されたと報告している。生成されたテストケースは、更新されたツールが引き続き正しく機能することを確認するための継続的テストや回帰テストにも再利用されている。
