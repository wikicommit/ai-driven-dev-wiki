---
title: "Agentic Context Engineering（ACE）"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agentic-context-engineering.md"
source_commit: "0426e7f2036ea739db9b2cbdbaaed396066f6d6c"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "AI エージェントのコンテキストを、静的な指示ファイルとしてではなく、generator/reflector/curator のパイプラインによって維持される、進化し続けるプレイブックとして扱うフレームワーク（ACE、ICLR 2026）。"
---

Agentic Context Engineering（ACE）は、ICLR 2026 に帰されるフレームワークであり、AI エージェントのコンテキストを `AGENTS.md` のような静的なファイルではなく、進化し続けるプレイブックとして扱う。ACE はそのプレイブックを generator/reflector/curator のパイプラインによって維持し、あらゆるタスクで同じ固定の指示セットを読み込むのではなく、タスクや状況の変化に応じてエージェントが目にする内容を適応させる。

## 用法

出典はこれを「静的ファイルの問題」への対応として挙げている。`AGENTS.md` のような固定のファイルは、現在どのような種類のタスクが実行されているかに応じて内容を変えることができない。そのため、あるタスクには有用な指示（例: コミットの前に必ずテストスイート全体を実行する）が、無関係なタスク（例: ドキュメントのみの変更）では労力の無駄になりうる。出典は、エージェントのベンチマークにおいて ACE が静的なコンテキストのアプローチを 12.3% 上回ったと報告している。

## 適用される場面

単一の静的なコンテキストファイルの固定コスト、すなわち適用されないタスクにおいて無関係な指示がモデルのアテンションを奪い合うことのコストが、代わりに適応的なパイプラインを採用することを正当化できるほど大きい場合に適用される。出典はこれを、同じ静的ファイルの制約に応える複数の提案の 1 つとして、別途説明されている 3 層のルーティングアーキテクチャと並べて提示しているが、2 つのアプローチが互いに直接比較されたとは述べていない。

## 関連用語

[[DefinedTerm/agents-md]], [[DefinedTerm/context-engineering]]
