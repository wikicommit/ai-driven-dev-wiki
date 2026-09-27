---
title: "LangChain によるツール呼び出し"
type: "schema:BlogPosting"
lang: ja
tags: [ツール利用, エージェントフレームワーク, LLM]
translated_from: .wikicommit/entity/en/BlogPosting/tool-calling-with-langchain.md
source_commit: "136844949634913857d6d1eb26ef9cb9cfaf8876"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "モデルプロバイダーが互換性のない API でネイティブのツール呼び出しを提供していたことを受けて、プロバイダーに依存しないツール呼び出しのインターフェース（bind_tools、AIMessage の tool_calls 属性、create_tool_calling_agent）を紹介した、2024 年 4 月の LangChain ブログ記事。"
  author: ["The LangChain Team"]
  datePublished: "2024-04-11"
  publisher: "LangChain"
---

LangChain チームによるこの記事は、[[SoftwareApplication/langchain]] におけるツール呼び出しの標準インターフェースを紹介している。ツール呼び出しとは、モデルがプレーンテキストと並べて、あるいはその代わりに、ツール呼び出しのリストを返せるようにする機能である（[[DefinedTerm/tool-use-design-pattern]] を参照）。記事のきっかけは、ネイティブのツール呼び出しを提供するモデルプロバイダーが増えつつあり、それぞれが少しずつ異なるインターフェースを通じて提供していたこと――記事が最も高性能だとする OpenAI、Anthropic、Gemini の 3 社のものも互いに互換性がなかったと記事は指摘している――そして、コミュニティがそれらを切り替える標準的な方法を求めていたことである。

インターフェースは 3 つの部分からなる。モデル呼び出しにツール定義を付与する `ChatModel.bind_tools()`、モデルが実行すると決めたツール呼び出しを読み取るための `AIMessage.tool_calls` 属性、そして両方を実装する任意のモデルで動作するエージェントコンストラクターである `create_tool_calling_agent()` である。記事は、これが完全な後方互換性を持ち、ネイティブのツール呼び出しをサポートするすべてのモデルで利用できると述べている。

## 要点

- 記事は、ネイティブのツール呼び出しの起源を、記事の約 1 年前にリリースされ 11 月に「tool calling」へと発展した OpenAI の「function calling」に置いている。その後 12 月から 4 月にかけて、Gemini、Mistral、Fireworks、Together、Groq、Cohere、Anthropic が続いたとしている。
- ツール定義の形式はプロバイダーによって異なる――OpenAI は `name`、`description`、`parameters` を、Anthropic は `name`、`description`、`input_schema` を想定する。`bind_tools` は生の定義に加えて Pydantic クラス、LangChain のツール、通常の関数も受け付けるため、同じ定義をツール呼び出しに対応した任意のモデルで使える。
- ツール呼び出しは以前は `AIMessage.additional_kwargs` や `AIMessage.content` の中に、プロバイダー固有の形式で入っていた。`tool_calls` はそれらを `ToolCall` エントリーのリストとして返し、各エントリーは名前、引数、および省略可能な id を持つ。
- `create_tool_calling_agent()` は、OpenAI のツール呼び出し API に従うモデルでしか動作しなかった従来の `create_openai_tools_agent()` を一般化したものである。
- 同じインターフェースにより、[[SoftwareApplication/langgraph]] でのエージェント構築も簡単になる。
- `with_structured_output()` は、それをサポートするほとんどのモデルでツール呼び出しの上に構築されている。これは常に指定したスキーマで出力を返すため情報抽出に向いており、一方 `bind_tools` はモデルが 1 つのツール、複数のツール、あるいはツールを使わないことを選べるため、ユーザーへの応答も求められるエージェントに向いている。

## 背景

この記事はベンダーによる自社フレームワークの変更の告知であり、モデルにおけるネイティブのツール呼び出しへの流れは今後も続くと見込んでいると述べている。
