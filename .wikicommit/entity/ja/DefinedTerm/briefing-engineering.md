---
title: "Briefing Engineering（BriefingEng）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/briefing-engineering.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている、エージェントへのミッションブリーフィングを作成するエンジニアリング活動。要求仕様、アーキテクチャ設計、戦略的な実装上の助言、テスト計画を、単一の BriefingScript アーティファクトへと融合する。"
---

Briefing Engineering（BriefingEng）は、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で提案されている、構造化されたエンジニアリング活動の 1 つである。論文はこれを、エンジニアの主要な創造的アウトプットが実装ロジックから、曖昧さのない意図とガイダンスの明文化へと移る活動として位置づけており、要求工学（Requirements Engineering）やアジャイル／スクラムのコミュニティによる数十年の成果を作り直すのではなく、その上に積み上げるものだとしている。その目的として述べられているのは、生の曖昧なチケットを貼り付けてエージェントが良い結果を出すことを期待する、というよくある失敗パターンから脱し、ミッションブリーフを第一級のアーティファクトとして扱うことである。

## 用法

論文は Briefing Engineering を人間の Agent Coach に割り当てており、それは [[DefinedTerm/agent-command-environment]]（ACE）の中で行われる。ACE では AI による支援が、曖昧さを指摘する、エッジケースを浮かび上がらせる、論理的な一貫性を確保する、プロパティベースの受け入れテストを生成する、といった形でコーチが質の高いブリーフを作成するのを助けられる。この活動のアーティファクトは [[DefinedTerm/briefingscript]] である。この活動についての論文の研究ロードマップは、次のものを求めている。時期尚早な設計判断を強いることなく、目標、制約、不変条件、ドメインのコンテキスト、受け入れ基準を表現できる言語とスキーマ。脆い具体例ではなくプロパティベースの受け入れ基準へとエンジニアを導く、AI を活用した作成・レビュー支援ツール。そして、生成されたコードとエビデンスから、それらを動機づけたブリーフィングの条項へと遡るトレーサビリティである。論文によれば、このトレーサビリティは、コーチがエージェントの生成した複数の代替案（N バージョンプログラミング）を比較し、選択を正当化しなければならない場合にとりわけ重要になる。

## 関連用語

[[DefinedTerm/briefingscript]], [[DefinedTerm/structured-agentic-software-engineering]], [[DefinedTerm/product-requirement-prompt]]
