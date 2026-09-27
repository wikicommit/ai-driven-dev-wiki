---
title: "LiveCodeBench：コード向け大規模言語モデルの包括的で汚染のない評価"
type: "schema:ScholarlyArticle"
lang: ja
tags: [ベンチマーク, コード生成, 評価, データ汚染]
translated_from: ".wikicommit/entity/en/ScholarlyArticle/livecodebench-holistic-and-contamination-free-evaluation-of-large-language-models-for-code.md"
source_commit: "5bacbd79c76dd8cc2c996065acd6063b17df868b"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "コード LLM 向けの継続的に更新されるベンチマーク LiveCodeBench を導入した論文。日付の付いたコンテスト問題から構築されるため、モデルを学習データのカットオフ以降に公開された問題だけで評価でき、コード生成に加えて自己修復、コード実行、テスト出力予測もカバーする。52 のモデルを評価し、一部のモデルにおける汚染の証拠と、ファインチューニングされたオープンモデルにおける HumanEval への過剰適合の証拠を報告している。"
  author: ["Naman Jain", "King Han", "Alex Gu", "Wen-Ding Li", "Fanjia Yan", "Tianjun Zhang", "Sida I. Wang", "Armando Solar-Lezama", "Koushik Sen", "Ion Stoica"]
  keywords: ["ベンチマーク", "コード生成", "データ汚染", "自己修復", "コード実行", "テスト出力予測"]
---

この論文は、HumanEval、MBPP、APPS のような既存のコードベンチマークでは、もはや新しい LLM を評価するのに不十分だと主張する。これらは自然言語からコードへの生成しか測っておらず、問題が学習データに含まれうるため、汚染されていたり過剰適合されていたりする可能性がある。UC Berkeley、MIT、Cornell の著者らは [[Dataset/livecodebench]] を提案しており、これは 4 つの原則に基づいている。第 1 に、毎週のコンテストから新しい問題を収集して公開日のタグを付けるライブ更新であり、これによってモデルをそのカットオフ以降に公開された問題だけで採点できる。第 2 に、複数のコード関連能力にまたがる包括的な評価。第 3 に、高品質な問題とテスト。第 4 に、バランスの取れた問題難易度である。

このベンチマークはコード生成に加えて、[[DefinedTerm/self-repair]]（実行フィードバックから誤ったプログラムを修正すること）、コード実行（入力に対するプログラムの出力を予測すること）、そして新たに導入されたテスト出力予測タスク（問題文だけから与えられた入力に対する期待出力を作ること）を評価する。著者らはその動機として、推論、テスト生成、コード生成、自己修復を組み合わせて直接生成よりも性能を高める [[ScholarlyArticle/code-generation-with-alphacodium]] のようなパイプラインを挙げている。論文の時点で、ベンチマークには 2023 年 5 月から 2024 年 5 月までに公開された LeetCode、AtCoder、CodeForces の 511 問が含まれており、著者らは 18 のベースモデルと 34 の指示チューニング済みモデルを評価した。

## 主なポイント

- 時期で区切った評価によって、[[DefinedTerm/data-contamination]] の可能性が明らかになった。DeepSeek のモデルは 2023 年 8 月以降に公開された LeetCode の問題で、GPT-4-O は 2023 年 11 月（公表されたカットオフ）以降に公開された問題で、Codestral は 2024 年 2 月以降の問題で性能が大きく低下した一方、AtCoder の問題では性能は時期を通じて比較的安定していた。
- モデルの順位は 4 つのシナリオ間で高い相関を示した（すべての組で 0.88 超）が、相対的な差はばらついた。たとえば Claude-3-Opus はテスト出力予測で GPT-4-Turbo を上回った。
- HumanEval+ と LiveCodeBench の easy 分割を比較すると、相関は中程度（0.72）にとどまり、モデルは 2 つのクラスタに分かれた。HumanEval+ でのみ好成績を挙げたクラスタは主にファインチューニングされたオープンアクセスのモデルで構成されており、著者らはこれを HumanEval への過剰適合の可能性が高いと解釈している。
- GPT-4-Turbo、GPT-4、Gemini-Pro-1.5、Claude-3-Opus のようなクローズドな API モデルが大きな差をつけて首位に立ち、それに迫ったのはごく少数の大規模な指示チューニング済みオープンモデル（L3-Ins-70B、Mixtral、DS-Ins-33B）だけだった。
- 事後学習はベースモデルに比べてコード生成を改善し、著者らは、強力なベースモデルと高品質な事後学習データの組み合わせが優れたコード LLM を得るための有効なレシピであると結論づけている。
- GPT-4-Turbo は自己修復によって顕著に改善した（medium の問題で 24.5% から 36.9%）一方、Gemini-Pro の改善はわずかだった（8.5% から 9.4%）。

## 補足

著者らは限界として、汚染された時期を除外すると評価セットが小さくなること（349 問で、推定 1〜1.5% の性能のばらつき）、Python のみに焦点を当てていること、プロンプトをモデルごとに調整していないこと、そして問題領域が競技プログラミングに限られており、現実世界の自由度の高い LLM の使われ方を代表していない可能性があることを挙げている。彼らは LiveCodeBench をドメイン固有の評価と併用する出発点として使うことを推奨しており、さらに多くのプラットフォームと未公開のプライベートテストセットの追加を計画している。
