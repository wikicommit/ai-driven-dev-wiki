---
title: "Agentic Context Engineering"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agentic-context-engineering.md"
source_commit: "908ab492691e9fcd622bfa73c6c2fd839716bea1"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "AI エージェントのコンテキストを、静的な指示ファイルとしてではなく、generator／reflector／curator のパイプラインを通じて保守される進化するプレイブックとして扱うフレームワーク（ACE、ICLR 2026）。"
---

Agentic Context Engineering（ACE）は ICLR 2026 に帰されるフレームワークであり、AI エージェントのコンテキストを
`AGENTS.md` のような静的なファイルではなく、進化するプレイブックとして扱う。ACE はそのプレイブックを
generator／reflector／curator のパイプラインを通じて保守し、すべてのタスクに同じ固定の指示一式を読み込ませるのではなく、
タスクや状況の変化に応じてエージェントが目にする内容を適応させる。

## 用法

ソースはこれを「静的ファイル問題」への応答として挙げている。`AGENTS.md` のような固定されたファイルは、今どんな種類の
タスクが走っているかに応じて内容を変えることができないので、あるタスクには有用な指示（たとえば、コミット前に必ずテスト
スイートを全部走らせること）が、無関係なタスク（たとえば、ドキュメントだけの変更）では労力の無駄になりうる。ソースは、
エージェントのベンチマークにおいて ACE が静的なコンテキストの手法を 12.3% 上回ったと報告している。

## 適用される場面

単一の静的なコンテキストファイルが抱える固定的なコスト — 当てはまらないタスクにおいても無関係な指示がモデルの注意を
奪い合うこと — が、代わりに適応的なパイプラインを持ち込むに足るほど大きい場面に当てはまる。ソースはこれを、同じ静的
ファイルの限界に応える複数の提案の 1 つとして、別途説明されている 3 層のルーティングアーキテクチャと並べて提示しており、
2 つの手法が互いに直接比較されたとは述べていない。

## 関連用語

[[DefinedTerm/agents-md]], [[DefinedTerm/context-engineering]]
