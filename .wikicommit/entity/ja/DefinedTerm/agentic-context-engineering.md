---
title: "Agentic Context Engineering"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agentic-context-engineering.md"
source_commit: "c6bf44a9d0262400c75a0abf7dee6a8fbb53ff80"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "AI エージェントのコンテキストを、静的な指示ファイルとしてではなく、generator/reflector/curator のパイプラインによって維持される進化するプレイブックとして扱うフレームワーク（ACE、ICLR 2026）。"
---

Agentic Context Engineering（ACE）は、ICLR 2026 として引用されているフレームワークであり、AI エージェントのコンテキストを `AGENTS.md` のような静的なファイルではなく、進化するプレイブックとして扱う。ACE は generator/reflector/curator のパイプラインによってそのプレイブックを維持し、すべてのタスクで同じ固定の指示セットを読み込むのではなく、タスクや状況の変化に応じてエージェントが目にする内容を適応させる。

## 用法

ソースはこれを「静的ファイル問題」への対応として引用している。`AGENTS.md` のような固定のファイルは、現在どのような種類のタスクが実行されているかに応じて内容を条件づけることができない。そのため、あるタスクには有用な指示（例: コミット前に必ずテストスイート全体を実行する）が、無関係なタスク（例: ドキュメントのみの変更）では労力の無駄になりうる。ソースによれば、エージェントのベンチマークにおいて ACE は静的なコンテキストのアプローチを 12.3% 上回った。

## 適用される場面

これが当てはまるのは、単一の静的なコンテキストファイルの固定コスト、すなわち当てはまらないタスクにおいて無関係な指示がモデルの注意を奪い合うことが、代わりに適応的なパイプラインを導入するに足るほど大きい場合である。ソースはこれを、同じ静的ファイルの限界に対応するいくつかの提案の 1 つとして、別に説明されている 3 層のルーティングアーキテクチャと並べて示しているが、2 つのアプローチが互いに直接比較されたとは述べていない。

## 関連用語

[[DefinedTerm/agents-md]], [[DefinedTerm/context-engineering]]
