---
title: "BriefingScript"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/briefingscript.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている、構造化され、バージョン管理され、機械可読なアーティファクト。自律型コーディングエージェントに対する詳細な作業指示書として機能し、成功基準、アーキテクチャ上のコンテキスト、戦略的な助言、既知の落とし穴をまとめたもの。"
---

BriefingScript とは、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）が、「Agent Coach」がエージェントに与える主要な仕様として提案しているアーティファクトであり、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] において [[DefinedTerm/briefing-engineering]] の成果物として導入されている。これは単なる意図の仕様以上のものとして説明されている。すなわち、シニア開発者がジュニア開発者に渡すような詳細な作業指示書であり、実装に依存しない従来のソフトウェア要求仕様書（Software Requirements Specification）とは異なるものである。

## 用法

BriefingScript は 4 種類の内容を組み合わせる。**What & Success Criteria**（何を作るかと成功基準）は、スクラムの「完成の定義（Definition of Done）」に似ているが、形式的でテスト可能な事前条件と不変条件によって補強された、検証可能なチェックリストである。**Architectural Context**（アーキテクチャ上のコンテキスト）は、主要なモジュール、データモデル、API などを含め、その作業がシステムのどこに位置づけられるかを明確にする。**Strategic Advice**（戦略的な助言）は、使うべきライブラリや避けるべきパターンなど、特定の実装アプローチを推奨する。**Potential "Gotchas"**（起こりうる落とし穴）は、微妙なビジネスロジック、性能上の制約、依存関係の問題など、既知の落とし穴を強調する。論文はこれを、硬直的で一度きりのウォーターフォール型の仕様ではなく、人間のコーチとエージェントとの反復的な対話を通じて進化する、生きたバージョン管理されたドキュメントだと説明しており、Markdown、YAML、JSON、あるいはドメイン固有のスキーマでシリアライズできるとしている。論文はこれを Donald Knuth の「文芸的プログラミング（literate programming）」をエージェント向けに発展させたものと位置づけており、主要なアーティファクトを、コードから、エージェントの作業の元となるロジックと意図を説明する人間が読めるスクリプトへと移すものだとしている。REST API のレート制限を実装する具体例が、Goal & Why、What & Success Criteria、All Needed Context、Implementation Blueprint、Validation Loop の各セクションに構造化された形で、論文の付録に示されている。

## 関連用語

[[DefinedTerm/briefing-engineering]], [[DefinedTerm/product-requirement-prompt]], [[DefinedTerm/loopscript]], [[DefinedTerm/mentorscript]]
