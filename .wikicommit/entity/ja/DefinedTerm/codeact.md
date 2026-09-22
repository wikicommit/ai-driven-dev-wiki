---
title: "CodeAct"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント, ツール利用, エージェントアーキテクチャ, 用語]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/codeact.md"
source_commit: "c30b98db983bd016bce35703f3ae928b84c5f04c"
translated_at: "2026-09-22"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "論文 Executable Code Actions Elicit Better LLM Agents で提案されたアプローチ。LLM エージェントのアクションを、あらかじめ定められた形式の JSON やテキストではなく、実行可能な Python コードという単一の統一されたアクションスペースへ集約する。"
---

CodeAct は、[[ScholarlyArticle/executable-code-actions-elicit-better-llm-agents]] が、実行可能な Python コードを用いて
大規模言語モデルエージェントのアクションを統一された [[DefinedTerm/action-space]] へ集約することに与えた名前である。これは、
あらかじめ定められた形式の JSON やテキストを生成することでアクションを出力するようエージェントに促す一般的な構成に対抗して
提案されている。論文はその構成を、あらかじめ定められたツールの範囲といった制約されたアクションスペースによって、また複数の
ツールを合成できないといった制限された柔軟性によって、限界づけられていると述べている。

## 用法

CodeAct は統合された Python インタプリタと対になる。それが備わっていれば、CodeAct はコードのアクションを実行し、新しい観察に
応じて先行するアクションを動的に修正したり新しいアクションを出力したりすることが、複数ターンのやり取りを通じてできると論文は
述べている——つまりコードはアクションの記法であるだけでなく、実際に走るものであり、その結果が次のターンへ送り込まれる。

## 適用される場面

このアプローチは、ツールを呼び出して環境に働きかけることで行動するエージェントに適用され、2 つのものが利用可能であることを
前提とする。エージェントの出力を実行できる Python インタプリタと、コードをアクションの形式として出力できるモデルである。
それらが成り立つ場合、論文の論点は、1 つのアクションスペースが、固定されたツールスキーマなら列挙しなければならないものを
包含する、というものである。複数のツールを合成することは、形式が備えねばならない機能ではなく、ありふれたコードだからである。

その位置づけは、定着した慣習ではなく、報告された比較を伴う提案のそれである。論文は API-Bank と新たに整備したベンチマークに
おける 17 の LLM の分析を報告しており、そこでは CodeAct が広く使われている代替手段を最大 20% 高い成功率で上回っている。
同じ著者らはさらに、CodeAct を用いた 7,000 件の複数ターンのやり取りからなるデータセット [[Dataset/codeactinstruct]] で
[[SoftwareApplication/codeactagent]] をファインチューニングしている。この研究は ICML 2024 に採択された。

## 関連用語

- [[DefinedTerm/action-space]]
- [[DefinedTerm/tool-use-design-pattern]]
- [[DefinedTerm/code-then-execute-pattern]]
- [[DefinedTerm/code-execution-mcp]]
