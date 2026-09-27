---
title: "Kilo Code"
type: "schema:SoftwareApplication"
lang: ja
aliases: ["Kilo"]
tags: [エージェント, コーディングエージェント, コーディングツール, オープンソース, CLI]
translated_from: ".wikicommit/entity/en/SoftwareApplication/kilo-code.md"
source_commit: "5a469d929e172ff921cd501cb6f2c1e9edd4c65b"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "VS Code、JetBrains、ターミナル向けのクライアントが MIT ライセンスのオープンソースとして公開され、Gateway と Cloud のバックエンドコードがソースアベイラブルとして公開されている AI コーディングエージェント。開発元は、ユーザーが多数のモデルから選択できるオールインワンのエージェント型エンジニアリングプラットフォームだと説明している。"
  applicationCategory: "AI コーディングエージェント"
  featureList: "VS Code 拡張機能、JetBrains プラグイン、CLI、Cloud Agents、自前のキーによるモデルアクセス（BYOK）"
  author: "Kilo Code, Inc."
---

Kilo Code は、Kilo Code, Inc. が開発する [[DefinedTerm/ai-coding-agent]] である。そのローカルクライアント、すなわち
VS Code 向け拡張機能、JetBrains IDE 向けプラグイン、コマンドラインインターフェースは MIT ライセンスのオープンソースとして
公開されており、ユーザーはそれらを検査、改変、フォーク、実行できる。同社のオープン性に関するページは、これを自分が使う
コーディングエージェントを検査でき、モデルの選択権を保てる手段として売り込んでいる。同サイトには、Kilo が Anaconda に
買収されたことを告知するバナーが掲示されている。

同社は Kilo Code を、単一の用途に特化したツールではなく、オールインワンのエージェント型エンジニアリングプラットフォームとして
提示しており、同社の言葉を借りれば、ゲートやスロットリングでユーザーの足を引っ張るプロプライエタリなエージェントと対比して
いる。

## 機能

同社のコンポーネントとライセンスの一覧表は、オープンソースであるものと、ソースアベイラブルにとどまるものを区別している。

| コンポーネント | 公開形態 | ライセンス |
| --- | --- | --- |
| VS Code 拡張機能 | オープンソース | MIT |
| JetBrains プラグイン | オープンソース | MIT |
| Kilo CLI | オープンソース | MIT |
| Gateway と Cloud のバックエンド | ソースアベイラブル | リポジトリのライセンス |

Gateway と Cloud のバックエンドコードは検査のために公開されているが、セキュリティおよび不正利用対策のコードはそこから
除外されている。同ページは、「オープン」とは特定のコードとライセンスを指すものであり、ホストされるすべてのサービスを
区別のない 1 つのパッケージとして指すものではないと述べている。

プラットフォームとして、Kilo Code は architect、code、debug、review の各エージェントによって、アプリケーションを
切り替えることなく Architect → Code → Debug → Review の流れをカバーすると説明されている。同じセッションとコンテキストが
VS Code、JetBrains、CLI、Cloud Agents の間で引き継がれるとされ、作業をスマートフォンで始め、ノートパソコンで続け、
夜間はクラウドエージェントに引き渡すといったことができる。自前のキーの持ち込み（BYOK）に対応しており、同社は、あらゆる
プロバイダーの 500 以上のモデルへのアクセスを提供し、いつでも切り替えられるとしている。

## 採用状況とエコシステム

同社は一連の公約を掲げている。現在オープンソースである機能はオープンソースのままとする、自前のキーの持ち込みを常に
サポートする、オープンソースのコードベースへのコミュニティの貢献はオープンソースのままとする、ロードマップを公開する、
ドキュメント・ダウンロード・機能はアカウントなしで閲覧できる、というものである。また、同社は Kilo を Kilo で構築している
とも述べており、Kilo Autocomplete、Parallel Agents、Kilo Sessions、Cloud Agents、Code Review、Voice Prompting、
Team AI Dashboard を、Kilo Code 自体を使って 6 週間のうちに出荷した機能として挙げ、さらに Kilo Deploy は最初のコミット
から一般提供まで 2 週間で到達したとしている。同社はこのペースを「Kilo Speed」と呼んでいる。このプロジェクトは GitHub を
通じて貢献を受け付けており、Discord コミュニティもある。
