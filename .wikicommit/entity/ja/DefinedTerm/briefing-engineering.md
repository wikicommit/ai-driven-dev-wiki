---
title: "Briefing Engineering（BriefingEng）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/briefing-engineering.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）において提案されているエンジニアリング活動で、エージェントへのミッションブリーフィングを執筆するもの — 要求仕様、アーキテクチャ設計、実装上の戦略的助言、テスト計画を、単一の BriefingScript という成果物へと融合させる。"
---

Briefing Engineering（BriefingEng）とは、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] において [[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として提案された、構造化されたエンジニアリング活動のひとつである。論文はこれを、エンジニアの主たる創造的成果が実装のロジックから、曖昧さのない意図と指導を言語化することへと移行する、その活動として位置づけており、要求工学およびアジャイル／スクラムのコミュニティによる数十年の蓄積を作り直すのではなく、その上に築くものだとしている。その目的として掲げられているのは、生の漠然としたチケットを貼りつけてエージェントによい結果を期待するというよくある失敗のパターンを超えて、ミッションのブリーフをファーストクラスの成果物として扱うことである。

## 使われ方

論文は Briefing Engineering を人間の Agent Coach に割り当て、[[DefinedTerm/agent-command-environment]]（ACE）の中で行われるものとしている。そこでは AI の支援が、曖昧さを指摘し、エッジケースを浮かび上がらせ、論理的な整合性を確かめ、プロパティベースの受け入れテストを生成することによって、コーチが質の高いブリーフを書く助けとなりうる。その成果物が [[DefinedTerm/briefingscript]] である。この活動に関する論文の研究ロードマップが求めているのは、目標・制約・不変条件・ドメインの文脈・受け入れ基準を、時期尚早な設計上の決定を強いることなく表現できる言語とスキーマ、脆い事例ではなくプロパティベースの受け入れ基準へとエンジニアを導く、AI を用いた執筆・レビュー支援、そして生成されたコードや証跡から、それらを動機づけたブリーフィングの条項へと遡れるトレーサビリティである。論文によれば、最後のものは、コーチが複数のエージェント生成の代替案を比較し正当化しなければならない場合（N バージョンプログラミング）にとりわけ重要になる。

## 関連用語

[[DefinedTerm/briefingscript]], [[DefinedTerm/structured-agentic-software-engineering]], [[DefinedTerm/product-requirement-prompt]]
