---
title: "MCPToolBench++"
type: "schema:Dataset"
lang: ja
tags: [ベンチマーク, 評価, ツール利用, MCP]
translated_from: ".wikicommit/entity/en/Dataset/mcptoolbench-plus-plus.md"
source_commit: "770ac91fbc61b9b005a66b0665ab3295b8aaac32"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "LLM や AI エージェントが Model Context Protocol（MCP）のツールをどの程度うまく使えるかを評価するための、正解のツール呼び出しラベルが付いた約 1.5K 件のクエリから成るベンチマーク。6 つのドメインにわたる単一ステップおよびマルチステップの呼び出しを対象とし、多言語のクエリを含む。"
  creator: ["Shiqing Fan", "Xichen Ding", "Liang Zhang", "Linjian Mo"]
  url: "https://github.com/mcp-tool-bench/MCPToolBenchPP"
---

MCPToolBench++ は、大規模言語モデルや AI エージェントが [[DefinedTerm/model-context-protocol]]（MCP）を通じて公開されたツールをどのように呼び出すかを評価するためのベンチマークである。自然言語のクエリと正解のツール呼び出しラベルを組み合わせ、単一ステップのクエリと、ツール呼び出しの連鎖を必要とするマルチステップのクエリを混在させており、世界各地の地図を使った経路探索や世界の金融市場に関する質問といった多言語のクエリも含む。Ant Group の研究者らによって [[ScholarlyArticle/mcptoolbench-plus-plus]] で導入された。

## 内容

各レコードは、クエリとそれを満たすために期待されるツール呼び出しを JSON 形式でまとめたものである。マルチステップのレコードでは呼び出しの順序と、どの呼び出しが先行する呼び出しの結果に依存するかが指定されており、1 つのリクエストに最大 10 個のツールを使う連鎖もある。論文によれば、インスタンスは 1,509 件で、Browser、File System、Search、Map、Finance、Pay の 6 カテゴリに分かれ、87 個の MCP ツールを利用している。最大のカテゴリは Map（500 インスタンス）、最小は Finance（90）である。ツールスキーマは 1 ツールあたり平均約 288 トークンであり、論文はこのベンチマークを、2025 年 7 月時点で 40 以上のカテゴリにわたる 4,000 以上の MCP サーバーを擁するマーケットプレイスの上に構築されたものと説明している。

## 来歴

MCP サーバーは smithery.ai、deepnlp.org、pulsemcp.com、modelscope.cn などのオープンな MCP マーケットプレイスから集められ、その設定ファイル、サーバーのメタデータ、ツールスキーマが収集されてローカルでインデックス化された。次にツールサンプラーが、単一のツール（復元抽出）と 2〜10 個のツールから成るマルチステップの連鎖（非復元抽出）を、1 つのカテゴリ内から、あるいは金融とプロット作成のように LLM が生成したカテゴリの組み合わせにまたがって抽出した。LLM 駆動のクエリジェネレーターがクエリのテンプレートを作成し、パラメータ値を生成し — 株式のティッカーシンボルやジオコードのような入力にはコード辞書を用いる — テンプレートを埋め、その結果を自然なクエリに書き換えた。後処理では、意味的チェック（たとえば、書き換えで地名に変換できなかった座標）や妥当性チェック（たとえば、ニューヨークから東京へ列車で移動する）に通らなかったクエリが除去された。

著者らは、使用したすべてのツールがテスト済みであり、結果を再現できるよう、提供元から無料のアクセスまたは十分な無料の呼び出し枠が得られるものだと述べている。このベンチマークは GitHub 上と Hugging Face のデータセットとして公開されている。

## 用途

[[ScholarlyArticle/mcptoolbench-plus-plus]] で著者らは、GPT-4o、Qwen2.5-max、Claude-3.7-Sonnet、Kimi-K2-Instruct、Qwen3-coder をこのベンチマーク上で評価し、すべてのカテゴリで首位に立つ単一のモデルは存在せず、ツール選択の正確さと実際の実行成功とでは必ずしもモデルの順位が一致しないと報告している。
