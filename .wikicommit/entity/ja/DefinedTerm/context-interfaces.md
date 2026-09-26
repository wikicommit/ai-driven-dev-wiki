---
title: "コンテキストインターフェース"
type: "schema:DefinedTerm"
lang: ja
tags: [コーディングエージェント, コンテキストウィンドウ]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/context-interfaces.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Birgitta Böckeler が提唱した用語で、コーディングエージェントの LLM に対して、必要と判断した場合にさらにコンテキストを得る方法を示す記述を指す。組み込みツール、MCP サーバー、スキルなどがこれにあたる。"
---

コンテキストインターフェース（context interfaces）とは、この用語を導入したメモの言葉を借りれば、LLM が必要と判断した
場合にさらにコンテキストを得る方法を LLM に向けて示した記述である。Birgitta Böckeler は
[[BlogPosting/context-engineering-for-coding-agents]] でこの名称を提唱し、この種のものを指す確立した用語が見つから
なかったと述べている。彼女はこの用語を使って、コーディングエージェントにおけるこの種のコンテキスト設定を、コンテキストに
直接置かれる再利用可能なプロンプト（指示やガイダンス）と区別した。

## 用法

同メモは、コンテキストインターフェースを三種類挙げている。**ツール**は、bash コマンドの実行やファイルの検索といった
コーディングエージェントの組み込み機能である。**MCP サーバー**（[[DefinedTerm/model-context-protocol]]）は、ローカルまたは
サーバー上で動作するカスタムのプログラムやスクリプトで、エージェントにデータソースやその他のアクションへのアクセスを
与える。**スキル**（[[DefinedTerm/agent-skills]]）は、追加のリソース、指示、ドキュメント、スクリプトについての記述で、
LLM が関連すると判断したときに必要に応じて読み込めるものである。同メモは、ワークスペース内のファイルの読み取りと検索を、
最も基本的かつ強力なコンテキストインターフェースとして特に取り上げている。エージェントが現在のコードベースを理解するのは
それらを通じてだからである。

設定された各インターフェースの記述はコンテキスト内の領域を占めるため、同メモは、特定のタスクが実際にどのコンテキスト
インターフェースを必要とするのかを戦略的に考えるよう勧めている。また同メモは、コンテキストをいつ読み込むかを LLM に
判断させること（その例としてスキルを挙げている）こそがエージェントを監督なしで動かせるようにしている一方で、期待した
ときにコンテキストが実際に読み込まれるかどうかにはある程度の不確実性が残る、とも指摘している。

## 関連用語

- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/agent-skills]]
