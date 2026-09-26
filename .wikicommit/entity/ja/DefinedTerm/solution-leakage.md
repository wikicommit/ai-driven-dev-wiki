---
title: "解答リーク"
type: "schema:DefinedTerm"
lang: ja
tags: [ベンチマーク, 評価]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/solution-leakage.md"
source_commit: "90f235c19401779128f2c36166ba9e641fa1393d"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "イシュー解決ベンチマークのインスタンスが持つ欠陥の一つで、イシューの解決策がイシュー報告やそのコメントの中ですでに示されているため、そのテキストを与えられたモデルが修正を自ら導き出すのではなく書き写せてしまうもの。"
---

解答リーク（solution leakage）とは、[[ScholarlyArticle/swe-bench-plus-enhanced-coding-benchmark-for-llms]] の著者らが、イシューの解決策がイシューの説明やそれに付いたコメントの中で明確に示されているベンチマークインスタンスに与えた名前である。[[Dataset/swe-bench]] のようなイシュー解決ベンチマークは、イシューの説明とそのコメント（SWE-bench では `hints_text` と呼ばれる）の両方を入力としてモデルに与えるため、モデルは解決策を独自に生成する代わりに、そのテキストから直接抜き出すことができる。論文は、このようにして作られたパッチを「不正行為（cheating）」と表現し、問題解決能力を示すものではなく、与えられたものを再現しているにすぎないとしている。論文ではこれを「solution leak」や「answer leak」とも呼んでいる。

## 用法

この用語は、ベンチマークで報告される解決率が真の問題解決を測っているかどうかを評価する際に用いられる。論文は、必要なコードパッチそのものが説明に含まれていた sympy プロジェクトのイシューを例に挙げ、調査した SWE-Agent と GPT-4 による SWE-bench のパッチ 251 件のうち 32.67% が解答リークであり、解決済みインスタンスの中で最も多いパターンであったと報告している。また、SWE-bench Lite と SWE-bench Verified にもそうしたインスタンスを見つけている。著者らはこれへの対応として [[Dataset/swe-bench-plus]] を構築し、イシュー報告に明確な解決の詳細を含むインスタンスを手作業で取り除いた。

論文は、解答リークを隣接する二つの問題とは別のものとして扱っている。一つは弱いテストで、テストが検出できないために誤ったパッチや不完全なパッチが通ってしまう問題である。もう一つは潜在的なデータリークで、イシューとその修正がモデルのカットオフ日より前のものであるために、モデルの学習データに含まれていた可能性がある問題である。

## 関連用語

- [[DefinedTerm/data-contamination]]
- [[DefinedTerm/software-issue-resolution]]
