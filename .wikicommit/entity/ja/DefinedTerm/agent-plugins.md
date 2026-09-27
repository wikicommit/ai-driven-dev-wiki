---
title: "Agent Plugins"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェントツーリング, エージェントスキル, MCP]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-plugins.md"
source_commit: "f3cd768971749927e49083efe4fbd9f44cf27fb0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Agent Skills のスキルと MCP サーバーを 1 つの可搬なプラグインディレクトリにまとめてパッケージ化し、異なるエージェントクライアントが読み込めるようにするための、オープンでベンダー中立な仕様。"
---

Agent Plugins は、[[DefinedTerm/agent-skills]] と [[DefinedTerm/model-context-protocol]] サーバーを可搬なプラグインへとパッケージ化するための、オープンでベンダー中立な仕様である。プラグインは決まったレイアウトを持つディレクトリであり、プラグイン名を記した最小限の `plugin.json` マニフェスト、`skills/` 配下のスキル、`mcp.json` で宣言される MCP サーバーから成る。これに加えて、単一のクライアントが独自の追加要素のために所有する、逆ドメイン形式の名前を持つディレクトリを任意で置くことができる。バージョン 1.0.0 は、Amazon、Cursor、Microsoft、OpenAI、Vercel のコアメンテナーから成る技術運営委員会によって公開され、[[Organization/google]] は 2026 年 8 月に Core Maintainer として参加することを発表した。

## 用法

Google の発表（[[BlogPosting/agent-plugins-package-your-skills-tools-and-more]]）によれば、このフォーマットが扱う問題は構成要素そのものではなく、それらを出荷する箱にある。スキルと MCP サーバーはそれぞれすでに可搬だったが、クライアントごとに独自のディレクトリレイアウト、マニフェストのメタデータ、MCP 設定の形を考案していたため、作成者はクライアントごとにパッケージをフォークせざるを得なかった。この仕様は、どこでも同じになる部分を固定し、それ以外には余地を残す。マニフェストは構成要素の配置を変えたり、インラインで宣言したりすることはできない。`mcp.json` の各エントリはトランスポート（stdio、Streamable HTTP、またはレガシーの HTTP+SSE）を明示するため、クライアントが設定オブジェクトの形からトランスポートを推測することはない。また構成要素は独立して失敗するため、起動しないサーバーはスキップされて報告される一方、プラグインのスキルは引き続き読み込まれる。フック、エージェント、コマンド、その他のクライアント固有の機能は、そのクライアント自身の名前空間ディレクトリに置かれ、他のクライアントはそれを無視する。

バージョン 1 は意図的にパッケージフォーマットだけにとどめられている。インストールの仕組み、配布プロトコル、パーミッションモデル、サンドボックス化の要件、信頼や来歴の検証、ユーザー体験はいずれも定義せず、それらは各クライアントに委ねられている。Google の投稿はこれを階層化されたエコシステムの中に位置づけている。すなわち、Agentic Resource Discovery による発見、AI Catalog によるカタログ登録、Agent Plugins によるパッケージ化、MCP と Agent Skills による実行であり、それぞれ単独で採用できる。Google は、このフォーマットをサポートする最初の自社製品として [[SoftwareApplication/agents-cli]] と Data Agent Kit を挙げている。

## 適用される場面

発表によれば、プラグインを使う価値があるのは、複数の構成要素が一体のものであり、一緒に持ち運ぶ必要がある場合に限られる。単一の MCP サーバーを単一のクライアントに提供するだけなら、`mcp.json` 単体のほうが依然として簡単であり、単一のスキルにプラグインは必要ない。ここに記述した内容はすべて、あるベンダーが参加したばかりの仕様について出した発表に基づくものであり、設計と意図を述べたものであって、実際の採用状況や相互運用性が測定されたものではない。

## 関連用語

- [[DefinedTerm/agent-skills]]
- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/agent-hooks]]
