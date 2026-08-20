---
title: "検索拡張生成 (RAG) の包括的サーベイ: 進化、現在の情勢、今後の方向性"
type: "schema:ScholarlyArticle"
lang: ja
tags: [コンテキストエンジニアリング]
review_status: pending
translated_from: ".wikicommit/entity/en/ScholarlyArticle/comprehensive-survey-of-retrieval-augmented-generation.md"
source_commit: "1804b4f09d8e8e88510a78cca5839eb041febbe0"
translated_at: "2026-08-20"
translated_by: "claude-opus-5[1m]"

properties:
  description: "検索拡張生成を、その基礎的な概念から最新の水準まで追跡したサーベイ。基本的なアーキテクチャ、検索拡張型言語モデルにおける技術的進展、質問応答・要約・知識ベースのタスクにわたる応用、そしてスケーラビリティ・バイアス・倫理という未解決の課題を扱っている。"
  author: ["Shailja Gupta", "Rajesh Ranjan", "Surya Narayan Singh"]
  keywords: ["検索拡張生成", "サーベイ", "検索効率", "知識集約型タスク"]
---

Carnegie Mellon University の Shailja Gupta と Rajesh Ranjan、BIT Sindri の Surya Narayan Singh による本サーベイは、そのアブストラクトが「検索拡張生成（RAG）の包括的な研究であり、その基礎的な概念から現在の最新水準に至る進化を追跡する」と呼ぶものを提示している。[[DefinedTerm/retrieval-augmented-generation]] が何のためのものかについての枠づけは標準的なものである。RAG は検索の仕組みと生成型の言語モデルを組み合わせて出力の正確さを高め、LLM の主要な限界に対処する。

## 主な貢献

- **アーキテクチャ。** サーベイは RAG の基本的なアーキテクチャを、知識集約型のタスクを扱うために検索と生成がどのように統合されているかに焦点を当てて探究している。
- **技術のレビュー。** 検索拡張型言語モデルにおける主要な革新を含め、RAG における重要な技術的進展を詳細にレビューしている。
- **応用。** 質問応答、要約、知識ベースのタスクを含む諸領域にわたる応用を扱っている。
- **近年のブレークスルー。** 近年の研究上のブレークスルーを論じ、検索効率を高めるための新規の手法を取り上げている。
- **未解決の課題。** スケーラビリティ、バイアス、そして導入における倫理的懸念を含む、現在進行中の課題を検討している。

## 注記

本サーベイはソフトウェアエンジニアリングに特化したものではなく RAG の汎用的な扱いであり、本 wiki が収録しているのは領域固有の知見のためではなく、その進化と未解決の課題についての記述のためである。近年のブレークスルーが集まる軸として検索効率を特定している点が、本 wiki の主題領域の実践に最も直接つながる部分である。そこでは検索のコストと品質こそが、コーディングエージェントが正しいコードを見つけられるかどうかを決めるからである——[[DefinedTerm/semantic-search]] を参照。

この技術の創始的な定式化については [[ScholarlyArticle/retrieval-augmented-generation-for-knowledge-intensive-nlp-tasks]] を、本サーベイが記述する静的なパイプラインこそが限界なのだという議論については [[ScholarlyArticle/agentic-rag-survey]] を参照。
