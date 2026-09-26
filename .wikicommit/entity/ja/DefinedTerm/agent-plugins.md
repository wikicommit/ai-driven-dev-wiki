---
title: "Agent Plugins"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェントツーリング, エージェントスキル, MCP]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-plugins.md"
source_commit: "83a69e2424e621789facae2288c4aa54d75ba9ed"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "エージェントスキルと MCP サーバーを、異なるエージェントクライアントが読み込める 1 つのポータブルなプラグインディレクトリにまとめてパッケージングするための、オープンでベンダー中立な仕様。"
---

Agent Plugins は、[[DefinedTerm/agent-skills]] と [[DefinedTerm/model-context-protocol]] サーバーをポータブルなプラグインへとパッケージングするための、オープンでベンダー中立な仕様である。プラグインは決まったレイアウトを持つディレクトリであり、プラグインの名前を示す最小限の `plugin.json` マニフェスト、`skills/` 配下のスキル、`mcp.json` で宣言される MCP サーバーから成り、これに加えて、単一のクライアントが独自の追加要素のために所有する、逆ドメイン名形式の任意のディレクトリを持てる。バージョン 1.0.0 は Amazon、Cursor、Microsoft、OpenAI、Vercel のコアメンテナーから成る技術運営委員会によって公開され、[[Organization/google]] は 2026 年 8 月に Core Maintainer として参加することを発表した。

## 用法

Google の発表（[[BlogPosting/agent-plugins-package-your-skills-tools-and-more]]）によれば、このフォーマットが扱う問題は構成要素そのものではなく、それらを運ぶ箱のほうにある。スキルと MCP サーバーはそれぞれすでにポータブルだった一方で、クライアントごとに独自のディレクトリレイアウト、マニフェストのメタデータ、MCP 設定の形が考案されており、作者はクライアントごとにパッケージをフォークせざるを得なかった。この仕様は、どこでも同じになる部分を固定し、それ以外には余地を残す。マニフェストは構成要素の場所を移したり、インラインで宣言したりすることはできない。`mcp.json` の各エントリはトランスポート（stdio、Streamable HTTP、またはレガシーの HTTP+SSE）を明示するので、クライアントが設定オブジェクトの形からトランスポートを推測することはない。また構成要素は互いに独立して失敗するため、起動しないサーバーはスキップされて報告される一方で、プラグインのスキルは引き続き読み込まれる。フック、エージェント、コマンドといったクライアント固有の機能は、そのクライアント自身の名前空間ディレクトリに置かれ、他のクライアントはそれを無視する。

バージョン 1 は意図的にパッケージフォーマットにとどめられている。インストールの仕組み、配布プロトコル、権限モデル、サンドボックス化の要件、信頼や来歴の検証、ユーザー体験はいずれも定めておらず、それらは各クライアントに委ねられている。Google の投稿はこれを階層化されたエコシステムの中に位置づけている。Agentic Resource Discovery による発見、AI Catalog によるカタログ掲載、Agent Plugins によるパッケージング、MCP と Agent Skills による実行であり、それぞれ単独で採用できる。Google は、このフォーマットをサポートする最初の自社製品として [[SoftwareApplication/agents-cli]] と Data Agent Kit を挙げている。

## 適用される場面

発表によれば、プラグインが使う価値を持つのは、複数の構成要素がひとまとまりであり、一緒に運ばれる必要がある場合に限られる。単一の MCP サーバーを単一のクライアントへ届けるだけなら、`mcp.json` 単体のほうが依然として簡単であり、単一のスキルにプラグインは必要ない。ここに述べたことはすべて、参加したばかりの仕様についての一ベンダーの発表に基づくものであり、述べられているのは設計と意図であって、測定された採用状況や相互運用性ではない。

## 関連用語

- [[DefinedTerm/agent-skills]]
- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/agent-hooks]]
