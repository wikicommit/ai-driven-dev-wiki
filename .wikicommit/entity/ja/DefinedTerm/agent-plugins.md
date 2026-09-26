---
title: "Agent Plugins"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェントツーリング, エージェントスキル, MCP]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-plugins.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Agent Skills と MCP サーバーを、異なるエージェントクライアントが読み込める 1 つのポータブルなプラグインディレクトリにまとめてパッケージングするための、オープンでベンダー中立な仕様。"
---

Agent Plugins は、[[DefinedTerm/agent-skills]] と [[DefinedTerm/model-context-protocol]] のサーバーをポータブルなプラグインとしてパッケージングするための、オープンでベンダー中立な仕様である。プラグインは決まったレイアウトを持つディレクトリであり、プラグイン名を記した最小限の `plugin.json` マニフェスト、`skills/` 配下のスキル、`mcp.json` で宣言される MCP サーバーから成る。さらに、単一のクライアントが独自の追加要素のために所有する逆ドメイン形式のディレクトリを、任意で置くことができる。バージョン 1.0.0 は、Amazon、Cursor、Microsoft、OpenAI、Vercel のコアメンテナーから成る技術運営委員会によって公開され、[[Organization/google]] は 2026 年 8 月に Core Maintainer として参加することを発表した。

## 用法

Google の発表（[[BlogPosting/agent-plugins-package-your-skills-tools-and-more]]）の言い方では、このフォーマットが取り組む問題は構成要素ではなく、それらを出荷する箱のほうにある。スキルと MCP サーバーはそれぞれすでにポータブルだったが、クライアントごとに独自のディレクトリレイアウト、マニフェストのメタデータ、MCP 設定の形式を考案していたため、作者はクライアントごとにパッケージをフォークせざるを得なかった。この仕様は、どこでも同じになる部分を固定し、それ以外の部分には余地を残す。マニフェストは構成要素の場所を変更することも、構成要素をインラインで宣言することもできない。`mcp.json` の各エントリはトランスポート（stdio、Streamable HTTP、または従来の HTTP+SSE）を明示的に記述するので、クライアントが設定オブジェクトの形からトランスポートを推測することはない。また、構成要素はそれぞれ独立して失敗するため、起動しないサーバーはスキップされて報告される一方で、そのプラグインのスキルは引き続き読み込まれる。フック、エージェント、コマンド、その他のクライアント固有の機能は、そのクライアント自身の名前空間ディレクトリに置かれ、他のクライアントはそれを無視する。

バージョン 1 は、意図的にパッケージフォーマットだけにとどめられている。インストールの仕組み、配布プロトコル、パーミッションモデル、サンドボックスの要件、信頼や来歴の検証、ユーザー体験はいずれも定義しておらず、それらは各クライアントに委ねられている。Google の投稿はこれを階層化されたエコシステムの中に位置づけている。Agentic Resource Discovery による発見、AI Catalog によるカタログエントリ、Agent Plugins によるパッケージング、そして MCP と Agent Skills による実行であり、それぞれを単独で採用できる。Google は、このフォーマットをサポートする最初の自社製品として [[SoftwareApplication/agents-cli]] と Data Agent Kit を挙げている。

## 適用される場面

発表によれば、プラグインを使う価値があるのは、複数の構成要素がひとまとまりであり、一緒に持ち運ぶ必要がある場合だけである。単一の MCP サーバーを単一のクライアントに提供するなら、依然として `mcp.json` だけのほうが簡単であり、単一のスキルにプラグインは必要ない。ここで述べた内容はすべて、あるベンダーが参加したばかりの仕様についての、そのベンダー自身の発表に基づいている。そこに示されているのは設計と意図であり、測定された採用状況や相互運用性ではない。

## 関連用語

- [[DefinedTerm/agent-skills]]
- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/agent-hooks]]
