---
title: "SWE-bench ファミリーのベンチマーク"
lang: ja
kind: comparison
review_status: pending
translated_from: ".wikicommit/view/en/swe-bench-family-of-benchmarks.md"
source_commit: "919e25954936f0b338d88f77d1d4a0245c0b4a64"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
---

[[Dataset/swe-bench]] は、実際の GitHub のイシューを言語モデルとコーディングエージェントの評価に変えたものであり、その後のいくつかのデータセットは、その形式を再利用しつつ何かを変えている。このページでは、それらのデータセットを並べて比較し、それぞれが何を変えているのかを引き出し、このファミリーがどのように使われ、土台にされ、批判されているかについてウィキの他のページが記録していることを集める。ベンチマークの順位付けは行わない。

## 共通しているもの

ここにあるどのデータセットも、同じ基本的なタスクを保っている。インスタンスは、コードベースと解決すべきイシューを与え、評価対象のシステムはパッチを生成する。[[DefinedTerm/software-issue-resolution]] は、ウィキがこのタスクに用いる名前であり、[[ScholarlyArticle/advances-and-frontiers-of-llm-based-issue-resolution]] はこれを形式的に述べている。インスタンス `I = (D, C, T)` はイシューの記述、コードベース、テストを保持し、解決の間に観察できるのは記述とコードベースだけであり、パッチはテストを実行して評価される。集計指標は Resolved Rate で、インスタンスごとの二値の結果の平均である。ベンチマーク自身のサイトは、ホストしているファミリーの各メンバーについて **% Resolved** を報告している。

大半のデータセットでは、パッチが解決と数えられるかどうかはテストが決める。[[Dataset/swe-bench]] はユニットテストと継続的インテグレーションで正しさを確認する。[[Dataset/swe-bench-multimodal]] は、対応するプルリクエストの fail-to-pass テストと pass-to-pass テストを用いる。[[Dataset/swe-bench-java-verified]] は、与えられたテストケースがすべて通った場合にのみイシューを解決済みと数える。[[Dataset/swe-bench-plus]] は、各インスタンスが SWE-bench の形式に従うと述べており、SWE-bench 自身のオープンソースのスクリプトで収集された。[[Dataset/swe-bench-verified]]、[[Dataset/swe-bench-lite-s]]、[[Dataset/swe-bench-pro]]、[[Dataset/multi-swe-bench]] のページは、パッチの確認方法を記述していない。

## 並べて比較する

最初の 8 行は、このウィキに独自のページを持つデータセットである。最後の 3 行は、ベンチマーク自身のサイトが挙げ、[[Dataset/swe-bench]] のページに記録されているメンバーで、独自のページは持たない。

| データセット | ページが示す規模 | 言語 | 構築者 | SWE-bench と比べて何を変えているか |
|---|---|---|---|---|
| [[Dataset/swe-bench]] | 12 の Python リポジトリから 2,294 問 | Python | [[ScholarlyArticle/swe-bench-can-language-models-resolve-real-world-github-issues]] の著者ら | —（オリジナル） |
| [[Dataset/swe-bench-verified]] | 500 タスク | Python | OpenAI と SWE-bench の著者ら | 曖昧であったり仕様が不十分であったりしたタスクに対処する、人間が検証したサブセット |
| [[Dataset/swe-bench-lite-s]] | 記載なし | ページに記載なし | [[DefinedTerm/agentless]] 論文の著者ら | より厳密な比較のために、SWE-bench Lite を手作業でフィルタリングしたバージョン |
| [[Dataset/swe-bench-plus]] | 548 タスク | Python（Django を除く SWE-bench のプロジェクト） | [[ScholarlyArticle/swe-bench-plus-enhanced-coding-benchmark-for-llms]] の著者ら | 評価対象モデルの学習カットオフ後に作成されたイシューで、イシュー本文に解答が含まれていないかを選別したもの |
| [[Dataset/swe-bench-pro]] | 41 のリポジトリから 1,865 問 | ページに記載なし | [[ScholarlyArticle/swe-bench-pro-can-ai-agents-solve-long-horizon-software-engineering-tasks]] の著者ら | 長期的でエンタープライズレベルのタスク。一般公開されていないパーティションを含む |
| [[Dataset/multi-swe-bench]] | 1,632 インスタンス | Java、TypeScript、JavaScript、Go、Rust、C、C++ | [[ScholarlyArticle/multi-swe-bench-a-multilingual-benchmark-for-issue-resolving]] の著者ら | Python 以外の言語 |
| [[Dataset/swe-bench-java-verified]] | 6 つのリポジトリから 91 イシュー | Java | [[ScholarlyArticle/swe-bench-java-a-github-issue-resolving-benchmark-for-java]] の著者ら | SWE-bench Verified のアノテーションガイドラインで選別した Java 版 |
| [[Dataset/swe-bench-multimodal]] | 17 のリポジトリから 619 インスタンス（論文）、480（ベンチマークサイト） | JavaScript / TypeScript | [[ScholarlyArticle/swe-bench-multimodal-do-ai-systems-generalize-to-visual-software-domains]] の著者ら | すべてのタスクが視覚的なコンテンツを含む |
| SWE-bench Lite | 300 インスタンス | Python | SWE-bench のサイトに掲載 | より低コストな評価のために選定されたサブセット |
| SWE-bench Multilingual | 42 のリポジトリから 300 インスタンス | 9 つのプログラミング言語 | SWE-bench のサイトに掲載 | 複数の言語にまたがるタスク |
| Bash Only | Verified と同じ 500 インスタンス | Python | SWE-bench のサイトに掲載 | Verified リーダーボードのデフォルト表示で、すべてのモデルが同じ [[SoftwareApplication/mini-swe-agent]] 環境で実行される |

規模が情報源によって異なって示されているものが 1 つある。[[Dataset/swe-bench-multimodal]] について、導入論文は 619 のタスクインスタンス（アブストラクトでは 617）を報告し、それを 517 インスタンスのテストセットと 102 インスタンスの開発セットに分けているが、ベンチマークのサイトは 480 インスタンスとしている。SWE-bench Lite については、[[ScholarlyArticle/masai-modular-architecture-for-software-engineering-ai-agents]] が、その 300 のイシューが 11 の Python リポジトリから来ていると補足している。

## 登場の順序

各ページはいくつかのメンバーについて日付を示しており、それに従うと次の順序になる。

- **2023 年 10 月** — SWE-bench の論文が 2023 年 10 月 10 日に最初に投稿される。
- **2024 年 3 月** — ベンチマークのサイトによれば、SWE-bench Lite が公開される。
- **2024 年 6 月** — サイトは、評価を容易にするために SWE-bench が Docker 化されたことを記録している。
- **2024 年 7 月** — [[Dataset/swe-bench-lite-s]] を構築した Agentless の論文が、2024 年 7 月 1 日に最初に投稿される。
- **2024 年 8 月** — [[Dataset/swe-bench-verified]] が [[Organization/openai]] との共同作業として発表される。
- **2024 年 10 月** — サイトによれば、[[Dataset/swe-bench-multimodal]] が導入される。
- **2025 年 4 月** — Multi-SWE-bench の論文が 2025 年 4 月 3 日に投稿される。
- **2025 年 9 月** — SWE-Bench Pro の論文が 2025 年 9 月 21 日に最初に投稿される。

[[Dataset/swe-bench-plus]] は 2023-11-01 から 2024-08-22 までに作成されたイシューを集めているが、そのページは公開日を示していない。[[Dataset/swe-bench-java-verified]] のページも公開日を示していない。

## どこが異なるか

各バリアントはオリジナルに対する異なる不満に応えており、どの不満を取り上げるかによって、おおよそ 4 つのグループに分かれる。

### タスクが十分に仕様化されているか

[[Dataset/swe-bench-verified]] は、SWE-bench の一部のタスクが曖昧であったり仕様が不十分であったりするという懸念に対処するために公開された。その 500 のタスクは、十分に仕様化されていて解決可能であることが人間によって検証されている。[[Dataset/swe-bench-lite-s]] は、著者ら自身の分類によって同種の問題に対処している。Agentless の著者らは SWE-bench Lite の問題を手作業で分類し、正解パッチが exact であるイシューと、記述が不十分または誤解を招くイシューを除外した。[[Dataset/swe-bench-java-verified]] は Verified のアプローチを Java に持ち込んでいる。Java の経験を持つ 10 人の開発者が、SWE-bench Verified のガイドラインに従ってイシューの明確さ、テストカバレッジ、重大な欠陥を評価し、3 つの基準すべてを満たすインスタンスだけが残され、137 の候補が 91 に絞られた。[[Dataset/swe-bench-pro]] は、すべてのタスクが人間によって検証され、解決可能性を確保するのに十分なコンテキストで補強されていると述べている。

他のページは、古いセットで仕様の不十分さがどの程度要因として残っているかを記録している。[[ScholarlyArticle/specrover-code-intent-extraction-via-llms]] は、未解決のまま残った 207 の SWE-bench Lite のイシューのうち、107 がイシューの記述が曖昧なものだったと数えている。

### 答えがすでにモデルから見えているか

ここでは 2 種類の異なるリークが問題になる。[[DefinedTerm/solution-leakage]] は、イシューレポートやコメントがすでに修正内容を具体的に示しているインスタンスに対して SWE-Bench+ の著者らが与えた名前である。SWE-bench はその両方をモデルへの入力として与える（コメントは `hints_text` として）ため、モデルは修正を自分で導き出すのではなく写すことができる。もう 1 つの懸念は、モデルの学習カットオフより前のイシューが学習中に見られていた可能性があることである。SWE-Bench+ の論文は、SWE-bench のイシューとプルリクエストの 94% が、検討対象のモデルのカットオフより前に作成されていたと述べている。

[[Dataset/swe-bench-plus]] はこの両方に同時に対処する。著者らが使用したモデルの中で最も遅いカットオフの 1 か月後から始まる、2023-11-01 から 2024-08-22 までに作成されたイシューを取り、イシューレポートに明確な解答の詳細が含まれるものを取り除くために、すべてのインスタンスを手作業で確認している。[[Dataset/swe-bench-pro]] は、公開を控えるという別の方法で露出に対処している。41 のリポジトリのうち、11 が公開セット、12 がホールドアウトセット、18 がプロプライエタリなリポジトリからなる商用セットを構成し、ホールドアウトセットと商用セットの問題は一般公開されていない。著者らはこれを汚染耐性があると説明している。

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] は、SWE-Bench から、曖昧であったり仕様が不十分であったりしたタスクに対処した SWE-Bench Verified へ、そして OpenAI が SWE-Bench Verified がますますデータ汚染にさらされていると警告した後に推奨した SWE-Bench Pro へという流れを記述している。

各バリアントが、汚染が同じように重要だと見ているわけではない。SWE-bench Multimodal の論文は時間的な分析を報告しており、モデルの学習データに解答がリークしていたことがテストセットで有利に働いたという証拠は見つからなかった。[[Dataset/featurebench]] の論文は、タスクの成績はタスクのコミット日よりも、必要なコードの量にはるかに強く依存すると観察している。いくつかのシステム論文は、自らの結果についてこの懸念を提起している。[[ScholarlyArticle/lingmaagent-improving-automated-issue-resolution]] は、使用したモデルが学習中にテストリポジトリの一部を見ていた可能性を挙げており、SpecRover は正解と構文的に同一のパッチを数えることで記憶の有無を確認し、解決した 93 の Lite のイシューのうち 9 件を見つけている。DeepSWE の投稿 [[BlogPosting/deepswe-training-a-fully-open-sourced-state-of-the-art-coding-agent-by-scaling-rl]] は、汚染を避けるために、SWE-Bench-Verified にも登場するリポジトリを除外するよう学習タスクをフィルタリングしている。

### どの言語と領域をカバーするか

オリジナルは Python のリポジトリに限定されている。[[Dataset/multi-swe-bench]] は他の 7 つの言語をカバーしており、その導入論文は、SWE-bench を含む既存のベンチマークがほぼ Python だけに焦点を当てていることを動機として挙げている。[[Dataset/swe-bench-java-verified]] は、著者らによって多言語のイシュー解決評価への第一歩として提示されている。その論文は、SWE-bench が Python に焦点を当てているためにデータ処理や人工知能のような分野に限られ、Web、モバイル、システムプログラミングが取り残されていると論じ、著者らが Go、Rust、C、C++ を加える予定だと述べている。その論文のプロジェクトリンクは、multi-swe-bench.github.io と、Daoguang/Multi-SWE-bench という名前の Hugging Face のデータセットを指している。ベンチマークのサイトも、9 つの言語をカバーする SWE-bench Multilingual というセットを挙げている。

[[Dataset/swe-bench-multimodal]] は言語と領域の両方を変えている。そのタスクはユーザー向けの JavaScript ライブラリから来ており、すべてのタスクが問題文またはテストに視覚的なコンテンツを持つ。そして、Python のみの SWE-bench 向けに開発されたシステムが、他の言語や、視覚的に理解しなければならない問題に汎化するかを問うために構築された。その論文は、SWE-bench のタスクのうち画像を含むのは 5.6% にすぎないと指摘している。69 のタスクからなるサブセットは、レンダリングされたスクリーンショットを比較するピクセルレベルの視覚的テストで確認される。

Python から離れたことで、一部のシステムがどれほど強くオリジナルに適合させられていたかが明らかになった。Multimodal の論文は、AutoCodeRover と Moatless が Python 固有のプログラム解析に依存しているためベンチマークの対象にならなかったこと、そして Agentless にはゼロから書いた JavaScript パーサーが必要だったことを報告している。論文は、そこでの Agentless の低い結果を、Python を中心に設計された位置特定モジュールに帰している。

### どのような種類と規模のタスクか

[[Dataset/swe-bench-pro]] は、タスクの規模を中心に構築されたバリアントである。その導入論文は、その問題を、プロのエンジニアが数時間から数日かかることもある長期的なものであり、しばしば複数のファイルに大幅な変更を加えるパッチを伴い、ビジネスアプリケーション、B2B サービス、開発者ツールにまたがるリポジトリから来ていると説明している。比較として、SWE-bench のページで引用されているサーベイは、SWE-bench 自身の構成を、関数レベルのタスクが 65%、モジュールレベルが 25%、プロジェクトレベルが 10% 未満と特徴付けている。[[ScholarlyArticle/ai-agentic-programming-survey]] は、SWE-Bench をケーススタディとして用い、一般的に使われるコーディングベンチマークは Python に大きく偏っており、典型的には小さく自己完結した、あるいは関数レベルやモジュールレベルの問題を評価すると報告している。Multimodal の論文のアノテーターは、そのタスクは SWE-bench のタスクより解決に時間がかかり、参照解答がより多くのファイル、関数、行を編集していると見積もった。

タスクの種類は、規模とは別の軸である。FeatureBench の論文 [[ScholarlyArticle/featurebench-benchmarking-agentic-coding-for-complex-feature-development]] は、SWE-bench のインスタンスのうち機能要求は約 18〜22% にすぎないとし、プルリクエストに基づく収集では複数のプルリクエストにまたがる機能を捉えられないと論じている。

## キュレーションの方法

バリアントは、インスタンスの選び方でも異なる。

- **人間による検証**: [[Dataset/swe-bench-verified]]（十分に仕様化されていて解決可能であることを人間が検証）。
- **アノテーターによる手作業の検証**: [[Dataset/multi-swe-bench]]（2,456 の候補から 68 人の専門アノテーターが 1,632 のインスタンスをアノテーションしており、著者らはこれを正確で信頼できる評価を提供できる理由として挙げている）、[[Dataset/swe-bench-java-verified]]（10 人の Java 開発者）。
- **著者ら自身による手作業の点検**: [[Dataset/swe-bench-lite-s]]、[[Dataset/swe-bench-plus]]（解答の詳細について全インスタンスを点検）、[[Dataset/swe-bench-multimodal]]（残ったすべてのインスタンスを点検し、不可能と判断した 24 件を除去）。
- **人間が検証しコンテキストで補強したと表明**: [[Dataset/swe-bench-pro]]。

いくつかのバリアントは、収集パイプライン自体も変更している。[[Dataset/swe-bench-plus]] は SWE-bench の属性フィルタと実行フィルタを再利用した。SWE-bench-java の論文は、ブランチの違いを無視するために誤ったベースコミットを取ることがあった、オリジナルの SWE-bench の収集スクリプトのバグを修正したと報告している。[[Dataset/swe-bench-multimodal]] は、SWE-bench の Docker セットアップに Node.js と Chrome のサポートを追加し、繰り返し実行したときに結果が一貫しないテストを取り除いた。[[Dataset/multi-swe-bench]] の著者らは、コミュニティがデータセットを拡張し続けることを明示的な目的として、データ作成パイプライン全体をオープンソース化しており、このベンチマークを、強化学習の学習データとして 7 つの言語にわたる 4,723 のインスタンスを公開するコミュニティの取り組みである [[Dataset/multi-swe-rl]] と組み合わせている。

## バリアントがオリジナルについて報告していること

これらのページのいくつかは、各バリアントが中心に据えた不満を超えて、SWE-bench についての知見を記録している。SWE-Bench+ の論文は、フルの SWE-bench ですべてのテストを通った SWE-Agent+GPT-4 の 251 のパッチのうち、32.67% が解答リークだったと報告している。疑わしいパッチをフィルタリングすると、そのシステムの解決率はアブストラクトでは 12.47% から 3.97% に下がる（2.2 節では 5.49% としている）。また、SWE-bench Lite（18 件）と SWE-bench Verified（37 件）でもイシューに解答が含まれるインスタンスを特定し、疑わしい修正によって SWE-Agent+GPT-4 の解決率が Lite では 18% から 9.33% に、Verified では 22.4% から 10.0% に下がると報告している。つまり、Verified のページが記述するような仕様の品質についての人間による検証だけでは、解答リークは取り除かれなかった。

一方の欠陥をフィルタリングしても、もう一方の欠陥は取り除かれなかった。SWE-Bench+ では解答リークはもはや見られないが、弱いテストは残っている。解決済みとされたインスタンスの約 67.72% は実際にはイシューを解決しておらず、各システムの検証済みの解決率は、報告されている SWE-bench の数値をはるかに下回る。SWE-bench のページは、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] を通じて同じ系統の知見を引用している。「もっともらしい」修正の 29.6% が再テストでリグレッションを持ち込んだか誤っており、テストを通ることだけではパッチがマージ可能であることは確立されない。

あるシステム論文は、反対側から関連する測定に到達している。SpecRover の著者らは、解決した 93 の SWE-bench Lite のパッチを点検し、56 件（60.2%）が開発者のパッチと意味的に等価であり、残りの 37 件のうち 29 件が正解と同じメソッドを変更していることを見出した。

## ウィキの他のページはこのファミリーをどう読んでいるか

バリアント自体以外のページは、5 つの仕方でこのファミリーを取り上げている。

### モデル以外の要素にもスコアが左右される測定として

- [[BlogPosting/quantifying-infrastructure-noise-in-agentic-coding-evals]] と [[DefinedTerm/infrastructure-noise]] は、SWE-bench でのクロスオーバー実験を報告している。227 の問題にわたって利用可能な RAM を最大 5 倍まで変えたところ、スコアは 1.54 パーセントポイント動いた。これは Terminal-Bench 2.0 と同じ単調な効果だが規模は小さく、この用語のページは、それを SWE-bench のタスクがリソースをあまり消費しないことに帰している。
- [[ScholarlyArticle/survey-on-agent-system-and-harness-design]] は SWE-bench Verified のリーダーボードのデータをまとめ、同じモデルでもハーネスの選択によって、Claude 3.5 Sonnet が SWE-agent での 33.6% から PatchPilot での 53.6% まで動くことを示している。そして、この表は対照実験ではなく観察に基づくものだと注意を促している。
- [[ScholarlyArticle/coding-benchmarks-are-misaligned-with-agentic-software-engineering]] は、SWE-bench などを、単一のモデル、ハーネス、環境から単一の数値を出すものであり、個々のコンポーネントのレベルでのシグナルがないと説明している。
- [[ScholarlyArticle/agentic-ai-in-the-software-development-lifecycle]] は、ベンダーの報告と論文から SWE-bench Verified の推移をまとめている。2023 年 10 月の 1.96% から 2026 年 4 月の 78.4% まで上昇しており、この向上は生のモデル能力よりもスキャフォールディングが主因だと読んでいる。その数値は概数だと明記されている。
- [[ScholarlyArticle/harness-engineering-anatomy-architecture-and-evolution-of-coding-agents]] は、SWE-bench のもののような、モデルではなくエージェントを包む評価ハーネスを、エージェントハーネスと区別している。
- [[BlogPosting/devstral]] は、同じスキャフォールドの下での比較と、任意のスキャフォールドで評価されたモデルとの比較とを分けている。

### スコアに但し書きが必要なベンチマークとして

- [[ScholarlyArticle/advances-and-frontiers-of-llm-based-issue-resolution]] は、エージェントの成功率はしばしば解答リーク、曖昧なイシューの記述、弱いテストスイートによって水増しされていること、手作業でのクリーンアップは大規模には高コストすぎるため、分野はモデルベースの合意による自動検証へと移りつつあること、そしてベンチマークが飽和に近づくにつれて汚染が信頼性を脅かすことを報告している。また、SWE-bench を、ソフトウェアの*生成*から保守と進化への転換として位置付けている。
- [[ScholarlyArticle/vibe-coding-practice-performance-productivity-and-risk-a-state-of-the-art-review]] は、SWE-Bench Verified でのスコアの上昇を、汚染耐性のある評価や独立に実施された評価でのより低いスコアによって割り引いて読んでいる。
- [[ScholarlyArticle/human-in-the-loop-software-development-agents]] は、機能的な正しさの評価はユニットテストを通ることにとどまるべきではないと論じている。
- [[BlogPosting/demystifying-evals-for-ai-agents]] は、コーディングエージェントにとって自然な、決定論的でテストに基づく採点の例として SWE-bench Verified を挙げている。

### 別のベンチマークの土台として

- [[Dataset/swe-review-bench]] は、[[Dataset/swe-bench-verified]] の 500 のイシューからインスタンスを導いており、その指標が依存する実行可能なテストは Verified が提供している。
- [[Dataset/repocompliancebench]] は、SWE-bench のイシューからパッチへという土台と汚染に対する規律を再利用しているが、修正の品質ではなくコントリビューションルールへの準拠を測定する。
- [[Dataset/featurebench]] は、SWE-bench に対する、より難しく機能に焦点を当てた対応物として導入されている。SWE-bench と共通するリポジトリに限定したサブセットで、その論文は Claude Opus 4.5 がタスクの 5.2% を解決したと報告しており、同じモデルについて SWE-bench Verified で挙げている 74.40% と対比している。
- [[Dataset/swe-compass]] は、[[Dataset/swe-bench-verified]]、[[Dataset/swe-bench-pro]]、[[Dataset/multi-swe-bench]] がカバーする言語が少なく、多くの場合バグ修正しか扱わないことを根拠に、それらに対して自らを位置付けている。
- [[ScholarlyArticle/loopsbench-from-harness-engineering-to-loop-engineering-in-coding-agent-evaluation]] は、SWE-bench とそのバリアントが依然として終端的、すなわち最終的なタスクの成功で判定されるものだと論じ、代わりに依存構造を中心に [[Dataset/loopsbench]] を構築している。
- [[ScholarlyArticle/tracelab]] は、SWE-bench のような能力ベンチマークは狭い範囲のタスクを比較的少数しか含まないため、コーディングエージェントを提供するコストを左右するものを捉えていないと述べている。

### 学習シグナルの供給源として

[[DefinedTerm/critic-model]] と [[BlogPosting/learning-to-verify-ai-generated-code]] は、以前のクリティックモデルが、ユニットテストが検証済みの報酬を与える SWE-bench と SWE-Gym で学習されていたことを記録している。OpenHands は、ベンチマーク形式のデータだけで学習したクリティックが、本番環境での結果に対して約 0.45〜0.48 の AUC にとどまったと報告している。[[Dataset/multi-swe-rl]] はイシュー解決のインスタンスを強化学習の学習データとして公開しており、DeepSWE の投稿はソフトウェアエンジニアリングのタスクを強化学習の環境として扱い、SWE-Bench-Verified に登場するリポジトリを除外している。

### ついでに挙げられる名前として

いくつかのページは、SWE-bench を参照点としてのみ用いている。OpenHands の論文 [[ScholarlyArticle/openhands-an-open-platform-for-ai-software-developers-as-generalist-agents]] は、プラットフォームが取り込むソフトウェアエンジニアリングのタスクの例としてこれを挙げている。[[SoftwareApplication/openhands]] と [[BlogPosting/one-year-of-openhands-a-journey-of-open-source-ai-development]] は、SWE-Bench のようなベンチマークでの精度をプロジェクトの目標の 1 つとして挙げている。[[ScholarlyArticle/the-semi-executable-stack]] は、SWE-bench のようなエージェント型コーディングのベンチマークを主にそのリング 1〜3 に置いている。[[BlogPosting/building-effective-agents]] は、SWE-bench のタスク向けのコーディングエージェントを Anthropic 自身の例の 1 つとして挙げている。[[ScholarlyArticle/magentic-ui]] は、SWE-Bench 形式のタスクを苦手とするものの中に挙げている。[[ScholarlyArticle/agent-skills-for-large-language-models]] は、デプロイメントの軸で SWE-bench でのベンチマークの進展を取り上げている。[[ScholarlyArticle/building-effective-ai-coding-agents-for-the-terminal]] は、SWE-bench での評価を今後の課題として挙げている。[[SoftwareApplication/swe-agent]] のリポジトリは、SWE-bench をチームの関連プロジェクトと並べて提示しており、ベンチマーク自身のサイトは、[[SoftwareApplication/swe-agent]]、mini-SWE-agent、SWE-smith、SWE-ReX、SWE-bench CLI をベンチマークとともに 1 つのファミリーとしてまとめている。

## 各結果がどのメンバーで報告されているか

各ページは異なるメンバーでの結果を報告しており、どのメンバーかということは数値の意味の一部である。次の表は、各ページが報告する結果がどこで測定されたかを、そのページ自身の用語で挙げたものである。異なる行の数値は同じ条件の下で測定されたものではなく、いくつかのページは自らそう述べている。

| メンバー | 結果を報告しているページ |
|---|---|
| SWE-bench（フル） | 導入論文（Claude 2 で 1.96%）、[[ScholarlyArticle/swe-agent-agent-computer-interfaces-enable-automated-software-engineering]]（pass@1 で 12.5%）、[[BlogPosting/introducing-devin]] と [[Organization/cognition]]（ランダムな 25% のサブセットで、支援なしで 13.86%、比較対象のベースラインは支援あり）、SpecRover（19.31%）、SWE-Bench+ の監査、[[BlogPosting/stop-using-init-for-agents-md]] で説明されている ETH Zurich の研究、インフラストラクチャノイズのクロスオーバー実験 |
| SWE-bench Lite | [[ScholarlyArticle/autocoderover-autonomous-program-improvement]] と [[SoftwareApplication/autocoderover]]（19%）、[[ScholarlyArticle/agentless-demystifying-llm-based-software-engineering-agents]]（32.00%）、MASAI（28.33%）、[[ScholarlyArticle/marscode-agent-ai-native-automated-bug-fixing]] と [[SoftwareApplication/marscode-agent]]（34%）、LingmaAgent（GPT-4 Turbo で 21.33%、Claude 3.5 Sonnet と実行フィードバックで 38.33%）、SpecRover（31.00%）、[[ScholarlyArticle/spec-kit-agents-context-grounded-agentic-workflows]]（フックありで 58.2%、なしで 56.5%） |
| SWE-bench Verified | HULA（すべてのユニットテストを通ったイシューが 31%）、[[ScholarlyArticle/context-as-a-tool-context-management-for-long-horizon-swe-agents]] と [[DefinedTerm/context-as-a-tool]]（57.6%）、[[ScholarlyArticle/the-complexity-trap]] と [[DefinedTerm/observation-masking]]、DeepSWE（Pass@1 で 42.2%）、[[BlogPosting/openhands-context-condensation-for-more-efficient-ai-agents]]（サブセットで 54% 対 53%）、[[ScholarlyArticle/swe-pruner-self-adaptive-context-pruning-for-coding-agents]]、[[BlogPosting/how-were-making-github-copilot-smarter-with-fewer-tools]]、[[BlogPosting/writing-effective-tools-for-agents]] と [[DefinedTerm/tool-use-design-pattern]]、[[BlogPosting/learning-to-verify-ai-generated-code]]（結果が混在するサブセット）、[[ScholarlyArticle/swe-review]] と [[DefinedTerm/generate-review-revise-loop]]、[[BlogPosting/devstral]]（46.8%）、[[BlogPosting/introducing-devstral-2-and-mistral-vibe-cli]]（72.2% と 68.0%）、Agentless の v1.5 の実行、AutoCodeRover-v2（46.2%）、[[SoftwareApplication/mini-swe-agent]]、[[ScholarlyArticle/agentic-software-restructuring-paradigm]]、SDLC とハーネスのサーベイにまとめられた推移と表 |
| SWE-Bench Pro | [[BlogPosting/agent-driven-development-in-copilot-applied-science]]（スコアではなく軌跡の分析） |
| Multi-SWE-bench、SWE-bench-java-verified、SWE-bench Multimodal、SWE-Bench+ | それぞれ自身の導入論文のみ |

これらのページのいくつかは、数値についてそれぞれ但し書きを付けている。Devstral と Devstral 2 の投稿の数値は Mistral 自身のものである。[[SoftwareApplication/mini-swe-agent]] のページは、引用している数値が自己申告であり、モデルも日付も異なると注記している。AutoCodeRover の論文は、自ら実行したものではなく SWE-agent が報告した有効性と比較している。SpecRover のベースラインは他のツールが報告した数値である。MASAI の著者らは、SWE-bench Lite のイシューはテストで検証できるものに限られ、すべて英語であること、そして比較した手法の一部がヒントテキストのような追加の入力を用いていたことを注記している。
