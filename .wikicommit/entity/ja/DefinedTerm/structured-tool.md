---
title: "構造化ツール"
type: "schema:DefinedTerm"
lang: ja
aliases: ["StructuredTool"]
tags: [ツール利用, エージェントフレームワーク]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/structured-tool.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "任意の数の型付き入力を受け取るツールを表す LangChain の抽象化。名前、説明、引数スキーマ、そしてツールを実行する関数によって定義され、単一の文字列しか受け付けなかった従来のツールと対比される。"
---

構造化ツールとは、2023 年 5 月に導入された LangChain の抽象化であり、エージェントが実行できるアクションのうち、単一の入力文字列ではなく、任意の型の入力を任意の数だけ受け取るものを指す。関数をラップしてエージェントから呼び出せるようにするもので、4 つの部分によって定義される。エージェントがどのツールを選ぶかを示す `name`、いつ・なぜそのツールを使うかを説明する `description`、引数とその型を宣言する Pydantic モデルである `args_schema`、そしてツールの同期処理と非同期処理のロジックを保持する `_run` および `_arun` 関数である。

## 用法

この用語は [[SoftwareApplication/langchain]] に属するものであり、`StructuredTool` クラスは [[BlogPosting/structured-tools]] で発表された。LangChain の説明によれば、`args_schema` は 2 つの役割を果たす。ツールが必要とする情報をエージェントに伝えることと、ツールの実行前にエージェントからの入力を検証することである。ツールは、関数のシグネチャからスキーマを推論する `StructuredTool.from_function()` を使って通常の関数から構築することも、より細かく制御するために `BaseTool` をサブクラス化して構築することもできる。構造化ツールは従来の文字列ツールを置き換えたわけではない。元の `Tool` クラスは `StructuredTool` と基底クラスを共有しており、1 つの文字列引数を取るツールは引き続き文字列ツールとして扱われる。LangChain はこうしたツールを使うために `StructuredChatAgent` をリリースした。従来のエージェントのプロンプトと出力パーサーは、カスタマイズなしでは複数引数のツールに対応できなかったためである。

## 関連用語

- [[DefinedTerm/tool-use-design-pattern]]
- [[DefinedTerm/react-prompting]]
