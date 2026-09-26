---
title: "CRISP プロンプトパターン"
type: "schema:DefinedTerm"
lang: ja
aliases: ["CRISP"]
tags: [プロンプティング, 仕様駆動開発]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/crisp-prompt-pattern.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "コーディングエージェントへのプロンプトのための 5 つの部分からなる構造。Context、Role、Instructions、Specifications、Polish/Criteria から成り、曖昧な依頼がもたらす推論トークンのコストを避ける方法として示されている。"
---

CRISP パターンは、コーディングエージェントへの依頼を書くための 5 つの部分からなる構造であり、[[BlogPosting/from-vibe-coding-to-spec-driven-development]] で、「ログインが動かない、直して」のような曖昧な意図に代わるものとして示されている。その頭文字は、**Context**（コードが実行される正確な環境）、**Role**（エージェントがまとうべき人物像）、**Instructions**（エージェントが何をすべきかを正確に）、**Specifications**（プロトコル、API、型、制約）、**Polish/Criteria**（完了の定義と受け入れ基準）を表す。

## 用法

この記事の具体的な対比では、1 行だけの手抜きのプロンプトと、CRISP に沿ったプロンプトが並べられている。後者は、ファイル、メソッド、エラーが発生する行とそれを引き起こす条件を指定し、どの既存のエラーハンドラーを使うかを示し、新しいファイルの作成を禁じている。記事はこのパターンを [[DefinedTerm/spec-driven-development]] の説明の中で用いており、そこではエージェントに渡すものの精度が、それ自体としてエンジニアリングの作業として扱われる。そして要点を、プロンプトをうまく書くことは「ingeniería de costes」、つまりコストのエンジニアリングである、とまとめている。

## 適用される場面

このパターンが狙うのは、記事が高くつくと述べる場面、すなわち不正確な依頼のせいで、モデルが手探りでファイルを探索し、有用なものに行き着くまで仮説を立て直し続けなければならない場面である。記事の主張は、その違いはコードの品質の問題であるだけでなく経済的なものでもあり、曖昧なプロンプトは、同じ結果に到達するために、正確なプロンプトより桁違いに多くの推論トークンを消費し、しかも誤りも多くなりうる、というものである。

どの程度確立しているか：ここで保持している説明はこの 1 本の記事だけであり、記事はこのパターンを特定の考案者に帰することなく示しており、コストに関する主張も測定ではなく一般論として述べている。

## 関連用語

- [[DefinedTerm/prompt-engineering]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/spec-driven-development]]
