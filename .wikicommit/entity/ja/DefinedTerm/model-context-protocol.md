---
title: "Model Context Protocol"
type: "schema:DefinedTerm"
lang: ja
aliases: ["MCP"]
tags: [エージェント, ツール利用]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/model-context-protocol.md"
source_commit: "48d80cbbb1b1176580f1d3e42bed65bbe89633ce"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "MCP サーバーが公開する外部ツールを AI エージェントが発見・選択・呼び出す方法を標準化するクライアント・サーバー型のプロトコル。ただし、ツールのメタデータや出力をどの程度モデルに公開すべきかは規定していない。"
---

Model Context Protocol（MCP）は、異種の実行環境にまたがって AI エージェントが外部ツールを発見し呼び出す方法を標準化する、クライアント・サーバー型のプロトコルである。MCP サーバーはツールのメタデータ（名前、入力スキーマ、説明）を公開し、エージェントは接続している複数のサーバーにわたってそれを照会できる。エージェントがツールを選択すると構造化されたリクエストを発行し、サーバーがそれを実行して結果をシリアライズされた形式で返す。

## 用法

[[ScholarlyArticle/from-determinism-to-delegation]] は、このプロトコルの起源とロール構造を説明している。異種のモデルを独自ツールに接続するには、従来は個別に作り込んだコネクタが必要だった。同論文は MCP を、N × M 通りのカスタム統合を単一のクライアント・サーバー契約に置き換えるものとして説明している。同論文が挙げるロールは 3 つあり、同意とポリシーを管理する **MCP Host**、個々のサーバーに接続する **MCP Client**、そして読み取り専用の **Resources**、JSON Schema で検証され人間の承認によって制御される実行可能な **Tools**、再利用可能な **Prompts** を公開する **MCP Server** である。標準化されたツールプロトコルがなぜ重要かについて、同論文の見方は構造的である。それらは、古典的なソフトウェアエンジニアリングが提供する決定論的な API をエージェントが発見し、それに基づいて行動することを可能にするものであり、同論文はこれを両分野の共生における技術的な継ぎ目と呼んでいる。

GitHub のブログに掲載された実務者による解説 [[BlogPosting/building-your-first-mcp-server]] は、同じ構造をサーバーを設定・構築する側の視点から説明している。ホストとは使用中の AI ツールであり（例として挙げられているのは VS Code 上の [[SoftwareApplication/github-copilot]]）、ホストは接続するサーバーごとにクライアントを 1 つ作成する。サーバーをホストに登録すること（VS Code では、サーバーを起動するコマンドを指定した `.vscode/mcp.json` のエントリ）によって、そのサーバーの機能がエージェントから利用可能になる。この記事は、ツール（AI が実行できるアクションで、それぞれに説明と入力スキーマを持つ）、リソース（AI が読み取れるコンテキストで、多くの場合 URI ベースの識別子で示される）、プロンプト（サーバーが同梱する定義済みのガイダンスで、VS Code ではスラッシュコマンドとして提示される）をサーバーの 3 つの中核的な構成要素として示し、その後の仕様にはサンプリングやエリシテーションなどの機能がさらに追加されたことにも触れている。実践的な助言としては、自分で構築する前に [[SoftwareApplication/github-mcp-server]] のような既存のサーバーを探すこと、そしてサードパーティのサーバーをサプライチェーン上の依存関係として精査すること（発行元が見覚えのある相手か、コードがレビューできる形で公開されているか）を挙げている。

Google の [[BlogPosting/developers-guide-to-ai-agent-protocols]] は、同じ契約を保守コストの側面から捉えている。同ガイドによれば、MCP がなければ開発者はエージェントが利用する各サービスのエンドポイントごとにカスタムツールを書いて保守することになるが、MCP があればサーバーが自らのツールを告知し、エージェントは単一の標準的な接続パターンを通じてそれらを自動的に発見する。さらに、MCP サーバーは基盤となるシステムを構築したチーム自身によって保守されるため、開発者が統合コードを書いたり更新したりしなくても、エージェントは最新のツール定義を得られると付け加えている。同ガイドの実例では、[[SoftwareApplication/agent-development-kit]] のエージェントが 3 つの MCP サーバーを通じて PostgreSQL データベースを読み取り、レシピを検索し、仕入れ先にメールを送る。同ガイドは締めくくりの助言として、ほとんどのエージェントはデータアクセスのために MCP から始め、要件が増えるにつれて他のプロトコルを追加していくと述べている。これは、Google 自身のフレームワーク向けのチュートリアルの中でなされた Google の推奨である。

MCP はツールのインターフェースを標準化するが、どの程度のメタデータと出力をモデルに公開すべきかは規定していない。MCP の実行モデルに関する研究 [[ScholarlyArticle/from-tool-orchestration-to-code-execution]] は、従来の構成をコンテキスト結合型の実行モデルと呼んでいる。既存の実装は、ツールのメタデータ、完全なスキーマ、ツールの出力をエージェントの推論コンテキストに直接シリアライズしており、そこではそれらがユーザー入力や途中の推論とスペースを奪い合う。同論文は、接続されるサーバーや利用可能なツールの数が増えるにつれ、こうした情報がコンテキストウィンドウに占める割合が大きくなり、推論に使える容量が減って、広いコンテキストを要する分析タスクの性能が低下すると論じている。つまり、コンテキスト結合型の実行はツールエコシステムの規模に対してスケールしないということである。

同論文は、ツールのオーケストレーションをエージェントのコンテキストウィンドウから切り離すことでこの制約に対処する、コンテキスト分離型の代替実行モデルとして [[DefinedTerm/code-execution-mcp]] を提示している。

エージェント間通信プロトコルのサーベイ [[ScholarlyArticle/a-survey-of-agent-interoperability-protocols]] は、MCP を安全なツール呼び出しと型付きデータ交換のための JSON-RPC クライアント・サーバー・インターフェースを提供するものとして説明し、他の 3 つの新興プロトコル、[[DefinedTerm/agent-communication-protocol]]、[[DefinedTerm/agent2agent-protocol]]、[[DefinedTerm/agent-network-protocol]] と並べて位置づけている。同サーベイが提案する段階的な導入ロードマップでは、ツールアクセスのための MCP が最初に来て、その後にメッセージング、協調的なタスク実行、分散型エージェントマーケットプレイスのために他の 3 つが導入される。

## 関連用語

- [[DefinedTerm/code-execution-mcp]] — コンテキストウィンドウを通じてツールを逐次呼び出す代わりに、単一の実行可能プログラムを生成する MCP の代替実行モデル
- [[ScholarlyArticle/from-tool-orchestration-to-code-execution]] — 従来の MCP と Code Execution MCP を、効率・タスク品質・セキュリティの面で比較した実証研究
- [[ScholarlyArticle/from-determinism-to-delegation]] — 上記の Host/Client/Server のロール構造と N × M の捉え方の出典
- [[BlogPosting/building-your-first-mcp-server]] — MCP サーバーを構築し、VS Code 上の GitHub Copilot に登録するまでの入門的な解説
- [[DefinedTerm/agent2agent-protocol]] — Google のプロトコルガイドが MCP と並べて位置づける、エージェント間通信の対応物
- [[ScholarlyArticle/a-survey-of-agent-interoperability-protocols]] — MCP を ACP、A2A、ANP と比較し、段階的な導入ロードマップを提案するサーベイ
