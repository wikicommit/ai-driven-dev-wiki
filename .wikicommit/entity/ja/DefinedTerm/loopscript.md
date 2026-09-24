---
title: "LoopScript"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/loopscript.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案された、宣言的でバージョン管理される成果物であり、人間のコーチがエージェントワークフローのタスク分解、厳密さの水準、証拠要件を標準作業手順書（SOP）として定義できるようにし、場当たり的なプロンプトハッキングに取って代わるもの。"
---

LoopScript とは、エージェントがタスクをどのように実行するかを定義するために [[DefinedTerm/structured-agentic-software-engineering]]（SASE）が提案する成果物であり、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] において [[DefinedTerm/agentic-loop-engineering|Agentic Loop Engineering（ALE）]]の産物として導入された。同論文は、エージェントはタスクの「重要度」を自力では推し量れない — 単純な依頼に対して「考えすぎ」たり、重要な依頼に対して不十分な成果しか出さなかったりする — ため、コーチには求められる厳密さの水準を伝える明示的な手段が必要である、という点をその動機として挙げている。

## 使われ方

LoopScript は、タスクの分解と並列化（1 つの [[DefinedTerm/briefingscript|BriefingScript]] を複数のエージェント、あるいは専門化されたエージェントからなる異種混成チームに割り当て、N バージョンプログラミングを可能にする — たとえば、開発者が 7 件のチケットを解決する際に、1 チケットあたり 4 件、計 28 件のプルリクエストが並行して作成される）、ワークフロー戦略（単純なバグ修正には完全な自律性を与える一方、重大なセキュリティパッチには厳格な多段階のレビュープロセスを課す）、そして証拠に基づく受け入れ基準（最終成果物である [[DefinedTerm/merge-readiness-pack]] の構造を定義する）を規定できる。同論文はこれを、コーチが動的に調整できる生きた文書 — たとえば有望な方向により多くのエージェントを割り当てたり、初期の結果が不確かに見える場合にレビューのチェックポイントを追加したりする — として描き、宣言的パイプライン、Infrastructure as Code、オブザーバビリティといった DevOps の実践の直系の子孫として位置づけている。また、一部のフロンティアなコーディングエージェントにはすでにその要素が見られると指摘している。Google の [[SoftwareApplication/google-jules]] は当初から計画ステップを備えていた一方、Anthropic の [[SoftwareApplication/claude-code]] は最近になって、エージェントが計画を生成し、人間のレビューを待ってから先へ進むオンデマンドの計画モードを追加したばかりである。

## 関連用語

[[DefinedTerm/agentic-loop-engineering]]、[[DefinedTerm/briefingscript]]、[[DefinedTerm/merge-readiness-pack]]
