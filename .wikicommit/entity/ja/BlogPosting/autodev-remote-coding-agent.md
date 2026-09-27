---
title: "AutoDev Remote 编程智能体：你何必只让 AI 在白天分析需求、设计方案"
type: "schema:BlogPosting"
lang: ja
tags: [コーディングエージェント, エージェントツーリング, サンドボックス化, MCP, オープンソース]
translated_from: ".wikicommit/entity/en/BlogPosting/autodev-remote-coding-agent.md"
source_commit: "19bc48f9255734f269436c88f52086be2c4420a5"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Phodal Huang による 2025 年 6 月の中国語のブログ記事。AutoDev Workbench のオープンソースの一部で、GitHub Actions 上または MCP サービスとして動作し、イシューの分析、タスクの計画、コードの記述を行う AutoDev Remote Agent を紹介するとともに、著者が IDE の構築ではなくリモートエージェントを選んだ理由を説明している。"
  author: ["Phodal Huang"]
  datePublished: "2025-06-13"
---

Phodal Huang が中国語で書いたこの記事は、AutoDev Workbench の一部であり、[[SoftwareApplication/unit-mesh-auto-dev]] の次の段階を構成する要素の 1 つである AutoDev Remote Agent が試用段階に入ったことを告知している。記事はその用途として、サーバー上で MCP サービスとして動作すること、GitHub のイシューの分析とタスクの計画を支援すること、開発プロセスに組み込まれること、そしてコードの記述、アーキテクチャの設計、テストケースの記述を挙げており、自動化されたコーディング、テスト、デプロイ（GitHub Pages に限る）を将来の目標としている。コードは GitHub の `unit-mesh/autodev-workbench` リポジトリで公開されており、読者はそこにイシューを立てて試すよう呼びかけられている。

タイトルの問い、すなわち AI に要求の分析や解決策の設計をなぜ昼間だけさせるのかという問いは、リモートエージェントを、バックグラウンドで開発タスクを完了させるアシスタントとして位置づけている。著者によれば、これは [[SoftwareApplication/claude-code]] や Codex エージェントといったツールも追求している方向である。

## 要点

- 著者は、AutoDev が独自の IDE を構築しない理由を説明している。以前に IntelliJ Community 上で IDE を構築した経験から、独立した IDE のマシンやクラウドサーバーのコストは個人では負担できないと結論づけたこと、また VS Code の構文解析とリファクタリングの能力は受け入れられなかったことを挙げている。
- 彼は 2024 年の主流の AI コーディングを、RPC／Go と Rust によるエージェントのバックエンド、クロスプラットフォーム IDE 向けの WebView フロントエンド、ベクトルベースのコードのインデックス作成と検索という構成として特徴づけている。そして 2025 年には、Grep／Ripgrep による検索がベクトル化に代わる好ましい手段となり（彼はベクトル化はもはや重要ではないと述べる）、Claude のようなコーディングモデルがエージェント的にコーディングできるようになったことで、エージェントはサーバー上で動作してコードの記述、テスト、デプロイを行えると論じている。
- それまでの 1 か月余りで構築されたプロトタイプは、GitHub プロジェクトの Actions の中で使ってイシューの分析、タスクの計画、コードの記述を行うことができ、記事はそれを GitHub Marketplace のアクションにリンクしている。
- 著者によれば、エージェントの設計の最初のバージョンは Augment の助けを借りて作られた。彼は Augment をこれまでで最も強力な AI コーディングアシスタントと呼んでいる。この設計は、AutoDev の VS Code 版からリファクタリングで切り出したコアと、AutoDev Workbench のアシスタント設計を土台としている。
- エージェントのツール設計は AutoDev Sketch のものを踏襲しており、MCP でラップした汎用ツールの上に GitHub ツールを加えることで、イシューを取得し、分析と計画の結果をイシューに書き戻せるようにしている。実行例では、DeepSeek をモデルプロバイダーとして 18 個のツールが読み込まれている。
- 著者が設計の過程で Augment が生み出したと言う「Round」の仕組みは、無限ループを避けるために会話のラウンド数を制限するもので、各ラウンドでツール呼び出しとその要約を行い、最終的に完全なタスク計画に至る。
- 記事は、このエージェントのツールを Claude Code、Augment、Cursor Agent、Codex Agent のツールと、ファイル操作、ターミナル実行、プロセス管理、コード検索、コード解析、GitHub 連携、ネットワーク機能、Jupyter サポート、メモリ管理、可視化の各項目にわたって比較している。その比較で GitHub 連携を備えているとされているのは AutoDev Remote Agent だけである。著者は、ツールにはまだ多くのバグがあると認めている。
- GitHub Actions で実行する際の安全性について、著者は、GitHub Action の中に完全なコード実行環境を作ることと、新しい GitHub Actions を動的に作成することによるサンドボックス化を説明している。Docker は、彼の古い MacBook では性能が悪かったため、ひとまず見送ったという。
- 記事で挙げられている次の段階の目標は、AutoDev Remote Agent が自らをブートストラップできるようにすることと、プロセス関連のツールを追加することである。

## 背景

この記事は著者自身のオープンソースプロジェクトの告知であり、そのツール比較は独立した評価ではなく著者自身が作成した表である。
