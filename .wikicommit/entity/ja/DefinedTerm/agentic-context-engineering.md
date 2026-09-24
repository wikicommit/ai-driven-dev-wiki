---
title: "Agentic Context Engineering"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agentic-context-engineering.md"
source_commit: "ecc1bee15ae3ca4148e95adec43c589c16f912f2"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "AI エージェントのコンテキストを静的な指示ファイルとしてではなく、生成器／内省器／キュレーターのパイプラインによって維持される、進化するプレイブックとして扱うフレームワーク（ACE、ICLR 2026）。"
---

Agentic Context Engineering（ACE）は、ICLR 2026 を出典とするフレームワークであり、AI エージェントのコンテキストを `AGENTS.md` のような静的なファイルではなく、進化するプレイブックとして扱う。このプレイブックは生成器／内省器／キュレーターのパイプラインによって維持され、すべてのタスクで同じ固定の指示セットを読み込むのではなく、タスクや状況の変化に応じてエージェントが目にする内容を適応させる。

## 用法

ソースはこれを「静的ファイル問題」への応答として挙げている。`AGENTS.md` のような固定のファイルは、現在どのような種類のタスクが実行されているかに応じて内容を変えることができない。そのため、あるタスクには有用な指示（たとえば、コミット前に必ずテストスイート全体を実行する）が、無関係なタスク（たとえば、ドキュメントのみの変更）では労力の無駄になりうる。ソースは、エージェントのベンチマークにおいて ACE が静的なコンテキストの手法を 12.3% 上回ったと報告している。

## 適用される場面

単一の静的なコンテキストファイルの固定コスト、すなわち適用対象外のタスクにおいて無関係な指示がモデルの注意を奪い合うことのコストが、適応的なパイプラインを代わりに導入することを正当化するほど大きい場合に適用される。ソースはこれを、同じ静的ファイルの限界に応える複数の提案の 1 つとして、別途説明されている 3 層のルーティングアーキテクチャと並べて提示しているが、両者を直接比較したとは述べていない。

## 関連用語

[[DefinedTerm/agents-md]], [[DefinedTerm/context-engineering]]
