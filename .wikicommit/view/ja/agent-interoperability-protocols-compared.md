---
title: "エージェント相互運用プロトコルの比較"
lang: ja
kind: comparison
review_status: pending
translated_from: .wikicommit/view/en/agent-interoperability-protocols-compared.md
source_commit: 1a791d3f2e0c6d305eb03cf79739b27678bb8e32
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
---

この wiki には、AI エージェントが何かとつながる部分を標準化する 9 つのプロトコルのページがある。[[DefinedTerm/model-context-protocol]](MCP)、[[DefinedTerm/agent2agent-protocol]](A2A)、[[DefinedTerm/agent-communication-protocol]](ACP)、[[DefinedTerm/agent-network-protocol]](ANP)、[[DefinedTerm/agent-client-protocol]](こちらも ACP と略される)、[[DefinedTerm/universal-commerce-protocol]](UCP)、[[DefinedTerm/agent-payments-protocol]](AP2)、[[DefinedTerm/agent-to-user-interface-protocol]](A2UI)、[[DefinedTerm/agent-user-interaction-protocol]](AG-UI)である。このページでは、それぞれが何をつなぐか、メッセージをどう運ぶと説明されているか、発見と認可がどう機能するかという観点で、これらを並べて比較する。また、ソースごとにこれらがどうグループ分けされているかも扱う。比較には wiki のページに記録されている内容だけを用いる。新しいプロトコルの多くはそれぞれ 1 つのソースでしか説明されていないため、ここでそれらについて述べることはそのソースの説明である。

## それぞれが何をつなぐか

| プロトコル | つなぐもの | 説明されているトランスポートと形式 | 説明されている発見の仕組み |
| --- | --- | --- | --- |
| MCP | エージェントと外部のツールやデータ | JSON-RPC によるクライアント・サーバー型インターフェース。サーバーはツール名、入力スキーマ、説明を公開する | エージェントが接続先の各サーバーのツールメタデータを問い合わせる。VS Code ではサーバーを `.vscode/mcp.json` に登録する |
| A2A | エージェントと他のエージェント | A2A クライアントとサーバーの間で Task、Message、Artifact、Part を同期的に、またはストリーミングでやり取りする | `/.well-known/agent-card.json` の Agent Card、または直接設定、固定 URI、レジストリ |
| ACP(Agent Communication Protocol) | エージェント同士。汎用的なメッセージング向け | MIME タイプ付きマルチパートメッセージによる RESTful HTTP。同期・非同期の両方 | オンラインおよびオフラインの発見(サーベイがロードマップの段階と結びつけているもの) |
| ANP | オープンネットワーク上のエージェント | W3C の分散型識別子(DID)と JSON-LD グラフ | オープンネットワーク上でのエージェント発見 |
| ACP(Agent Client Protocol) | IDE やエディタとコーディングエージェント | 標準入出力上の JSON-RPC 2.0。エージェントは IDE のサブプロセスとして動く | セッション開始時のケイパビリティネゴシエーション。LSP の初期化ハンドシェイクに似ている |
| UCP | エージェントと加盟店のチェックアウトフロー | REST、MCP、A2A、Embedded Protocols のいずれの上でも同一に保たれる、強く型付けされたリクエスト・レスポンスのスキーマ | `/.well-known/ucp` の加盟店プロファイル |
| AP2 | 購入と、それを認可した人 | 型付きのマンデート(`IntentMandate`、`PaymentMandate`)と `PaymentReceipt` | 説明なし |
| A2UI | エージェントの出力と描画されるインターフェース | 18 種のコンポーネントプリミティブからなる固定カタログから取る宣言的な JSON。構造とデータは別々に送られる | 説明なし |
| AG-UI | エージェントフレームワークのイベントとフロントエンド | `TEXT_MESSAGE_CONTENT` や `TOOL_CALL_START` などの型付きイベントを流す Server-Sent Events ストリーム | 説明なし |

## ACP と呼ばれる 2 つのプロトコル

wiki にある異なる 2 つのプロトコルが ACP という略称を共有しており、それぞれがつなぐ相手は異なる。

- **Agent Communication Protocol** は、[[ScholarlyArticle/a-survey-of-agent-interoperability-protocols]] で扱われる 4 つのプロトコルの 1 つである。エージェントが HTTP 上で互いにメッセージをやり取りするためのプロトコルである。
- **Agent Client Protocol** は [[BlogPosting/acp-protocol-and-multiple-ai-coding-agents]] に由来する。IDE とコーディングエージェントの間に位置し、この記事はこれを Language Server Protocol になぞらえている。

ソースに「ACP」が出てきたときは、それがつなぐ当事者を見れば、どちらを指しているかがわかる。

## ソースによる整理の仕方

4 つのソースがそれぞれこれらのプロトコルの一部をグループ分けしており、いずれも異なる枠組みを使っている。

- **4 段階の導入ロードマップ。** サーベイは、MCP、ACP(Agent Communication Protocol)、A2A、ANP を、インタラクションモード、発見の仕組み、通信パターン、セキュリティモデルで比較している。そして導入の段階として次の順に並べている。
  1. MCP:ツールアクセス
  2. ACP:構造化されたセッション対応のメッセージング
  3. A2A:協調的なタスク実行
  4. ANP:分散型のエージェントマーケットプレイス
- **1 つのエージェント内の 6 つの層。** Google の [[BlogPosting/developers-guide-to-ai-agent-protocols]] は、MCP、A2A、UCP、AP2、A2UI、AG-UI を競合ではなく層として扱う。その例は [[SoftwareApplication/agent-development-kit]] のエージェントで、1 つのリクエストが 6 つすべてを使う。
  - MCP と A2A が情報を集める。
  - UCP と AP2 が取引を完了する。
  - A2UI と AG-UI が結果を提示する。

  このガイドは Google 自身のフレームワークのチュートリアルであり、コードサンプルはすべて ADK を使っている。
- **2 つのプロトコルからなるスタック。** A2A のページで引かれているハンドブックのある章は、業界は「MCP がツールをつなぎ、A2A がエージェントをつなぐ」という形に落ち着きつつあると述べている。この章によれば、両者を合わせたものがマルチエージェントシステムのプロトコル基盤となる。
- **プラットフォームガバナンスのための 3 つの層。** Agent Client Protocol の記事は、エンタープライズ AI プラットフォームを統制するための 3 層モデルを使い、ACP を MCP/Skills と A2A の間に置いている。このモデルでは、ACP がエージェントと IDE の間のやり取りを担い、MCP がエージェントの届く範囲を外部システムへ広げる。

4 つの枠組みすべてに登場するのは MCP と A2A だけである。サーベイのロードマップには、コマース、決済、ユーザーインターフェースの層がない。Google のガイドには ANP もどちらの ACP も含まれていない。

## 違いのあるところ

### 誰が誰と話すか

MCP はエージェントをツールにつなぐ。A2A、Agent Communication Protocol、ANP はエージェントを他のエージェントにつなぐ。これらは説明のされ方が異なる。

| プロトコル | 説明のされ方 |
| --- | --- |
| A2A | ケイパビリティに基づく Agent Card を通じたピアツーピアのタスク委譲 |
| Agent Communication Protocol | 軽量でランタイムに依存しない HTTP メッセージング |
| ANP | 分散型識別子によるオープンネットワーク上での発見 |

残りの 5 つのプロトコルは、それぞれ特定の 1 つの相手と向き合っている。

| プロトコル | 相手 |
| --- | --- |
| Agent Client Protocol | 開発者のエディタ |
| UCP | 加盟店 |
| AP2 | 購入を認可する人 |
| A2UI | 描画を行うクライアント |
| AG-UI | ストリームを受信するフロントエンド |

### 発見

ソースは発見をさまざまな形で説明している。

- **A2A** は Agent Card を well-known URL で公開する。
- **UCP** は `/.well-known/ucp` でプロファイルを公開する。Google のガイドはこれを A2A と同じ発見パターンだとしている。
- **ANP** はオープンネットワーク上の分散型識別子に依拠する。
- **MCP** の発見は、エージェントが接続しているサーバー上のツールメタデータを通じて行われる。
- **Agent Client Protocol** は、IDE とエージェントの間のケイパビリティネゴシエーションでセッションを開始する。
- **AP2、A2UI、AG-UI** は、それらを説明するページに発見のステップがない。

このガイドは、well-known URL による発見、型付きスキーマ、標準的なイベントストリームを、自らが扱うプロトコルに共通するパターンとして挙げている。

### 制御と認可

プロトコルごとに、エージェントの行動に対するチェックを置く場所が異なる。

- **MCP:** ある説明では、同意とポリシーを管理する MCP Host が挙げられている。同じ説明は、Tools は人間の承認によって制御されるとしている。
- **Agent Client Protocol:** ファイルの読み取り、編集、コマンドはすべて、IDE から見えて監査できるツール呼び出しを経由する。機密性の高い操作には IDE の許可が必要で、IDE はユーザーが設定したポリシーに基づいて自動的に許可するか、ユーザーに確認するか、差分として提示する。
- **AP2:** 所有者が設定した上限を超える注文は、マネージャーが承認するまで `PaymentMandate` が署名されないままになる。意図、認可、支払いは 1 本のチェーンとして記録される。

A2A のページで引かれているフレームワークは、プロトコルを構成要素であると同時にリスクの源としても扱う。その例は、ユーザーのデータを持ち出す信頼できない MCP サーバーである。MCP のページには、サードパーティのサーバーをサプライチェーン上の依存関係として精査すべきだという GitHub の助言が記録されている。

### 表明された成熟度

いくつかのページは、ソースが書かれた時点でプロトコルがどの段階にあったかを記録している。

- AP2 は Google のガイドの時点で v0.1 だった。
- あるハンドブックの章は、2026 年の A2A のアップデートでエージェントディレクトリが追加されたと報告し、MCP をデファクトスタンダードになったものとして挙げている。

サーベイは、扱う 4 つのプロトコルすべてを新興のものと呼んでいる。

## 重なり合うところ

これらのプロトコルは、互いの上で、あるいは互いと並んで動くものとして説明されている。

- UCP はトランスポートとして MCP や A2A を使える。
- AP2 は UCP の拡張である。
- Agent Client Protocol の記事は、機能の 1 つとして MCP サーバーのネイティブサポートを挙げている。
- A2A のページに記録されているとおり、[[BlogPosting/agentic-engineering-swarms-of-ai-agents]] で説明されているある導入事例では、A2A をネイティブにサポートしないコーディングエージェントを MCP アダプター経由で接続していた。
