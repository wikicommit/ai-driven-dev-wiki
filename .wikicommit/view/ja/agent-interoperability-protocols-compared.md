---
title: "エージェント相互運用プロトコルの比較"
lang: ja
kind: comparison
review_status: pending
translated_from: ".wikicommit/view/en/agent-interoperability-protocols-compared.md"
source_commit: "3e91660f792347d5c1022d36ed33f7b72e8a5561"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
---

この wiki には、AI エージェントの接続先のどこかを標準化する 9 つのプロトコルのページがある。[[DefinedTerm/model-context-protocol]]（MCP）、[[DefinedTerm/agent2agent-protocol]]（A2A）、[[DefinedTerm/agent-communication-protocol]]（ACP）、[[DefinedTerm/agent-network-protocol]]（ANP）、[[DefinedTerm/agent-client-protocol]]（こちらも ACP と略される）、[[DefinedTerm/universal-commerce-protocol]]（UCP）、[[DefinedTerm/agent-payments-protocol]]（AP2）、[[DefinedTerm/agent-to-user-interface-protocol]]（A2UI）、[[DefinedTerm/agent-user-interaction-protocol]]（AG-UI）である。このページでは、それぞれが何をつなぐか、メッセージをどう運ぶと説明されているか、発見と認可がどう機能するかという観点から、これらを並べて比較する。あわせて、ソースごとのグループ分けの違い、採用状況についてソースが報告していること、そして組み合わせて使われると説明されている箇所も扱う。比較には wiki のページに記録されている内容だけを用いる。新しいプロトコルの多くはそれぞれ単一のソースでしか説明されていないため、ここで述べることはそのソースの説明である。

## それぞれが何をつなぐか

| プロトコル | つなぐもの | 説明されているトランスポートと形式 | 説明されている発見の仕組み |
| --- | --- | --- | --- |
| MCP | エージェントと外部のツールやデータ | JSON-RPC によるクライアント・サーバー型インターフェース。サーバーはツール名、入力スキーマ、説明を公開する | エージェントが接続先のサーバー群にツールのメタデータを問い合わせる。VS Code ではサーバーを `.vscode/mcp.json` に登録する |
| A2A | エージェントと他のエージェント | A2A クライアントと A2A サーバーの間で、Task、Message、Artifact、Part を同期的に、またはストリーミングでやり取りする | `/.well-known/agent-card.json` に置かれる Agent Card、または直接設定、固定 URI、レジストリ |
| ACP（Agent Communication Protocol） | エージェント同士。汎用のメッセージングのため | MIME タイプ付きのマルチパートメッセージを用いる RESTful HTTP。同期・非同期の両方に対応 | オンラインとオフラインの発見。サーベイはこれをロードマップの該当段階と結びつけている |
| ANP | オープンネットワーク上のエージェント | W3C の分散型識別子（DID）と JSON-LD グラフ | オープンネットワークでのエージェント発見 |
| ACP（Agent Client Protocol） | IDE やエディタとコーディングエージェント | 標準入出力上の JSON-RPC 2.0。エージェントは IDE のサブプロセスとして動作する | セッション開始時のケイパビリティネゴシエーション。LSP の初期化ハンドシェイクに似ている |
| UCP | エージェントと販売者のチェックアウトフロー | 強く型付けされたリクエスト・レスポンスのスキーマを、REST、MCP、A2A、Embedded Protocols のいずれの上でも同一に保つ | `/.well-known/ucp` に置かれる販売者プロファイル |
| AP2 | 購入と、それを承認した人物 | 型付きのマンデート（`IntentMandate`、`PaymentMandate`）と `PaymentReceipt` | 説明なし |
| A2UI | エージェントの出力と、描画されるインターフェース | 18 個のコンポーネントプリミティブからなる固定カタログから組み立てる宣言的な JSON。構造とデータは別々に送られる | 説明なし |
| AG-UI | エージェントフレームワークのイベントとフロントエンド | `TEXT_MESSAGE_CONTENT` や `TOOL_CALL_START` のような型付きイベントを流す server-sent events のストリーム | 説明なし |

## ACP と呼ばれる 2 つのプロトコル

この wiki には、ACP という同じ略称を持つ別々のプロトコルが 2 つあり、それぞれつなぐ相手が異なる。

- **Agent Communication Protocol** は、[[ScholarlyArticle/a-survey-of-agent-interoperability-protocols]] が扱う 4 つのプロトコルの 1 つである。エージェント同士が HTTP 上でメッセージをやり取りするためのプロトコルだ。
- **Agent Client Protocol** は [[BlogPosting/acp-protocol-and-multiple-ai-coding-agents]] に由来する。IDE とコーディングエージェントの間に位置し、同記事はこれを Language Server Protocol になぞらえて「AI エージェントのための LSP」（LSP for AI agents）と呼んでいる。

ソースに「ACP」が出てきたときは、それがつなぐ当事者を見れば、どちらを指しているかがわかる。

## ソースによる整理の仕方

いくつかのソースはこれらのプロトコルの一部をグループ分けしているが、その枠組みはそれぞれ異なる。

- **4 段階の採用ロードマップ。** サーベイは MCP、ACP（Agent Communication Protocol）、A2A、ANP を、インタラクションモード、発見の仕組み、通信パターン、セキュリティモデルの観点で比較する。そして、これらを採用の段階として順序づけている。
  1. MCP：ツールへのアクセスのため
  2. ACP：構造化された、セッションを意識したメッセージングのため
  3. A2A：協調的なタスク実行のため
  4. ANP：分散型のエージェントマーケットプレイスのため
- **1 つのエージェントの中の 6 つのレイヤー。** Google の [[BlogPosting/developers-guide-to-ai-agent-protocols]] は、MCP、A2A、UCP、AP2、A2UI、AG-UI を競合ではなくレイヤーとして扱う。その例は [[SoftwareApplication/agent-development-kit]] のエージェントで、1 つのリクエストが 6 つすべてを使う。
  - MCP と A2A が情報を集める。
  - UCP と AP2 が取引を完了させる。
  - A2UI と AG-UI が結果を提示する。

  このガイドは Google 自身のフレームワークのチュートリアルであり、コードサンプルはすべて ADK を使っている。Google のスタッフによる 2 本目の記事 [[BlogPosting/build-better-ai-agents-agent-bake-off]] も、同じ 6 つのプロトコルを現在の全体像として挙げている。同記事は、ツールごとに独自の API ラッパーを書くのではなく、オープンなエージェントプロトコルを採用するよう勧めており、この全体像を使いこなせるかどうかがプロトタイプと本番システムを分けると論じている。
- **2 つのプロトコルからなるスタック。** A2A のページで引用されているハンドブックの章は、業界が「MCP はツールをつなぎ、A2A はエージェントをつなぐ」（MCP connects tools, A2A connects agents）という形に落ち着きつつあると述べる。同章によれば、この 2 つが合わさってマルチエージェントシステムのプロトコル基盤をなす。[[BlogPosting/new-sdlc-vibe-coding]] は、同じ役割分担を例で示している。Google の Agents CLI は、ツールについては MCP で、作業の引き渡しについては A2A で、他のエージェントと連携する。
- **プラットフォームガバナンスのための 3 つのレイヤー。** Agent Client Protocol の記事は、エンタープライズの AI プラットフォームを統制するための 3 層モデルを提案している。MCP と Skills が再利用可能なエンタープライズの能力を担い、ACP が開発者とアシスタントの間のインタラクション層となり、A2A がエージェント間の協働ネットワークとなる。
- **AI をシステムの一員にする 3 つのレイヤー。** [[DefinedTerm/spec-driven-development]] に記録されている仕様駆動開発に関するハンドブックの章は、3 層のプロトコルスタックを説明している。MCP は AI がツールとどうやり取りするかを定め、A2A はエージェント同士の協働を可能にし、AG-UI はユーザーとエージェントの間にリアルタイムで目に見えるインタラクションを確立する。

MCP と A2A は、これらのグループ分けのすべてに登場する。サーベイのロードマップには、コマース、決済、ユーザーインターフェースのためのレイヤーがない。Google の 2 本の記事は、ANP もどちらの ACP も含んでいない。

## 違いがあるところ

### 誰が誰と話すか

MCP はエージェントとツールを結ぶ。A2A、Agent Communication Protocol、ANP はエージェントと他のエージェントを結ぶ。これらは次のように説明の仕方が異なる。

| プロトコル | 説明のされ方 |
| --- | --- |
| A2A | ケイパビリティに基づく Agent Card を通じた、ピアツーピアのタスク委任 |
| Agent Communication Protocol | 軽量で、ランタイムに依存しない HTTP メッセージング |
| ANP | 分散型識別子を通じた、オープンネットワーク上での発見 |

残りの 5 つのプロトコルは、それぞれ特定の 1 つの相手に向き合っている。

| プロトコル | 相手 |
| --- | --- |
| Agent Client Protocol | 開発者のエディタ |
| UCP | 販売者 |
| AP2 | 購入を承認する人物 |
| A2UI | 描画を行うクライアント |
| AG-UI | ストリームを受信するフロントエンド |

### 発見

ソースは発見をさまざまな形で説明している。

- **A2A** は Agent Card を well-known URL で公開する。A2A のページで引用されているホワイトペーパーの章は、Nacos が A2A レジストリとして機能する例も説明している。
- **UCP** は `/.well-known/ucp` にプロファイルを公開する。Google のガイドは、これを A2A が使うのと同じ発見パターンだとしている。
- **ANP** はオープンネットワーク上の分散型識別子に依拠する。
- **MCP** の発見は、エージェントが接続しているサーバー上のツールのメタデータを通じて行われる。
- **Agent Client Protocol** は、IDE とエージェントの間のケイパビリティネゴシエーションでセッションを開始する。JetBrains は、IDE の中からエージェントをインストールするための ACP Agent Registry も提供している。
- **AP2、A2UI、AG-UI** については、それらを説明するページに発見のステップがない。

ガイドは、well-known URL による発見、型付きスキーマ、標準的なイベントストリームを、自らが扱うプロトコルに共通するパターンとして挙げている。

### 制御と認可

プロトコルごとに、エージェントの行動をチェックする場所が異なる。

- **MCP：** ある説明は、同意とポリシーを管理する MCP Host を挙げている。同じ説明によれば、Tools は人間の承認によってゲートされる。
- **Agent Client Protocol：** ファイルの読み取り、編集、コマンドの実行はすべて、IDE から見えて監査できるツール呼び出しを経由する。機微な操作には IDE の許可が必要であり、IDE はユーザーが設定したポリシーのもとで自動的に許可することも、ユーザーに確認することも、差分として提示することもできる。
- **AP2：** 所有者が設定した上限を超える注文では、マネージャーが承認するまで `PaymentMandate` が署名されないままとなる。意図、承認、支払いは連鎖として記録される。

### 研究対象としてのセキュリティ

ソースはプロトコルをリスクの源としても扱っている。

- A2A のページで引用されているフレームワークは、ユーザーのデータを持ち出す信頼できない MCP サーバーの例を挙げている。
- MCP のページは、サードパーティのサーバーをサプライチェーン上の依存関係として精査すべきだという GitHub の助言を記録している。
- [[ScholarlyArticle/agentic-ai-security-threats-defenses-evaluation-and-open-challenges]] は、「マルチエージェントおよびプロトコルレベルの脅威」（multi-agent and protocol-level threats）を 5 つの脅威カテゴリーの 1 つとしている。同論文はプロトコルレベルの議論を MCP と A2A に限定している。ANP と Agent Communication Protocol には名前を挙げているが、扱ってはいない。

### 表明されている成熟度と採用状況

いくつかのページは、ソースが書かれた時点でプロトコルがどの段階にあったかを記録している。

- Google のガイドの時点で、AP2 は v0.1 だった。
- あるハンドブックの章は、2026 年の A2A のアップデートでエージェントディレクトリが追加されたと報告し、MCP をデファクトスタンダードになったものとして挙げている。
- サーベイは、扱う 4 つのプロトコルすべてを新興のものと呼んでいる。

採用状況を直接数えているソースが 1 つある。[[ScholarlyArticle/harness-engineering-anatomy-architecture-and-evolution-of-coding-agents]] は、2026 年 7 月のリリースに固定した 11 のコーディングエージェントシステムのソースコードを読んでいる。同論文の報告は次のとおりである。

- MCP は 11 システム中 8 つにある。SKILL.md 形式の Skills は 9 つに現れるため、同論文はスキルが今や採用状況で MCP を上回っていると結論づけている。
- Agent Client Protocol は 6 つのシステムにある。
- A2A は、このコーパスの中では Gemini CLI だけが持つ機能である。

これらの数はコーディングエージェントのハーネスだけを対象としており、プロトコルが説明されている他の場面は含まない。

## 重なり合うところ

これらのプロトコルは、互いの上で、あるいは互いと並行して動くものとして説明されている。

- UCP は MCP や A2A をトランスポートとして使える。
- AP2 は UCP の拡張である。
- Agent Client Protocol の記事は、ACP がエージェントと IDE の間のインタラクションを担い、MCP がエージェントの手の届く範囲を外部システムへと広げると述べる。同記事は ACP の機能の 1 つとして MCP サーバーのネイティブサポートを挙げ、JetBrains が ACP のもとで動くエージェントに MCP 統合を提供しているとも述べている。
- [[BlogPosting/agentic-engineering-swarms-of-ai-agents]] で説明されているデプロイメントでは、ワーカーエージェントが A2A で通信する。A2A に対応していないエージェントには MCP ラッパーを通じて到達し、A2A のネイティブサポートを持たないコーディングエージェントは MCP アダプターを通じて接続した。著者らは、これによってシステムが IDE に依存しなくなったと述べ、エージェント型の通信プロトコル間の相互運用性を、フレームワークを選ぶ際の基準の 1 つに挙げている。

### 本来の役割を超えた役割

Agent Client Protocol は、エディタとエージェントをつなぐこと以上の役割を果たしていると報告されている。

- ハーネスエンジニアリングの論文は、このプロトコルが第 3 の役割として、ハーネス全体をホストする役割を獲得したと述べる。その例は、OpenHands が Claude Code、Codex、Gemini CLI を交換可能なバックエンドとして動かすものである。
- Agent Client Protocol の記事は、AutoDev の統合を双方向のものとして説明している。AutoDev は ACP サーバーとしても ACP クライアントとしても動作できる。Claude Code のように ACP を話さないエージェントは、それ自身のストリーミング出力を解析することで適合させる。

### 1 つのフレームワークでのサポート

[[SoftwareApplication/agent-development-kit]] のページは、Google のガイドに示されているとおり、1 つのフレームワークがこれらのプロトコルのいくつかをどう扱うかを記録している。

| プロトコル | 説明されている ADK のサポート |
| --- | --- |
| MCP | MCP サーバー向けの `McpToolset`、および MCP Toolbox for Databases |
| A2A | ADK エージェントを A2A サービスに変えるユーティリティがある。`RemoteA2aAgent` は 1 ターンにつき 1 つのリモートエージェントにルーティングし、複数にまたがるクエリについてはガイドは `a2a-sdk` を直接使っている |
| A2UI | `adk web` インターフェースが A2UI コンポーネントをネイティブに描画する |
| AG-UI | エージェントを `ag_ui_adk` パッケージでラップし、FastAPI アプリにマウントする |
| AP2 | その型は ADK のコアではなく、別パッケージとして提供される |

ADK のページは、このフレームワークが UCP をどうサポートするかを説明していない。
