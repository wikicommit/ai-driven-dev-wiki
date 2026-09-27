---
title: "BriefingScript"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/briefingscript.md"
source_commit: "f3cd768971749927e49083efe4fbd9f44cf27fb0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている、構造化され、バージョン管理され、機械可読な成果物。自律型コーディングエージェントに対する詳細な作業指示書として機能し、成功基準、アーキテクチャ上のコンテキスト、戦略的な助言、既知の落とし穴を組み合わせる。"
---

BriefingScript は、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）が、「Agent Coach」がエージェントに渡す主要な仕様として提案する成果物であり、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] において [[DefinedTerm/briefing-engineering]] の産物として導入された。これは意図を記述した仕様以上のものとして説明されている。すなわち、実装に依存しない従来のソフトウェア要求仕様書（Software Requirements Specification）とは異なり、シニア開発者がジュニア開発者に渡すものに匹敵する詳細な作業指示書である。

## 用法

BriefingScript は 4 種類の内容を組み合わせる。**What & Success Criteria（何を作るかと成功基準）** は、スクラムの「完成の定義（Definition of Done）」に似ているが、形式的でテスト可能な事前条件と不変条件で補強された、検証可能なチェックリストである。**Architectural Context（アーキテクチャ上のコンテキスト）** は、主要なモジュール、データモデル、API などを含め、その作業がシステムのどこに位置づけられるかを明確にする。**Strategic Advice（戦略的な助言）** は、使うべきライブラリや避けるべきパターンなど、具体的な実装アプローチを推奨する。**Potential "Gotchas"（想定される落とし穴）** は、微妙なビジネスロジック、性能上の制約、依存関係の問題といった既知の落とし穴を強調する。論文はこれを、硬直的で一度きりのウォーターフォール型の仕様ではなく、人間のコーチとエージェントとの反復的な対話を通じて発展していく、バージョン管理された生きたドキュメントとして説明しており、Markdown、YAML、JSON、あるいはドメイン固有のスキーマでシリアライズしてよいとしている。論文はこれを Donald Knuth の「文芸的プログラミング（literate programming）」のエージェント指向の発展形と位置づけ、主要な成果物をコードから、エージェントの作業の拠り所となるロジックと意図を説明する人間が読めるスクリプトへと移すものだとしている。REST API のレート制限を実装する例が、Goal & Why、What & Success Criteria、All Needed Context、Implementation Blueprint、Validation Loop の各セクションで構成された形で、論文の付録に示されている。

## 関連用語

[[DefinedTerm/briefing-engineering]], [[DefinedTerm/product-requirement-prompt]], [[DefinedTerm/loopscript]], [[DefinedTerm/mentorscript]]
