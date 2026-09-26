---
title: "メモリバンク"
type: "schema:DefinedTerm"
lang: ja
tags: [仕様駆動開発, コーディングエージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/memory-bank.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "コードベースについての汎用的なコンテキスト文書 — ルールファイルや、プロダクトとコードベースの高レベルな説明など — で、タスク固有の仕様とは区別され、あらゆる AI コーディングセッションに関係するもの。一部のツールが用いている名称で、Birgitta Böckeler がこのカテゴリーの呼び名として採用した。"
---

メモリバンクとは、AI コーディングエージェントにすべてのセッションを通じて与えられる、コードベースについての汎用的なコンテキスト文書の集まりである。たとえばルールファイルや、プロダクトとコードベースの高レベルな説明がこれにあたる。[[BlogPosting/understanding-spec-driven-development-kiro-spec-kit-and-tessl]] で Birgitta Böckeler は、一部のツールがこの種のコンテキストに用いているという名称を採用し、それを [[DefinedTerm/spec-driven-development]] における仕様と区別している。メモリバンクのファイルはそのコードベースでのあらゆる AI コーディングセッションに関係するのに対し、仕様は、それが記述する特定の機能を作成または変更するタスクにのみ関係する。

## 用法

この記事がメモリバンクのファイルの例として挙げるのは、[[DefinedTerm/agents-md]]、プロジェクトの説明、アーキテクチャの説明である。記事はまた、この概念を 3 つの SDD ツールに対応づけている。[[SoftwareApplication/kiro]] ではメモリバンクは「steering」と呼ばれ、Kiro にステアリング文書の生成を依頼するとデフォルトで product.md、structure.md、tech.md が作られるが、そのワークフローは特定のファイルが存在することに依存してはいないようである。[[SoftwareApplication/github-spec-kit]] では「constitution（憲法）」がこれにあたり、ワークフローの前提条件として、あらゆる変更に適用される高レベルで「不変の」原則を保持することを意図している — 著者の言葉では、非常に強力なルールファイルである。そして Tessl Framework（[[SoftwareApplication/tessl]]）では、framework フォルダーと KNOWLEDGE.md および AGENTS.md ファイルがこれに含まれていた。著者は、「メモリバンクをどう構成すればよいか」が実務者から最もよく受ける質問の一つだと述べている。

## 関連用語

- [[DefinedTerm/spec-driven-development-levels]]
- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/agents-md]]
