---
title: "有限のコンテキストウィンドウの中で作業する"
lang: ja
kind: landscape
review_status: pending
translated_from: ".wikicommit/view/en/working-within-a-finite-context-window.md"
source_commit: "013b5cc71eeffafccfe52ec7f414c7e0f1b40dd0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
---

このウィキがエージェントとそのコンテキストについて持つページ群は、1 つの前提を共有している。推論時に言語モデルが利用できるコンテキストは、満たすべき容器ではなく、限界収益が逓減する有限の資源だという前提である。このページはそのページ群への入口である。この領域がどこから始まるのか、なぜその制約が存在するとされるのか、何がウィンドウを埋めるのか、タスクがウィンドウに収まらなくなったときにセッション内とセッションをまたいで何がなされるのか、そしてこの領域が拠って立つ説明がどこから来ているのかを示す。

## 領域の出発点

入口は [[DefinedTerm/context-engineering]] である。このページは、推論中にモデルのコンテキストウィンドウを占める情報をキュレーションし、動的に管理する実践を名指すものであり、その実践についての異なる説明を並べて集めたページでもある。そこには、各説明がこの実践を [[DefinedTerm/prompt-engineering]] に対してどう位置づけるかも含まれる。すなわち、その自然な発展とみなすか、それとは根本的に異なるものとみなすか、それを部分集合として包含するものとみなすかである。その「When It Applies」節は、この領域が拠って立つ前提を述べている。この実践は、コンテキストが限界収益の逓減する有限の資源であることを前提としており、その根拠を特定のウィンドウサイズではなく、コンテキストロットとアテンション予算という捉え方に置いている。

## なぜウィンドウが希少なものとして扱われるのか

この制約を支える論拠は、経験的なページと説明的なページが担っている。

- [[DefinedTerm/context-rot]] は経験的な側面である。コンテキスト内の情報を想起するモデルの能力は、トークン数が増えるにつれて低下する。Anthropic はこの概念を「干し草の山から針を探す」（needle-in-a-haystack）型のベンチマークに由来するものとし、その効果を急な崖ではなく性能の勾配として説明している。
- [[DefinedTerm/attention-budget]] は説明的な側面である。これは、アテンションを追加のトークンごとに目減りしていく有限のプールとみなす Anthropic の捉え方であり、Anthropic はその原因を、Transformer のアテンションがトークン間に生み出すペアワイズの関係、短い系列のほうが一般的な訓練データの分布、そしてコンテキスト長を拡張する手法が伴う精度上のコストに求めている。

[[ScholarlyArticle/externalization-in-llm-agents]] は、アテンションの偏りと並ぶ第二の理由を加える。コンテキストは一時的なものであり、状態を別の場所に外部化しない限り、新しいセッションは毎回部分的な記憶喪失の状態から始まる。[[DefinedTerm/long-running-agent]] は、有限のコンテキスト、永続的な状態の欠如、自己検証の欠如をまとめて、通常のエージェント設計が数時間から数日にわたって機能しなくなる障害として挙げている。

### 解決策としてのより大きなウィンドウ

複数のページが、ウィンドウを大きくしても問題はなくならないという立場を、それぞれ独自の根拠から記録している。[[DefinedTerm/context-rot]] と [[DefinedTerm/context-engineering]] は、あらゆるサイズのウィンドウがコンテキスト汚染と情報の関連性の問題にさらされ続けるという Anthropic の議論を載せている。[[ScholarlyArticle/externalization-in-llm-agents]] は「Lost in the Middle」の知見を引きつつ、ウィンドウを拡張しても根底にある緊張関係は解消しないと論じる。[[DefinedTerm/long-running-agent]] は、大きなウィンドウであってもいずれは埋まり、コンテキストロットはハードリミットに達する前に性能を劣化させると指摘する。[[BlogPosting/what-is-harness-engineering]] では、著者が、問題はタスクの組み立て方にあったのだから、より大きなウィンドウがあってもずれていくスライドデッキは直らなかっただろうと論じている。[[DefinedTerm/token-caching]] はコストの観点を加える。キャッシュミスのコストはコンテキスト長に比例して増えるため、トークン単価が同じであっても、非常に大きなウィンドウはタダではない。

## 何がウィンドウを埋めるのか

一群のページは、作業そのものに先立って、あるいはそれと並んでコンテキストを占めるものを扱っている。

- **常設の指示。** [[DefinedTerm/ai-ide-rules]] とその背後にある研究 [[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] は、リンターのほうが確実に強制できるフォーマットや構文に限られたコンテキストウィンドウを費やさないよう勧めており、またルールへの準拠がそのルールを導入したコミットの後に低下していくことを報告している。研究はこれを、コンテキストウィンドウの複雑さが増していくことに一部起因するとしている。[[SoftwareApplication/claude-code]] は、CLAUDE.md を簡潔に保つようにという Anthropic の助言を記録しており、肥大化したファイルは実際の指示が無視される原因になると警告している。
- **必要に応じて読み込まれる機能。** [[DefinedTerm/agent-skills]] は [[DefinedTerm/progressive-disclosure]] を説明している。スキルのメタデータは常に読み込まれ、本体はトリガーされたときに、同梱リソースは読まれたときにだけ読み込まれる。また、同梱スクリプトは実行され、その出力だけがコンテキストに入る。[[BlogPosting/what-is-harness-engineering]] は、著者が蓄積してきた各スキルが読み込まれたときにどれだけのコンテキストを占めるかを測定したことを報告している。これは作業が始まる前に消費されるコンテキストである。[[ScholarlyArticle/dive-into-claude-code]] は、Claude Code の拡張メカニズムをコンテキスト上のコストの順に並べている。
- **ツールとテストの出力。** [[BlogPosting/building-a-c-compiler-with-a-team-of-parallel-claudes]] は、テスト出力をコンテキストウィンドウの汚染を念頭に設計した。数行だけを出力して残りはファイルにログとして書き出し、各エラーとその理由を grep できるよう 1 行にまとめるというものである。

[[DefinedTerm/harness-engineering]] で紹介されている [[ScholarlyArticle/externalization-in-llm-agents]] は、この競合をハーネスレベルの調整問題として扱う。メモリ検索、スキルの読み込み、プロトコルのスキーマ、ツールの説明、そしてモデル自身の推論トレースは、いずれも同じ有限の割り当てから引き出されており、適切な配分は実行のフェーズによって異なる。

## セッション内で何がなされるのか

Anthropic の記事 [[BlogPosting/effective-context-engineering-for-ai-agents]] は、この制約への対応を 1 つの指導原則を軸に整理している。可能な限り小さな、高シグナルのトークンの集合を見つけるという原則であり、それをシステムプロンプト、ツール、例示に適用する。続いて検索に話を移し、[[DefinedTerm/just-in-time-context-retrieval]] への移行を説明したうえで、ウィンドウに収まらないタスクのための 3 つの手法、すなわち [[DefinedTerm/compaction]]、[[DefinedTerm/structured-note-taking]]、[[DefinedTerm/sub-agent-architecture]] を取り上げる。それぞれが異なるタスクの形に適している。

Lance Martin の [[BlogPosting/context-engineering-for-agents]] と LangChain の [[BlogPosting/langchain-context-engineering]] は、モデルを CPU、そのコンテキストウィンドウを RAM とみなす捉え方から出発し、よく使われているエージェントに見られる戦略を、書き込み（write）、選択（select）、圧縮（compress）、分離（isolate）の 4 つの区分にまとめている。LangChain の記事はさらに、各区分を自社の [[SoftwareApplication/langgraph]] の機能に対応づけており、そのページはこれをベンダーによるガイダンスとして明記している。

2 つのページが、1 つの本番エージェントにおけるコンテキストの扱いを異なる角度から説明している。[[SoftwareApplication/claude-code]] は文書化された挙動を記録している。古いツール出力がまず消去され、必要に応じて会話が要約されるというものであり、セッションの制御手段として `/clear` と `/compact` がある。[[ScholarlyArticle/dive-into-claude-code]] はソースコードを読み、コンテキストウィンドウを拘束力のあるリソース制約と特定している。それは、モデルを呼び出すたびにその前に実行される一連のシェイパーによって管理され、より安価な戦略では不十分だと判明したときにだけ段階的に強化される。

分離はそれ自体が独立した対応として繰り返し現れる。[[ScholarlyArticle/dive-into-claude-code]] は、サブエージェントが分離されたコンテキストウィンドウで動作し、親には要約テキストだけを返すことを説明している。[[BlogPosting/what-is-harness-engineering]] は、作業の各単位を、設計ルール一式を持たせた独立したエージェントに任せたことを報告しており、その結果として、エージェントの核となる価値は並列性ではなくコンテキストの分離にあるという著者の見解を述べている。

[[DefinedTerm/context-as-a-tool]] は別の道をとる。コンテキストの維持をエージェント自身の意思決定の中で呼び出せるツールにし、追記のみのコンテキストや受動的にトリガーされる圧縮に頼るのではなく、エージェントがマイルストーンで自らの履歴を圧縮するようにする。

## セッションをまたいで何がなされるのか

タスクが 1 つのウィンドウに収まる長さを超える場合、各ページは状態をウィンドウの外に移し、新たに始めることを説明している。

- [[DefinedTerm/long-running-agent]] は、新しいコンテキストウィンドウが何よりも必要とするのは作業の状態を素早く把握する手段であり、それは git の履歴と並ぶ進捗ファイルによって提供されるという Anthropic の説明を記録している。
- [[DefinedTerm/ralph-loop]] は、選択・実装・検証・コミットのサイクルを反復するたびにエージェントのコンテキストをリセットし、リセットをまたぐ状態をウィンドウではなくファイルシステム上に持ち越す。
- [[BlogPosting/building-a-c-compiler-with-a-team-of-parallel-claudes]] では、各エージェントをコンテキストを持たない新しいコンテナで開始させ、詳細な README と進捗ファイルを維持するようエージェントに指示した。
- [[DefinedTerm/externalization]] は、コンテキストウィンドウを履歴の唯一の担い手として扱うのではなく、メモリを時間をまたいで状態を外部化するものとして捉える。
- [[ScholarlyArticle/deepcode-open-agentic-coding]] は、自らの問題全体を有限のコンテキストウィンドウに対する情報過多として捉え、生成されたファイルについての状態を持つ要約ベースのメモリを、素朴なスライディングウィンドウ方式で古い内容を追い出すベースラインと比較している。このベースラインは、切り捨てによって基礎的な定義を失った。

## それぞれの説明はどこから来ているのか

この領域が記録していることの大半は、実践者が自らの実践を測定するのではなく説明したものである。[[DefinedTerm/context-engineering]] は、そこに集めた説明のいずれも独立した評価ではないと明記している。[[BlogPosting/effective-context-engineering-for-ai-agents]] は [[Organization/anthropic]] の Applied AI チームが自らのエンジニアリング経験に基づいて書いたものであり、ベンチマークの集合ではなくメンタルモデルとして自らを提示している。書き込み・選択・圧縮・分離を扱う 2 つの記事は、その区分をすでに使われているパターンのまとめとして提示している。[[BlogPosting/what-is-harness-engineering]] と [[BlogPosting/building-a-c-compiler-with-a-team-of-parallel-claudes]] は当事者による報告であり、[[DefinedTerm/ralph-loop]] について報告されている限界は、Geoffrey Huntley 自身がこの手法を用いた経験に由来する。

測定された結果はいくつかの箇所に現れるが、それぞれに固有の範囲がある。[[DefinedTerm/context-as-a-tool]] と [[ScholarlyArticle/deepcode-open-agentic-coding]] はそれぞれ単一の論文のベンチマーク結果を報告しており、[[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] はルールファイルについての混合研究法による研究である。[[ScholarlyArticle/externalization-in-llm-agents]] は測定結果ではなく統合的な論考であり、[[ScholarlyArticle/dive-into-claude-code]] はソースコードの 1 つの静的なスナップショットを読んだもので、自らの主張をエビデンスの段階ごとに格付けしている。

## 関連ページ

[[DefinedTerm/context-poisoning]]、[[DefinedTerm/context-confusion]]、[[DefinedTerm/tool-call-offloading]]、[[DefinedTerm/context-reset]]、[[DefinedTerm/initializer-agent]]、[[DefinedTerm/agent-harness]]
