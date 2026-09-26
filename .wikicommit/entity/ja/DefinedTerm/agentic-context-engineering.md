---
title: "Agentic Context Engineering"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agentic-context-engineering.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AI エージェントのコンテキストを、静的な指示ファイルとしてではなく、generator/reflector/curator のパイプラインによって維持される進化するプレイブックとして扱うフレームワーク（ACE、ICLR 2026）。"
---

Agentic Context Engineering（ACE）は、ICLR 2026 のものとして引用されているフレームワークであり、AI エージェントのコンテキストを、`AGENTS.md` のような静的なファイルではなく、進化するプレイブックとして扱う。ACE はそのプレイブックを generator/reflector/curator のパイプラインによって維持し、すべてのタスクに同じ固定の指示セットを読み込ませるのではなく、タスクや状況の変化に応じてエージェントが目にする内容を適応させる。

## 用法

出典はこれを「静的ファイル問題」への応答として引用している。`AGENTS.md` のような固定ファイルは、いまどのような種類のタスクが実行されているかに応じて内容を変えることができない。そのため、あるタスクには有用な指示（例：コミット前に必ずテストスイート全体を実行する）が、無関係なタスク（例：ドキュメントのみの変更）では労力の無駄になりうる。出典は、エージェント向けベンチマークにおいて ACE が静的なコンテキストの手法を 12.3% 上回ったと報告している。

## 適用される場面

単一の静的コンテキストファイルがもつ固定コスト — 適用されないタスクにおいても、無関係な指示がモデルの注意を奪い合うこと — が、代わりに適応的なパイプラインを採用することを正当化するほど大きい場合に当てはまる。出典はこれを、同じ静的ファイルの限界に応えるいくつかの提案のひとつとして、別途説明されている 3 層のルーティングアーキテクチャと並べて示しているが、両者が直接比較されたとは述べていない。

## 関連用語

[[DefinedTerm/agents-md]]、[[DefinedTerm/context-engineering]]
