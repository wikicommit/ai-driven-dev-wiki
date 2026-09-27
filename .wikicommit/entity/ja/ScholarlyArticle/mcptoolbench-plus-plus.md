---
title: "MCPToolBench++: 大規模な AI エージェント向け Model Context Protocol（MCP）ツール利用ベンチマーク"
type: "schema:ScholarlyArticle"
lang: ja
tags: [ベンチマーク, 評価, ツール利用, MCP]
review_status: pending
translated_from: ".wikicommit/entity/en/ScholarlyArticle/mcptoolbench-plus-plus.md"
source_commit: "770ac91fbc61b9b005a66b0665ab3295b8aaac32"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "LLM や AI エージェントが Model Context Protocol（MCP）ツールをどれだけうまく呼び出せるかを評価するための、大規模・多分野・多言語のベンチマーク MCPToolBench++ を紹介し、5 つのモデルの結果を報告する Ant Group の論文。"
  author: ["Shiqing Fan", "Xichen Ding", "Liang Zhang", "Linjian Mo"]
  datePublished: "2025"
  keywords: ["[[DefinedTerm/model-context-protocol]]", "ツール利用", "関数呼び出し", "ベンチマーク"]
---

Ant Group の Shiqing Fan、Xichen Ding、Liang Zhang、Linjian Mo による論文で、[[DefinedTerm/model-context-protocol]]（MCP）を通じて公開されたツールを LLM や AI エージェントがどのように利用するかを評価するためのベンチマーク [[Dataset/mcptoolbench-plus-plus]] を紹介している。著者らは、MCP ツール利用の評価が難しい理由として次の 4 つを挙げる。非常に多様な MCP ツールとスキーマを網羅する包括的なベンチマークが存在しないこと。MCP ツール呼び出しが多様な形式のレスポンスを返すこと。既存のツール利用ベンチマークにおけるプログラミング関数や数学関数とは異なり、実世界の MCP ツールは確実に成功するとは限らず、その成功率がサーバーによって異なること。そして、ツールやパラメータの説明が長いため、モデルのコンテキストウィンドウによって 1 回の実行で提示できるツールの数が制限されることである。

このベンチマークは、オープンな MCP マーケットプレイスから収集した MCP の設定とツールスキーマをもとに、自動パイプラインによって構築されている。2025 年 7 月時点で、そのマーケットプレイスには 40 以上のカテゴリにわたる 4,000 を超える MCP サーバーが掲載されていた。ツールサンプラーが単一のツールや最大 10 個のツールの連鎖を抽出し、クエリ生成器がそれらを正解のツール呼び出しラベル付きの自然言語クエリに変換し、後処理で意味的な妥当性や合理性のチェックに通らないクエリを除外する。こうして得られたベンチマークは、6 つのドメインにわたる約 1.5K の質問と回答のペアからなり、多言語のクエリも含む。

著者らは GPT-4o、Qwen2.5-max、Claude-3.7-Sonnet、Kimi-K2-Instruct、Qwen3-coder を評価し、精度の結果に加えて、MCP ツール呼び出しが失敗する理由の根本原因分析を示している。

## 主なポイント

- 論文はツール呼び出しを 2 つのレベルで評価する。1 つは [[Dataset/berkeley-function-calling-leaderboard]] にならった、正しいツールの選択とパラメータの記入を測る抽象構文木（AST）スコア、もう 1 つは、ツール呼び出しが実際に実行され、期待される正解と一致する結果を返すことまで求める Pass@K である。複数ステップの呼び出しについては、予測された実行計画と正解の実行計画を有向非巡回グラフとして比較する「AST DAG Accuracy」という指標を提案している。
- これとは別に、Tool Call Success Rate が MCP ツールごとに、エラーなく実行された割合を測定する。成功ステータスコードを返したレスポンスが実際に成功したかどうかの判断には、LLM を審査役として用いている。Pass@K を推定するため、各ツール呼び出しは 5 回実行された。
- すべてのカテゴリで首位に立つ単一のモデルはなかった。AST では、Qwen3-coder が Browser と Map、Qwen2.5-max が File System と Finance、Kimi-K2-Instruct が Search と Pay で首位だった。Pass@1 では、Qwen3-coder が Browser、Qwen2.5-max が File System、Claude-3.7-Sonnet が Search、GPT-4o が Map と Finance、Kimi-K2-Instruct が Pay で首位だった。
- AST と Pass@K の順位は必ずしも一致しない。Search では、Claude-3.7-Sonnet は AST で Kimi-K2-Instruct をわずかに下回った（0.728 対 0.732）が、Pass@1 では大きく上回った（0.620 対 0.368）。著者らはこれを、Google Custom Search ツールの成功率が Tavily など他の検索プロバイダよりも高く、Claude-3.7-Sonnet がそれをより頻繁に選んだためだとしている。似た機能を持つツールが複数ある場合、モデルは正解ラベルと一致していても、最終結果が大きく異なることがある。
- 著者らは、MCP ツールの実世界での成功率を、特に外部 API を呼び出すツールについて、Pass@1 の総合スコアを左右する重要な変数として挙げている。
- MCP ツール呼び出しの失敗の根本原因の上位は、パラメータエラー、API エラー、空の結果、セッションおよびランタイムエラーであり、ドメイン固有の失敗としては、地図ツールにおける範囲外の緯度・経度の値や、ブラウザツールで存在しないパスにスクリーンショットが保存されるケースがあった。
- 論文は、モデルにツールを提示する際のトークンコストが、インストールされたサーバー数、サーバーあたりの平均ツール数、各ツールのスキーマの長さに応じて増大すると分析し、クエリに関連するツールだけを取得する「Tool Dispatcher」を提唱している。これによりモデルに渡すツールを約 100 個から約 10 個に減らせるという。

## 補足

著者らは、結果を再現できるよう、ベンチマークで使用したすべてのツールを確認し、無料で利用できるか十分な無料呼び出し枠があることを検証したと述べている。また、モデルによって同じタスクへの経路が異なることにも言及している。たとえば経路計画では、住所を渡して単一のツールを呼び出すモデルもあれば、まず住所をジオコードや座標に変換するモデルもある。AST DAG Accuracy 指標では、予測された計画と正解の計画における各タスクの最後の実行ノードで一致が評価される。
