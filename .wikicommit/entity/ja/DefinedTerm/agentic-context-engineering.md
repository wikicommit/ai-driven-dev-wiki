---
title: "Agentic Context Engineering"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agentic-context-engineering.md"
source_commit: "908ab492691e9fcd622bfa73c6c2fd839716bea1"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AI エージェントのコンテキストを、静的な指示ファイルとしてではなく、generator/reflector/curator のパイプラインによって維持される、進化し続けるプレイブックとして扱うフレームワーク（ACE、ICLR 2026）。"
---

Agentic Context Engineering（ACE）は、ICLR 2026 のものとして引用されているフレームワークで、AI エージェントのコンテキストを、`AGENTS.md` のような静的なファイルではなく、進化し続けるプレイブックとして扱う。このプレイブックは generator/reflector/curator のパイプラインによって維持され、タスクごとに同じ固定の指示セットを読み込むのではなく、タスクや状況の変化に応じてエージェントが目にする内容を適応させる。

## 用法

出典はこれを「静的ファイル問題」への応答として取り上げている。`AGENTS.md` のような固定のファイルは、現在どのような種類のタスクが実行されているかに応じて内容を変えることができないため、あるタスクには有用な指示（例：コミット前に必ずテストスイート全体を実行する）が、無関係なタスク（例：ドキュメントのみの変更）では労力の無駄になりうる。出典は、エージェントのベンチマークにおいて ACE が静的なコンテキストのアプローチを 12.3% 上回ったと報告している。

## 適用される場面

単一の静的なコンテキストファイルが抱える固定コスト、すなわち当てはまらないタスクにおいて無関係な指示がモデルのアテンションを奪い合うことのコストが、代わりに適応的なパイプラインを用いることを正当化するほど大きい場合に当てはまる。出典はこれを、同じ静的ファイルの限界に応答するいくつかの提案のひとつとして、別途説明されている 3 層のルーティングアーキテクチャと並べて提示しているが、両アプローチが互いに直接比較されたとは述べていない。

## 関連用語

[[DefinedTerm/agents-md]], [[DefinedTerm/context-engineering]]
