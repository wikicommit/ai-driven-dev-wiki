---
title: "CodeActInstruct"
type: "schema:Dataset"
lang: ja
tags: [エージェント, ツール利用]
translated_from: ".wikicommit/entity/en/Dataset/codeactinstruct.md"
source_commit: "c30b98db983bd016bce35703f3ae928b84c5f04c"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "CodeAct を用いた 7k 件のマルチターン対話からなるインストラクションチューニング用データセット。Executable Code Actions Elicit Better LLM Agents の著者らが収集し、CodeActAgent のファインチューニングに用いた。"
  url: "https://github.com/xingyaoww/code-act"
---

CodeActInstruct は、[[DefinedTerm/codeact]] を用いた 7k 件のマルチターン対話からなるインストラクションチューニング用
データセットであり、[[ScholarlyArticle/executable-code-actions-elicit-better-llm-agents]] の著者らによって収集された。

## 内容

データセットには 7k 件のマルチターン対話が含まれており、論文はそのアクション形式を CodeAct としている。
この形式では、エージェントが実行可能な Python コードを出力し、統合された Python インタープリタがそれを実行し、
エージェントは複数ターンにわたって新たな観測を受けるたびに、以前のアクションを動的に修正したり新しいアクションを
出力したりする。

## 来歴

論文は、このデータセットを著者ら自身が収集したと述べており、CodeAct を用いた 7k 件のマルチターン対話からなるものと
説明している。研究全体については、コード、データ、モデル、デモが <https://github.com/xingyaoww/code-act> で
公開されているとされている。

## 利用

著者らは CodeActInstruct を用いて、Llama2 と Mistral から [[SoftwareApplication/codeactagent]] をファインチューニング
した。著者らは、このデータセットを既存のデータと組み合わせることで、モデルの汎用的な能力を損なうことなく
エージェント指向のタスクにおける性能を改善できると報告している。これは、このデータセット単独での学習についてではなく、
他のデータと組み合わせることについての主張である。
