---
title: "Magentic-UI"
type: "schema:SoftwareApplication"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/magentic-ui.md"
source_commit: "fed0100a95b9cbca3a6a11c43d68e28bc873bdea"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "人間とエージェントのインタラクションを開発・研究するための、Microsoft Research によるオープンソースのヒューマン・イン・ザ・ループ Web インターフェース。Web の閲覧、コードの実行、ファイルの操作ができる拡張可能なマルチエージェントシステムの上に構築されており、Model Context Protocol（MCP）のツールで拡張できる。"
  applicationCategory: "ヒューマン・イン・ザ・ループのエージェント型システム"
  author: "Microsoft Research AI Frontiers"
  featureList: "共同計画、共同タスク実行、アクションの承認、回答の検証、長期メモリ、マルチタスク"
---

Magentic-UI は、Microsoft Research AI Frontiers が [[ScholarlyArticle/magentic-ui]] で発表した、ヒューマン・イン・ザ・ループのエージェント型システムを開発・研究するための、エンドユーザー向けのオープンソース Web インターフェースである。Magentic-One を改変した拡張可能なマルチエージェントシステムによって駆動されており、このシステムは Web を閲覧してその上で操作を行い、コードを生成・実行し、ファイルを生成・分析できる。また、1 つ以上の MCP サーバーをラップするカスタムエージェントを通じて、Model Context Protocol（MCP）のツールで拡張することもできる。そのアーキテクチャは、AutoGen を用いて実装された主導役の Orchestrator エージェントが、WebSurfer、Coder、FileSurfer などのサブエージェント群に指示してアクションを実行させるという構成であり、人間のユーザーはマルチエージェントチーム内の特別なロールを持つエージェントとして扱われる。

## 機能

Magentic-UI は、人間が低コストで関与するための 6 つのインタラクション機構を提供する。共同計画（実行開始前にアクションの計画について協働する）、共同タスク実行（タスクの途中で制御をシームレスに引き継いだり戻したりする）、アクションの承認（影響の大きいアクションにユーザーの承認を必須とする）、回答の検証（タスクが正しく完了したかどうかをユーザーが確かめるのを支援する）、メモリ（過去のタスクのワークフローを保存・再利用して将来の性能を向上させる）、そしてマルチタスク（ループに関与し続けながら複数のセッションを並行して実行する）である。Orchestrator には 2 つの動作モードがある。ユーザーと協働して計画を作成する計画モードと、実行モードである。また、タスクが曖昧であったり指定が不十分であったりする場合には、計画を生成する前にユーザーに確認の質問を行う。

安全性のために、Magentic-UI は各エージェントコンポーネントを個別のサンドボックス化された Docker コンテナで実行し、認証情報やセッション Cookie が共有されないようにユーザーのブラウザとは別の独自のブラウザを使用する。また、許可された Web サイトのリストをサポートしており、そのリストにないサイトへのアクセスにはユーザーの明示的な承認が必要となる。その際 Magentic-UI は、アクセス先の正確な URL、ページタイトル、アクセスの理由を提示する。

## 採用とエコシステム

Magentic-UI はオープンソースであり、github.com/microsoft/magentic-ui でホストされている。Microsoft が以前に開発したマルチエージェントシステムである Magentic-One のアーキテクチャの上に構築されている。AI エージェントに対するヒューマン・イン・ザ・ループの監督に関する未解決の問いを研究者が研究するのを支援するための研究プロトタイプとして位置づけられており、そのシミュレートされたユーザーによる評価手法は、τ-bench や Co-Gym などの先行研究に基づいている。
