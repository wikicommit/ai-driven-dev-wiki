---
title: "CodeAct"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント, ツール利用, エージェントアーキテクチャ, 用語]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/codeact.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "論文 Executable Code Actions Elicit Better LLM Agents で提案された手法。LLM エージェントのアクションを、事前に定められた形式の JSON やテキストではなく、実行可能な Python コードという単一の統一されたアクション空間に集約する。"
---

CodeAct とは、
[[ScholarlyArticle/executable-code-actions-elicit-better-llm-agents]] が、実行可能な Python コードを用いて
大規模言語モデルエージェントのアクションを統一された [[DefinedTerm/action-space]]（アクション空間）に集約することに
与えた名前である。これは、エージェントが事前に定められた形式の JSON やテキストを生成することでアクションを出力するよう
プロンプトされるという一般的な構成に対抗して提案されている。論文はその構成について、事前に定義されたツールの範囲といった
制約されたアクション空間と、複数のツールを組み合わせられないといった限定的な柔軟性によって制限されていると説明している。

## 用法

CodeAct は統合された Python インタープリタと組み合わせて使われる。インタープリタがある場合、論文によれば CodeAct は
マルチターンのやり取りを通じて、コードアクションを実行し、新たな観測に応じて以前のアクションを動的に修正したり
新しいアクションを出力したりできる。したがってコードは単にアクションを表す記法であるだけでなく、実際に実行されるものであり、
その結果が次のターンに反映される。

## 適用される場面

この手法は、ツールを呼び出して環境を操作することで行動するエージェントに適用され、2 つのものが利用可能であることを
前提とする。エージェントの出力を実行できる Python インタープリタと、アクションの形式としてコードを出力できるモデルである。
それらが満たされる場合、論文の主張は、固定されたツールスキーマが列挙しなければならないものを 1 つのアクション空間が
包含する、というものである。複数のツールを組み合わせることは、形式が用意しなければならない能力ではなく、
普通のコードにすぎないからである。

その位置づけは、確立された慣行というよりも、比較結果の報告に裏付けられた提案である。論文は API-Bank と新たに整備した
ベンチマークで 17 の LLM を分析し、CodeAct が広く使われている代替手法を最大 20% 高い成功率で上回ったと報告している。
さらに同じ著者らは、CodeAct を用いた 7k 件のマルチターンのやり取りからなるデータセット [[Dataset/codeactinstruct]] で
[[SoftwareApplication/codeactagent]] をファインチューニングしている。この研究は ICML 2024 に採択された。

## 関連用語

- [[DefinedTerm/action-space]]
- [[DefinedTerm/tool-use-design-pattern]]
- [[DefinedTerm/code-then-execute-pattern]]
- [[DefinedTerm/code-execution-mcp]]
