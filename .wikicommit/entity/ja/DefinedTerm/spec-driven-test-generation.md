---
title: "仕様駆動のテスト生成"
type: "schema:DefinedTerm"
lang: ja
tags: [仕様駆動開発, エージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/spec-driven-test-generation.md"
source_commit: "c044ecf40b811dd9fe94970a2c89786a7a0bda4f"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "LLM ベースのエージェントに対し、まずコードの事前条件、事後条件、未定義動作について推論してそれらを明示的に文書化するよう指示し、その中間的な半形式的仕様を、続いて書くテストの足場として用いさせるテスト生成手法。"
---

仕様駆動のテスト生成（Spec-driven test generation）とは、LLM ベースのコーディングエージェントにテストを書かせるためのプロンプティングの方法である。テストを直接求めるのではなく、エージェントにまずコードの事前条件、事後条件、未定義動作について推論し、それらを明示的に文書化するよう指示する。得られた中間的な半形式的仕様は、提案者が認知的な足場（cognitive scaffold）と呼ぶものとして、その後のテスト生成を導くために用いられる。この用語は [[ScholarlyArticle/grounding-ai-agents-in-contracts]] で提案された。

## 用法

この手法が付け加えるのは 1 つの成果物である。すなわち、コードの契約についての記述であり、それはどのテストよりも先に作成され、書き留められる。その動機は、直接的なプロンプティングに帰される失敗にある。テストを直接求められたエージェントは、コードとその根底にある契約について推論し損ね、その結果、テストの品質に関わるエッジケースや振る舞いの境界を見落とすことがある、というものである。

## 適用される場面

この手法は既存のコードに対するエージェント型のテスト生成のために提案されており、その設定で Google の本番環境のバグを対象に評価されている。従来のテスト生成エージェントと比べて報告されている改善は、バグ検出率で 9.8 パーセントポイント、分岐網羅率で 2.5 パーセントポイントである。モデルによる判定での比較では、そのベースラインに対して 77.8% のケースで、人間が作成したテストに対して 56.7% のケースで、この手法のテストスイートが好まれたと報告されている。

ここでこの用語が指すものは限定的である。仕様はエージェントによって、すでに存在するコードについて書かれ、実装を駆動するためではなく、そこから生成されるテストに根拠を与えるために用いられる。提案論文の発表の場がこれを位置づけている、より広い実践については [[DefinedTerm/spec-driven-development]] を参照のこと。

## 関連用語

[[DefinedTerm/spec-driven-development]], [[DefinedTerm/llm-as-a-judge]], [[DefinedTerm/test-design]], [[DefinedTerm/characterization-test]]
