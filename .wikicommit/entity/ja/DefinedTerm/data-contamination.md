---
title: "データ汚染"
type: "schema:DefinedTerm"
lang: ja
tags: [ベンチマーク, 評価]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/data-contamination.md"
source_commit: "5bacbd79c76dd8cc2c996065acd6063b17df868b"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "言語モデルの訓練データにベンチマークの問題が含まれていること。これによりモデルは実質的にすでに見たことのある問題で高得点を取れてしまい、ベンチマークは未知の問題に対するモデルの能力を過大に示すことになる。"
---

データ汚染とは、評価ベンチマークの問題が大規模言語モデルの膨大な訓練コーパスに含まれており、モデルが後でテストされるまさにその問題に遭遇していた可能性がある状況を指す。その場合、モデルのスコアの一部は新しい問題に対する能力ではなく記憶された内容を反映することになるため、汚染はモデルの能力について歪んだ、あるいは誤解を招く像を描きうる。[[ScholarlyArticle/livecodebench-holistic-and-contamination-free-evaluation-of-large-language-models-for-code]] は、過学習と並んで、これを HumanEval、MBPP、APPS といったコードベンチマークの欠点として挙げている。

## 用法

この用語は LLM の評価で使われ、コードモデルの評価もそこに含まれる。LiveCodeBench の論文は、先行研究が完全一致やあいまい一致によって訓練データの汚染除去を試みてきたこと、それが容易ではない場合があること、そして言い換えのような単純な方法で回避されうることを指摘している。論文が示す代替策は、時期で区切った評価である。[[Dataset/livecodebench]] は各問題に公開日のタグを付けており、モデルをその訓練カットオフ以降に公開された問題だけで採点できるようにしている。同じ日付によって汚染が可視化される。論文は、DeepSeek、GPT-4-O、Codestral の LeetCode 問題に対する性能が、各モデルのカットオフまたはリリース以降に公開された問題では大きく低下したと報告しており、これを、それ以前の問題がおそらく訓練データに含まれていた証拠と読んでいる。また、コードに対する編集距離や AST ベースの意味的類似度に基づく手法など、汚染の検出に関する関連研究も引用している。
