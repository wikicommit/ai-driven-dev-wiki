---
title: "LoopScript"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/loopscript.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている、宣言的でバージョン管理されたアーティファクト。人間のコーチが、エージェントのワークフローにおけるタスク分解、求められる厳密さの水準、証拠の要件を標準作業手順書（Standard Operating Procedure）として定義できるようにし、場当たり的なプロンプトハッキングに取って代わるもの。"
---

LoopScript とは、エージェントがタスクをどのように実行するかを定義するために [[DefinedTerm/structured-agentic-software-engineering]]（SASE）が提案しているアーティファクトであり、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] において [[DefinedTerm/agentic-loop-engineering]]（ALE）の成果物として導入されている。論文はその動機として、エージェントはタスクの「重大さ」を自力では推測できない、という点を挙げている。エージェントは単純な依頼に対して「考えすぎ」たり、重要な依頼に対して期待を下回る成果しか出さなかったりすることがあるため、コーチには求められる厳密さの水準を明示的に伝える手段が必要になる。

## 用法

LoopScript では、次のような事項を指定できる。第一に、タスクの分解と並列化である。1 つの [[DefinedTerm/briefingscript]] を複数のエージェント、あるいは専門化されたエージェントからなる異種混成チームに割り当てることで、N バージョンプログラミングが可能になる。たとえば、7 件のチケットを解決しようとする開発者が、チケットごとに 4 件ずつ、合計 28 件のプルリクエストを並列に発生させる、といった具合である。第二に、ワークフロー戦略である。単純なバグ修正には完全な自律性を与える一方、重要なセキュリティパッチには多段階の厳格なレビュープロセスを課す、といった使い分けができる。第三に、証拠に基づく受け入れ基準であり、最終成果物である [[DefinedTerm/merge-readiness-pack]] の構造を定義する。論文はこれを、コーチが動的に調整できる生きたドキュメントだと説明している。たとえば、有望な方向性により多くのエージェントを割り当てたり、初期の結果が不確かに見える場合にレビューのチェックポイントを追加したりできる。また論文は、LoopScript を DevOps の実践、すなわち宣言的パイプライン、Infrastructure as Code、オブザーバビリティの直系の子孫として位置づけている。さらに、一部の最先端のコーディングエージェントにはすでにこの要素が見られると指摘している。Google の [[SoftwareApplication/google-jules]] は当初から計画ステップを備えていた一方、Anthropic の [[SoftwareApplication/claude-code]] は、エージェントが計画を生成し、人間のレビューを待ってから先に進むオンデマンドの計画モードを最近になってようやく追加した。

## 関連用語

[[DefinedTerm/agentic-loop-engineering]], [[DefinedTerm/briefingscript]], [[DefinedTerm/merge-readiness-pack]]
