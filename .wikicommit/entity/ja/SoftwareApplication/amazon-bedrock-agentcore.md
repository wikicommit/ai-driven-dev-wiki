---
title: "Amazon Bedrock AgentCore"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コンテキストウィンドウ, AWS, エージェントランタイム]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/amazon-bedrock-agentcore.md"
source_commit: "cebf43107fcc80ba464fe278c5b12e158d6d81f2"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "エージェントをデプロイ・実行するための AWS のエンタープライズ向けプラットフォーム。Runtime、Identity、Memory、Code Interpreter、Browser、Gateway、Observability というモジュール式サービスの集合として提供され、フレームワーク非依存であるため、どのフレームワークで構築されたエージェントでも利用できる。"
  applicationCategory: "エージェントランタイムプラットフォーム"
  featureList: "Runtime、Identity、Memory（短期と長期の 2 層）、Code Interpreter、Browser、Gateway（セマンティックなツール検索を備えたツールゲートウェイ）、Observability"
  author: "Amazon Web Services"
---

Amazon Bedrock AgentCore は、エージェント型 AI の開発とデプロイのための AWS のエンタープライズグレードのプラットフォームとして紹介されている。[[BlogPosting/agentic-ai-infrastructure-context-engineering]] が示す 3 層のスタックのうち、基盤モデルとエージェントフレームワークの上にあるランタイム層を担う。単一の製品ではなく、Runtime、Identity、Memory、Code Interpreter、Browser、Gateway、Observability というモジュール式サービスの集合である。その利点として挙げられているのは、エンタープライズ級のセキュリティとオープンソースフレームワークとの互換性の両立であり、開発者はどのフレームワークやモデルでも使いながら、その下のインフラストラクチャは AWS に任せることができる。

このうち 2 つのコンポーネントは、[[DefinedTerm/context-engineering]]（コンテキストエンジニアリング）の問題に直接取り組むものであるため、同記事で詳しく扱われている。エージェントがターン間やセッション間で何を持ち越すかを決める Memory と、一度にいくつのツール定義をコンテキストウィンドウに置く必要があるかを決める Gateway である。

## 機能

**Memory** は 2 層アーキテクチャを採用している。短期メモリは現在のセッションを維持するために会話のやり取りを保存し、長期層へのデータ供給源にもなる。記事の例では、コーディングアシスタントエージェントが変数の検査や構文の修正を記録し、情報を繰り返さずに会話を続けられるようにしている。長期メモリは、抽出された知見を 3 つの戦略で保存する。ユーザー嗜好メモリ（snake_case の命名や pandas の好みといった開発者のコーディングスタイル）、セマンティックな事実メモリ（蓄積されたドメイン知識）、要約メモリ（進捗の追跡とコンテキストウィンドウ使用量の削減の両方に役立つセッション要約）である。マルチテナンシーとデータ分離を備えたフルマネージドの SaaS サービスであり、AWS 自身のフレームワークに加えて LangGraph や CrewAI とも統合できる。

**Gateway** は、既存の API、Lambda 関数、サービスを、エージェントが呼び出せる MCP 形式に変換する。記事によれば、これにより数週間分の独自統合作業が不要になる。注目すべき仕組みはセマンティックなツール検索である。すべてのツール定義をコンテキストに読み込むのではなく、手元のタスクに最も関連する定義をゲートウェイが取得する。記事はこれを、トークン使用量を削減すると同時に、大規模なツールカタログでは当てずっぽうの選択を強いられるような場面で選択精度を高めるものとして提示している。さらに、バージョン管理、IAM ベースのアクセス制御、使用状況の監視、コンプライアンス監査を備え、ツール定義・検索結果・呼び出し結果にまたがる多層キャッシュを持つ。

## 採用とエコシステム

記事のアーキテクチャでは、AgentCore Runtime が [[SoftwareApplication/strands-agents]] を動かす実行環境とライフサイクル管理を提供し、AgentCore Gateway がそのエージェントのツールを取りまとめる。Strands Agents はフック機構を通じて AgentCore Memory を統合しており、メモリの取得と保存はエージェント自身のロジックに手を入れることなく宣言的に行われる。

記事は、どのような場面で AgentCore を選ぶべきかについて意図的な対比を示している。AgentCore Memory はエンタープライズでのデプロイや厳格なコンプライアンスが求められる場面により適しているとされ、一方、Strands Agents を通じて統合される Mem0.ai のようなサードパーティのメモリサービスは、迅速なプロトタイピングや柔軟なカスタマイズにより適していると説明されている。

ここに記録した内容はすべて、ベンダーが自社製品について公開した単一の記事に基づく。AgentCore に関して言えば、記事はサービスを説明し、それらを呼び出す Python コードを示しているが、その計測結果は一切報告していない。記事の別の箇所で示されているコストの数値は Bedrock のプロンプトキャッシュに関するものであり、これらのコンポーネントに関するものではない。また、AgentCore の独立した評価も示されていない。
