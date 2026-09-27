---
title: "SWE-bench-java：Java 向けの GitHub イシュー解決ベンチマーク"
type: "schema:ScholarlyArticle"
lang: ja
tags: [ベンチマーク, 評価, コーディングエージェント, ソフトウェアエンジニアリング]
translated_from: ".wikicommit/entity/en/ScholarlyArticle/swe-bench-java-a-github-issue-resolving-benchmark-for-java.md"
source_commit: "0905902793f108bf59d40f17ccaecab6d323e38b"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "SWE-bench のイシュー解決ベンチマークの Java 版であり、手作業で検証された 91 件のイシューからなる SWE-bench-java-verified を、多言語でのイシュー解決評価に向けた第一歩として、Docker ベースの評価環境とリーダーボードとともに公開した論文。"
  author: ["Daoguang Zan", "Zhirong Huang", "Ailun Yu", "Shaoxin Lin", "Yifan Shi", "Wei Liu", "Dong Chen", "Zongshuai Qi", "Hao Yu", "Lei Yu", "Dezhi Ran", "Muhan Zeng", "Bo Shen", "Pan Bian", "Guangtai Liang", "Bei Guan", "Pengjie Huang", "Tao Xie", "Yongji Wang", "Qianxiang Wang"]
  abstract: "GitHub のイシュー解決はソフトウェアエンジニアリングにおける重要なタスクであり、LLM のイシュー解決能力を評価するために SWE-bench が公開されたが、これまで対象は Python のみだった。多言語対応への第一歩として、著者らは SWE-bench の Java 版である SWE-bench-java-verified を開発し、今後維持・更新していく Docker ベースの評価環境とリーダーボードとともにデータセットを公開した。その信頼性を確かめるために SWE-agent を実装して複数の LLM をテストしており、プルリクエストや共同作業による貢献を呼びかけている。"
---

この論文は、イシューの記述とバグを含むリポジトリからパッチを生成するようモデルに求めるイシュー解決
ベンチマーク [[Dataset/swe-bench]] を、Python の外へと拡張する。著者らは、SWE-bench が Python に
焦点を当てているため、その評価はデータ処理や人工知能といった分野に限られ、他の言語に依存する Web、
モバイル、システムプログラミングなどの領域が抜け落ちていると主張する。多言語ベンチマークへの第一歩
として著者らは Java 版を構築した。Java を選んだのは産業界での人気のためであり、C や C++ より Java を
選んだのは、それらの言語が選ばれる理由である性能上の問題に対処するようには、言語モデルが主として
設計されていないと考えたためである。

こうしてできたベンチマーク [[Dataset/swe-bench-java-verified]] は、SWE-bench の構築ワークフローに
従って 5 つのフェーズで作られている。候補リポジトリの収集、プルリクエストからのイシューインスタンスの
クロール、各イシューの実行環境の決定、fail-to-pass テストの抽出、そして SWE-bench Verified の
アノテーションガイドラインに従ったアンケートベースの手作業による検証である。論文はまた、パイプラインを
Java に移行する際に見つかった問題、すなわち元の SWE-bench スクリプトが誤ったベースコミットをクロール
することがあるエラー、リポジトリと依存関係の重複ダウンロード、インクリメンタルコンパイル中に
コンパイルが壊れる問題と、著者らがそれらにどう対処したかを説明している。

ベンチマークの信頼性を確かめるため、著者らは [[SoftwareApplication/swe-agent]] を複数のモデルで
実行している。解決率は全体的に低く、著者らはこれを、ベンチマークが挑戦的であり、モデル間の差を
識別できることの証拠と解釈している。

## 要点

- このベンチマークは、Java から始める多言語の GitHub イシュー解決評価への第一歩として提示されている。著者らは Go、Rust、C、C++ などの言語を追加する計画である。
- 構築の過程で、70 の候補リポジトリを 19 に絞り込み、そこから 1,979 件のイシューインスタンスをクロールし、決定した環境でコンパイルできる 308 件、少なくとも 1 つの fail-to-pass テストを持ち pass-to-fail テストを持たない 137 件を残し、手作業による検証を経て 6 リポジトリにまたがる 91 件のイシューとなった。
- 10 人の Java 開発者による手作業の検証では、イシューの明確さ、テストカバレッジ、重大な欠陥を評価し、明確でテストが十分にカバーしており重大な欠陥がないと評価されたイシューのみを残した。
- 著者らは、ブランチの違いを無視するために誤ったベースコミットを取ってしまうことがあった元の SWE-bench 収集スクリプトのバグを、git のコミットグラフを使って修正したと報告している。
- SWE-agent を用いた解決率は、91 件のイシューに対して 1.10%（GPT-4o-mini、Doubao-pro）から 9.89%（DeepSeek-V2）の範囲で、GPT-4o は 6.59%、DeepSeek-Coder-V2 は 7.69% だった。
- 著者らは、イシューの記述が最も詳しいリポジトリでは DeepSeek-V2 が DeepSeek-Coder-V2 を上回り、記述が最も少ないリポジトリではその逆になることを観察しており、これをより詳細なタスク記述ほど自然言語理解を多く要求することを示唆するものと捉えている。

## 補足

著者らは、すべての Java イシューについて実行環境を構成しないまま急いで SWE-agent を実装したと
述べており、これはエージェントがイシューを再現する能力に影響し、結果が本来の性能より低くなっている
可能性がある。データセット、評価環境、リーダーボードはオープンソース化されており、論文のプロジェクト
リンクは multi-swe-bench.github.io と、Daoguang/Multi-SWE-bench という名前の Hugging Face
データセットを指している。この研究は [[DefinedTerm/software-issue-resolution]] のベンチマーク群の
中に位置づけられ、論文はイシュー解決以外での先行する多言語の取り組みとして、多言語コード生成
ベンチマークの HumanEval-X、MBXP、MultiPL-E を挙げている。
