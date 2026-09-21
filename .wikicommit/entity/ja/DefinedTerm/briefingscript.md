---
title: "BriefingScript"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/briefingscript.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）において提案された、構造化されバージョン管理された機械可読の成果物。成功基準、アーキテクチャ上の文脈、戦略的助言、既知の落とし穴を組み合わせ、自律的なコーディングエージェントへの詳細な作業指示書として機能する。"
---

BriefingScript とは、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）が、「Agent Coach」がエージェントに与える主たる仕様として提案する成果物であり、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] において [[DefinedTerm/briefing-engineering]] の産物として導入されたものである。これは意図の仕様を超えるものとして説明されている。すなわち、実装から独立した従来のソフトウェア要求仕様書とは異なり、シニアの開発者がジュニアの開発者に与えるであろうものに匹敵する、詳細な作業指示書である。

## 使われ方

BriefingScript は 4 種類の内容を組み合わせる。**What & Success Criteria（何を・成功基準）**は、スクラムの「完了の定義」に似た検証可能なチェックリストでありながら、形式的でテスト可能な事前条件と不変条件によって豊かにされたものである。**Architectural Context（アーキテクチャ上の文脈）**は、その作業がシステムのどこに位置づけられるかを、主要なモジュール・データモデル・API を含めて明らかにする。**Strategic Advice（戦略的助言）**は、使うべきライブラリや避けるべきパターンといった具体的な実装方針を推奨する。そして **Potential "Gotchas"（潜在的な落とし穴）**は、微妙な業務ロジック、性能上の制約、依存関係の問題といった既知の落とし穴を際立たせる。論文はこれを、硬直した一発勝負のウォーターフォール的な仕様書ではなく、人間のコーチとエージェントとの反復的な対話を通じて進化していく、生きたバージョン管理下の文書として説明し、Markdown、YAML、JSON、あるいはドメイン固有のスキーマでシリアライズされうると述べている。論文はこれを、Donald Knuth の「文芸的プログラミング」のエージェント向けの発展形と位置づけ、主たる成果物を、コードから、エージェントの作業がそこから導かれるロジックと意図を説明する人間可読なスクリプトへと移すものだとしている。REST API のレート制限を実装する具体例が、Goal & Why、What & Success Criteria、All Needed Context、Implementation Blueprint、Validation Loop の各節に構造化されて、論文の付録に示されている。

## 関連用語

[[DefinedTerm/briefing-engineering]], [[DefinedTerm/product-requirement-prompt]], [[DefinedTerm/loopscript]], [[DefinedTerm/mentorscript]]
