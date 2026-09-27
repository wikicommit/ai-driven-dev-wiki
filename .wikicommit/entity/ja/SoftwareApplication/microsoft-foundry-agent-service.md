---
title: "Microsoft Foundry Agent Service"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール, ツール利用, エージェントアーキテクチャ]
translated_from: ".wikicommit/entity/en/SoftwareApplication/microsoft-foundry-agent-service.md"
source_commit: "08a4589307f8f63e62aeeda1db83306c45b6c74a"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "AI エージェントを構築・デプロイするための Microsoft のフルマネージドサービス。ツール呼び出しはサーバー側で実行され、会話の状態はマネージドなスレッドに保持されるため、開発者がツール呼び出しを解析したり会話履歴を自分で保存したりする必要がない。"
  applicationCategory: "マネージド AI エージェントサービス"
  featureList: "サーバー側での自動的なツール呼び出し、マネージドな会話スレッド、カスタムツールと組み込みツールを組み合わせるツールセット、ナレッジツール（Bing によるグラウンディング、File Search、Azure AI Search）、アクションツール（関数呼び出し、Code Interpreter、OpenAPI で定義されたツール、Azure Functions）"
  author: "Microsoft"
---

Microsoft Foundry Agent Service は、基盤となるコンピュートやストレージを管理することなく AI エージェントを構築・デプロイ・スケールするためのマネージドサービスである。Microsoft の *AI Agents for Beginners* コースは、これを [[DefinedTerm/tool-use-design-pattern]] を実装するための Microsoft の 2 つの手段のうち新しいほうとして紹介しており、フルマネージドであることとエンタープライズグレードのセキュリティを備えていることを理由に、エンタープライズ向けアプリケーションに位置づけている。

コースは、モデルの API を直接呼び出す場合と比べて 3 つの利点があると述べている。第一に、ツール呼び出しが自動で行われるため、アプリケーションがツール呼び出しを解析し、ツールを起動し、その応答を処理する必要がなく、これらはすべてサーバー側で行われる。第二に、会話の状態は開発者ではなくスレッドによって管理される。第三に、一般的なデータソースにアクセスするための一連のツールが最初から利用できる。

## 機能

ツールは 2 つのカテゴリに分けられる。**ナレッジツール**は情報を取得するもので、Bing Search によるグラウンディング、File Search、Azure AI Search がある。**アクションツール**は何かを実行するもので、関数呼び出し、Code Interpreter、OpenAPI 仕様から定義されたツール、Azure Functions がある。

ツールは**ツールセット**にまとめられ、そこには開発者が提供する関数と組み込みのツールを混在させることができる。ある要求に対してどれを使うかはモデルが判断する。コースの実例では、独自の SQLite クエリ関数と Code Interpreter ツールからツールセットを構築し、モデル、名前、指示、そのツールセットを指定してエージェントを作成する。これにより、モデルは問われた内容に応じて、データを問い合わせるかそのデータに対して計算するかを選ぶ。**スレッド**は特定の会話のメッセージ履歴を保持する。

## 採用状況とエコシステム

コースは、会話型エージェントが組織の売上データを問い合わせ、その結果を分析することで売上に関する質問に答えるという売上データのシナリオを通じて、このサービスを説明している。本サービスは、エージェントフレームワークを自前で運用することに対するマネージドな代替手段として、[[SoftwareApplication/microsoft-agent-framework]] と並んで取り上げられている。
