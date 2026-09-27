---
title: "「バイブコーディング」とは何を意味するのか"
lang: ja
kind: debate
review_status: pending
translated_from: ".wikicommit/view/en/what-does-vibe-coding-mean.md"
source_commit: "e44ba09db16b5c1d0a761746f7f7dee556f49de4"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
---

「バイブコーディング（vibe coding）」は、この wiki で最もよく使われる語の 1 つだが、その意味について各ページの見解は一致していない。あるページは、この語を 1 つの狭い基準、すなわちソフトウェアを作る人がコードを読むかどうかに限定する。別のページは、レビューの有無にかかわらず、主にモデルとの対話によって作られたソフトウェアすべてにこの語を使う。3 つ目のグループは、この語を、いずれ別の実践に取って代わられる初期段階の名前として使う。このページでは、それらの答えと、それぞれを誰が示しているか、その背後に何があるかを整理する。どれが正しいかは決めない。ページ同士が食い違う箇所では、その食い違いこそがこのページの記録するものである。

## 造語の由来

この語の出どころについては、各ページの見解が一致している。[[DefinedTerm/vibe-coding]] は、2025 年 2 月初めにこの語を作ったのは Andrej Karpathy だとしている。Karpathy の説明は、バイブス（雰囲気）に完全に身を委ね、コードが存在することさえ忘れるというものだった。すべての差分を読まずに受け入れ、エラーメッセージを何のコメントも付けずにそのまま貼り付け、モデルが直せないバグは回避するか、消えるまで適当な変更を頼む。[[BlogPosting/two-publishers-and-three-authors-fail-to-understand-what-vibe-coding-means]] はそのツイートを全文引用している。同記事が強調するのは 2 つのフレーズ、「コードが存在することさえ忘れる（forget that the code even exists）」と「使い捨ての週末プロジェクトなら悪くない（It's not too bad for throwaway weekend projects）」である。[[SoftwareApplication/cursor]] は、Karpathy が説明した環境を記録している。Sonnet モデルで動く Cursor Composer に、タイプするのではなく音声で話しかけるというものだ。

ほかにもいくつかのページが、この語を Karpathy に帰している。

- [[ScholarlyArticle/vibe-coding-vs-agentic-coding]]
- [[ScholarlyArticle/vibe-coding-programming-through-conversation-with-artificial-intelligence]]（2025 年 2 月の彼の投稿を「Karpathy の正典（the Karpathy canon）」と呼んでいる）
- [[BlogPosting/ai-coding-tools-evolution-and-vibe-coding]]
- [[BlogPosting/predictable-vibe-coding-strategy-with-claude-code]]
- [[Book/vibe-vibe]]
- [[BlogPosting/lessons-from-releasing-a-product-with-ai-agents]]

[[BlogPosting/2025-output-retrospective]] は、ソフトウェアの書き方の転換を 2025 年 2 月に位置づけている。同記事は、その月のある 1 つの発表がバイブコーディングを話題の的にしたとし、その月を、人間が運転席から助手席へ移った月としてまとめている。

各ページは、語の由来については食い違っていない。食い違っているのは、この語が Karpathy の説明をどこまで引き継いでいるかである。

## 答え 1: バイブコーディングとはコードを読まないことである

最もはっきりと線を引いた答えは、Simon Willison によるものだ。[[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]] は、この語を 1 つの観察可能なテストに還元する。バイブコーディングとは、LLM が書いたコードをレビューせずに、LLM でソフトウェアを作ることである。LLM が書いたコードでも、その後レビューされ、テストされ、理解されたものはソフトウェア開発であり、LLM が関与したかどうかは問題にならない。[[DefinedTerm/ai-assisted-programming]] は、この狭い語が属する包括的なカテゴリーを示している。

Willison は、この狭い読み方をバイブコーディングへの攻撃ではなく、その擁護として提示している。

- コンピュータサイエンスの学位もブートキャンプの経験もない人々にとって、プログラミングへの高い障壁を下げる。
- 経験のある開発者にとって、LLM についての直感を養う最良の方法である。

[[BlogPosting/two-publishers-and-three-authors-fail-to-understand-what-vibe-coding-means]] で、彼はこの区別を「死んでも譲れない一線（a hill I am willing to die on）」と呼んでいる。さらに、バイブコーディングはソフトウェア開発者ではない人々のためのものであり、すでに開発者である人々のためのものではないと付け加えている。

Willison は 2026 年になっても同じ線を守っていた。

- [[BlogPosting/writing-about-agentic-engineering-patterns]] は、この語を元の定義、すなわちコードにまったく注意を払わないコーディングという意味のまま保っている。今日この語は非プログラマーと結びつけられることが多い、とも述べている。
- [[BlogPosting/vibe-coding-and-agentic-engineering-getting-closer]] は、これを、コードをまったく見ず、場合によってはプログラミングの仕方すら知らず、結果を動くかどうかだけで判断することだと説明している。

ほかのページも、同じ境界を採用するか言い換えている。

- **[[BlogPosting/ai-coding-tools-evolution-and-vibe-coding]]** は、Karpathy の投稿を 4 つの点として読む。コードが存在することを忘れること、小さなエラーでさえ AI を通じて直すこと、AI が書いたものをレビューしないこと、そしてそれが使い捨てのプロジェクトなら構わないと受け入れることである。バイブコーディングをめぐる議論の多くは、2 つの異なる実践を区別していないことから生じている、と同記事は論じている。
- **[[ScholarlyArticle/vibe-coding-practice-performance-productivity-and-risk-a-state-of-the-art-review]]** は、定義に Willison の境界を採用している。バイブコーディングを際立たせるのは、生成されたコードから開発者が離れていることであり、検証は出力が動くかどうかによって行われる。この境界に従えば、開発者がなおレビューとテストを行う対話型 IDE のワークフローは、本来の意味でのバイブコーディングからは外れる。
- **[[ScholarlyArticle/swe-chat-coding-agent-interactions-from-real-users-in-the-wild]]** は、狭い読み方を測定可能なものにしている。コミットされたコードの 99% 超をエージェントが書いたセッションをバイブコーディングとして数え、その割合が 3 か月の観察期間のうちに約 20% から 40% 超へと倍増したと報告している。
- **[[BlogPosting/humans-and-agents-in-software-engineering-loops]]** は、「ループの外にいる人間（humans outside the loop）」、つまり how のループをエージェントに任せることを、バイブコーディングの一般的な定義と呼んでいる。
- **[[DefinedTerm/vibe-coding]]** は、Andrew Connell の説明を記録している。バイブコーディングはコードの所有権を AI に委ねる。エージェント型エンジニアリングは、開発者のエンジニアリング上の判断を運転席に据えたままにする。
- **[[ScholarlyArticle/sdd-foundation-of-ai-native-enterprise-software-engineering]]** は、AI 支援型の実践の 2 つの原型の 1 つとして、バイブコーディングを仕様駆動開発と対置する。バイブコーディングでは、仕様はワーキングメモリと会話履歴に散らばった暗黙の意図としてしか存在せず、受け入れは振る舞いの観察的なサンプリングに帰着する。同論文は「統制されていない（ungoverned）」という語を、明示的な契約との照合ではなく振る舞いのサンプリングによって受け入れが決まる実践に限定しており、「AI 支援そのものに対してではない（not to AI assistance as such）」としている。

## 答え 2: バイブコーディングとは対話によってソフトウェアを作ることである

2 つ目のグループのページは、開発者が出力を読み、舵を取る作業も含めて、プロンプト主導の開発全般にこの語を使う。

- **[[ScholarlyArticle/vibe-coding-vs-agentic-coding]]** は、バイブコーディングを、開発者が生成された各部分をレビューし洗練させる能動的な共同制作者であり続ける、人間中心のモデルとして定義する。これを、自律的なエージェントが複数ステップのタスクを計画・実行する [[DefinedTerm/agentic-coding]] と対置している。[[DefinedTerm/vibe-coding]] は、この説明が Karpathy の「コードが存在することさえ忘れる」ではなく、通常のレビューを伴う AI 支援型プログラミングに近いと指摘している。
- **[[ScholarlyArticle/vibe-coding-programming-through-conversation-with-artificial-intelligence]]** は、バイブコーディングを、主にコード生成モデルとのやり取りを通じてコードを書くことと捉える。実践の意味がまだ定まっていなかったため、対象に含める唯一の基準は、プログラマー自身が自分の活動をバイブコーディングと表現していることだった。同研究が観察したコードレビューは、存在しないのではなく、素早く、印象に頼ったものだった。
- **[[ScholarlyArticle/building-software-by-rolling-the-dice]]** は、バイブコーディングを、主にプロンプトを通じてソフトウェアを作ることと定義する。この語が、自律エージェントへの全面的な委任から、手作業での編集や点検を伴うエージェント支援型のエンジニアリングまで、幅広い実践を包む傘になっていると指摘している。
- **[[ScholarlyArticle/a-survey-of-vibe-coding]]** は、これを、実装を「1 行ずつのコード理解ではなく結果の観察によって（through outcome observation rather than line-by-line code comprehension）」検証することと定義する。ところが同サーベイは、この語のもとに 5 つの開発モデルを分類しており、元の定義に最も近いと呼ぶのはそのうち 1 つだけである。[[DefinedTerm/vibe-coding-development-models]] は、その 1 つを Unconstrained Automation Model と名づけ、残りを挙げている。対話型の協働、計画駆動、テスト駆動、そしてそのいずれにも追加できるコンテキスト強化の層である。[[BlogPosting/a-survey-of-vibe-coding-with-llm]] は、このサーベイの枠組みを、意図を述べて品質を判断する人間、プロジェクト、コーディングエージェントの三者関係として紹介している。
- **[[ScholarlyArticle/vibe-coding-multivocal-literature-review]]** は、36 の文献がこの語をどう枠づけているかを数えている。

  | 枠組み | 文献数 | 割合 |
  |---|---|---|
  | 社会技術的な開発実践 | 25 | 69% |
  | 自然言語からコードへの開発、またはプロンプトベースの開発 | 24 | 67% |
  | エージェント型または半自律的な開発 | 18 | 50% |
  | コパイロットまたはペアプログラミング | 7 | 19% |

  同レビューは、バイブコーディングを、検証が取り除かれるのではなく別の場所へ移される反復的な制御システムとして読んでいる。
- **[[BlogPosting/the-uncomfortable-truth-about-vibe-coding]]** は、これを広く、すべての行を自分で書くのではなく AI と対話することによってソフトウェアを作ることと定義している。
- **[[BlogPosting/the-new-era-of-software-development-from-vibe-coding-to-agentic-engineering]]** は、欲しいものを説明し、AI が生成したコードを受け入れ、エラーメッセージが出ればそれをチャットに貼り付けて AI に直させることと定義している。
- **[[BlogPosting/predictable-vibe-coding-strategy-with-claude-code]]** は、Karpathy の意図的に極端な定義から出発するが、実際にはこの語はもっと広く使われていると述べる。同ガイドが扱うのは、LLM が生成を主導する一方で、開発者がコードを読むモードである。
- **[[BlogPosting/vibe-coding-best-practices-what-not-to-let-slide]]** は、この語から軽蔑的な意味合いを取り除いている。バイブコーディングを、仕様を定め、トレードオフを整理し、実行をモデルに委ね、結果を検証するサイクルとして扱っている。
- **[[BlogPosting/pj-double-mercari-development-productivity]]** は、バイブコーディングを、AI に段階的に指示を送り、その出力を見ながら軌道修正することと説明している。これは手放しの実践ではなく、同期的で対話的な実践である。
- **[[DefinedTerm/agent-spec-driven-development]]** は、メルカリの CTO が ASDD を「直感的な」バイブコーディングと対比していることを記録している。
- **[[ScholarlyArticle/mise-en-place-for-agentic-coding]]** は、バイブコーディングを支配的なワークフローパターンと呼ぶ。開発者が意図を述べ、エージェントがコードを生成し、食い違いは反復的な修正によって直される。
- **[[BlogPosting/spec-driven-development-with-ai-open-source-toolkit]]** は、これを、目標を説明すると、正しく見えるが完全には動かないことの多いコードが返ってくるものだと説明している。
- **[[ScholarlyArticle/context-before-code]]** は、本番志向の 2 つのシステムにおける「対話型（conversational）」のバイブコーディングを調査している。
- **[[ScholarlyArticle/vibe-coding-kills-open-source]]** は、AI エージェントがオープンソースのコンポーネントを選んで組み合わせることによってソフトウェアを作ることを、バイブコーディングとして出発点に置いている。その際、ユーザーはそれらのコンポーネントのメンテナーと関わらないことが多い。

いくつかの製品やチュートリアルも広い意味でこの語を使っており、中には肯定的に使うものもある。

- [[Book/vibe-vibe]] は、バイブコーディングを、プログラミングの素養がない学習者のための AI プログラミングとして扱い、「Coder から Commander へ（from Coder to Commander）」と言い表している。
- [[SoftwareApplication/vibesdk]] は、自らをオープンソースのバイブコーディングプラットフォームと称している。
- [[SoftwareApplication/vibecraft]] と [[BlogPosting/programming-for-those-who-dont-write-code-how-vibecraft-works]] は、チャット駆動のアプリビルダーを、汎用アシスタントを使ったバイブコーディングの限界への応答として提示している。
- [[BlogPosting/software-engineering-debunking-myths-welcoming-vibe-coding]] は、AI がソフトウェアエンジニアリングにもたらした新しいアプローチの 1 つとして、バイブコーディングを紹介している。
- [[BlogPosting/ralph-wiggum-as-a-software-engineer]] は、自らのループ手法を「完全に手放しのバイブコーディング（full hands-off vibe coding）」と呼んでいる。

## 2 つの答えが分かれるところ

### レビューは実践の一部か

ここで 2 つの答えは互いに排他的になる。Willison のテストでは、コードがレビューされる作業はどれもバイブコーディングではない。広い意味をとる 2 つの文献は、レビューを実践の内側に置いている。

- [[ScholarlyArticle/vibe-coding-vs-agentic-coding]] は、各部分のレビューを定義に組み込んでいる。
- [[ScholarlyArticle/vibe-coding-programming-through-conversation-with-artificial-intelligence]] は、分析したすべてのセッションで軽いレビューを観察した。

[[DefinedTerm/material-disengagement]] は、この食い違いの経験的な側面を述べている。調査されたセッションでは、プログラマーはなお差分に目を通し、直接編集やデバッグを行っていた。ただし、それは常態としてではなく選択的にだった。コードはマテリアル（素材）であることをやめてはいなかった。

[[ScholarlyArticle/building-software-by-rolling-the-dice]] は、実践者自身のあいだでの食い違いを報告している。厳密な定義を主張する人もいれば、バイブコーディングと従来のソフトウェアエンジニアリングのあいだに境界を設けること自体を拒む人もいた。

### 誰がそれを行うのか

Willison は、[[BlogPosting/two-publishers-and-three-authors-fail-to-understand-what-vibe-coding-means]] と [[BlogPosting/writing-about-agentic-engineering-patterns]] において、バイブコーディングをプロの開発者ではない人々と結びつけている。広い意味の側では、[[BlogPosting/programming-for-those-who-dont-write-code-how-vibecraft-works]] が技術的な素養のない人々向けの製品を作っている。[[Book/vibe-vibe]] はプログラミングの素養がない学習者を対象としているが、従来のプログラマーも想定読者に含まれている。

[[BlogPosting/the-vibesec-reckoning]] は、「市民ビルダー（citizen builder）」、すなわち AI を使ってものを作る非技術系のユーザーが作ったプロトタイプを取り上げている。[[TechArticle/model-ai-governance-framework-for-agentic-ai]] のガバナンスフレームワークは、エージェントを使ってバイブコーディングするユーザーには、コードの堅牢性をレビューするためのソフトウェアエンジニアリングの専門知識が欠けている可能性があると警告している。[[DefinedTerm/automation-bias]] は、同じケースを、自分が承認するものを判断する専門知識を持たない監督者の例として使っている。

経験的研究が見ているのは、別の母集団である。

- [[ScholarlyArticle/vibe-coding-programming-through-conversation-with-artificial-intelligence]] のコーパスには、非プログラマーが含まれていなかった。バイブコーディングにはプログラミングの専門知識が必要だという同研究の知見は、それを持つバイブコーダーについてのみ成り立つ。
- [[ScholarlyArticle/building-software-by-rolling-the-dice]] は、プロのプログラマーと、正式な訓練を受けていない人々の両方をバイブコーダーとして数えている。
- [[ScholarlyArticle/professional-software-developers-dont-vibe-they-control]] は、経験のある開発者はバイブコーディングをしないことを見いだしている。彼らは計画と監督を通じて、設計と実装の主導権を保っている。

### カテゴリーか段階か

いくつかのページは、この語を、維持すべきカテゴリーとしてではなく、移行の最初の段階として使っている。

- **[[BlogPosting/the-new-era-of-software-development-from-vibe-coding-to-agentic-engineering]]** は、これを、ほとんどの人が最初に通過するフェーズと呼んでいる。
- **[[DefinedTerm/vibe-coding]]** は、これをプログラミングパラダイムの発展における 1 つの段階として扱い、その段階はチーム規模では不安定だと論じるハンドブックの章を記録している。
- **[[BlogPosting/impact-of-ai-on-the-state-of-the-art-in-software-engineering-in-2026]]** は、2025 年初めにはバイブコーディングが主流だったが、今では人々はその代わりに [[DefinedTerm/context-driven-engineering]] やエージェント型エンジニアリングについて語っているとしている。
- **[[ScholarlyArticle/agentic-agile-v]]** は、未来を「大規模なバイブコーディングではなく（not vibe coding at scale）」検証されたエンジニアリングとして描いている。
- **[[ScholarlyArticle/spec-driven-development-for-agentic-software-engineering]]** は、バイブコーディングを 4 つのパラダイムの 1 つとして扱い、そこへの移行を、説明責任、検証、オンボーディングの点で後退的だと呼んでいる。
- **[[DefinedTerm/agentic-coding]]** は、エージェント型コーディングをバイブコーディングの代替ではなく、それを補完するものとして提示している。この説明では、バイブコーディングによる探索的なプロトタイピングが後のフェーズにつながっていく。
- **[[BlogPosting/sequoia-ascent-2026-summary]]** は、Karpathy 自身の 2026 年の枠組みを伝えている。バイブコーディングは底上げ（raises the floor）をもたらし、エージェント型エンジニアリングは天井を引き上げる（raises the ceiling）。

## バイブコーディングではないものに与えられた名前

語を狭く保つと、残りを指す語が必要になる。以下の各ページは、それぞれ異なる語を提案するか使用している。

| 名前 | この wiki での記録箇所 | バイブコーディングとの対置のされ方 |
|---|---|---|
| [[DefinedTerm/ai-assisted-programming]] | [[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]] | バイブコーディングを、レビューされない部分集合として含む包括的な実践 |
| [[DefinedTerm/vibe-engineering]] | [[BlogPosting/vibe-engineering]] | スペクトラムの反対側。プロフェッショナルが、自分の出荷するものについて「誇りと自信をもって責任を負う（proudly and confidently accountable）」状態にとどまる |
| [[DefinedTerm/agentic-engineering]] | [[BlogPosting/writing-about-agentic-engineering-patterns]]、[[BlogPosting/sequoia-ascent-2026-summary]]、[[BlogPosting/lessons-from-releasing-a-product-with-ai-agents]] | プロのエンジニアが、コーディングエージェントによって自らの専門性を増幅すること |
| [[DefinedTerm/context-coding]] | [[BlogPosting/ai-coding-tools-evolution-and-vibe-coding]] | Karpathy の狭い意味とは区別される、AI 支援型プログラミング全般 |
| AI 支援型エンジニアリング（AI-assisted engineering） | [[BlogPosting/good-spec]] | 仕様、テスト、レビューを必要とする作業。探索や使い捨てプロジェクトのためのバイブコーディングと対置される |
| [[DefinedTerm/context-driven-engineering]] | [[BlogPosting/impact-of-ai-on-the-state-of-the-art-in-software-engineering-in-2026]] | プロンプトの代わりに、意図と制約からなる完全なコンテキストを与えること |
| [[DefinedTerm/spec-driven-development]] | [[BlogPosting/from-vibe-coding-to-spec-driven-development]]、[[BlogPosting/spec-driven-development-with-ai-open-source-toolkit]]、[[ScholarlyArticle/sdd-foundation-of-ai-native-enterprise-software-engineering]] | 構造化された仕様を信頼できる唯一の情報源（source of truth）とすること |
| [[DefinedTerm/mise-en-place-methodology]] | [[ScholarlyArticle/mise-en-place-for-agentic-coding]] | スペクトラムの反対側。アラインメントの作業を前もって行う |
| ヒューマン・オン・ザ・ループ（Humans on the loop） | [[BlogPosting/humans-and-agents-in-software-engineering-loops]] | ループの外にとどまることと、すべての行を点検することのあいだにある第 3 の立場 |

名前同士も互いに競合している。[[DefinedTerm/vibe-engineering]] は、同じ考えについては「エージェント型エンジニアリング（agentic engineering）」が優勢になりつつあるようだ、という Willison の 2026 年 2 月の追記を記録している。[[DefinedTerm/agentic-engineering]] は、この語が「バイブコーディング」が 2 つの異なる活動を覆ってしまうのを止めるために提案されたこと、そして「バイブエンジニアリング」をめぐる数か月の議論の後に登場したことを述べている。

[[BlogPosting/what-is-spec-driven-development-practitioners-guide]] は、各手法が真実をどこに置くかによって、関連する線を引いている。バイブコーディングでは、それは最後のプロンプトである。TDD ではユニットテスト、BDD では振る舞いの例、仕様駆動開発では承認された仕様である。

## 狭い線は保たれているか

狭い陣営のページ自身が、その立場が劣勢になっていることを報告している。

- **[[DefinedTerm/semantic-diffusion]]** は、Willison が 2025 年 3 月に、Martin Fowler のこの用語をバイブコーディングの受け止められ方に当てはめたことを記録している。この語の定義は、広まるにつれて弱まっていた。
- **[[BlogPosting/two-publishers-and-three-authors-fail-to-understand-what-vibe-coding-means]]** は、この語をプロの仕事に使った 2 冊の本をきっかけとしている。[[Book/vibe-coding-building-production-grade-software]] と、後に改題された [[Book/beyond-vibe-coding]] である。同記事は、この議論にはおそらく負けたと認めている。
- **Karpathy の返答**は、[[DefinedTerm/vibe-coding]] と [[DefinedTerm/semantic-diffusion]] が記録するところによれば、定義が落ち着くには時間がかかるというものだった。彼は、自分自身が全面的なバイブコーディングをすることはめったにない、とも付け加えた。

2026 年までには、この侵食は反対側からも見えるようになっている。

- [[BlogPosting/vibe-coding-and-agentic-engineering-getting-closer]] は、Willison が本番の作業も含めて、エージェントの書く行をもはやすべてはレビューしていないことを報告している。彼は自分の実践の中で 2 つのカテゴリーの境界がぼやけつつあると述べ、そのリスクを逸脱の常態化（normalization of deviance）と名指している。
- [[BlogPosting/humans-and-agents-in-software-engineering-loops]] は、仕様駆動開発のいくつかの解釈は、バイブコーディングとほとんど変わらないと述べている。
- [[DefinedTerm/spec-driven-development]] は、バイブコーディングのソリューションではないと説明されながら、人間のチェックポイントなしに単一のプロンプトから実行するとバイブコーディングのように振る舞う、ある仕様駆動のプラグインを記録している。
- [[ScholarlyArticle/from-prompt-to-process]] は、エビデンスの裏づけがなければ、エージェント向けのプロセスフレームワークは、用語を増やしただけでバイブコーディングを制度化するにとどまるおそれがあると警告している。

## それぞれの答えが適するとする場面

どちらの読み方でも、各ページはおおむねバイブコーディングの居場所を、プロトタイプ、個人用ツール、使い捨ての作業に置いている。違うのは、何がそれを排除するかである。

**レビューの欠如。** 狭い陣営の反論は、誰もコードを読まないという点にある。

- [[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]] は、その条件として、リスクが低いこと、秘密情報と個人データに注意を払うこと、他のサービスにかける負荷、そして課金に厳格な上限を設けることを挙げている。
- [[SoftwareApplication/claude-artifacts]] は、同記事が挙げる、読まれていないコードが到達できる範囲を制限するサンドボックスの例である。
- [[SoftwareApplication/cursor]] は、同記事が挙げる、安全柵がはるかに少ないツールの例である。
- [[BlogPosting/vibe-coding-and-agentic-engineering-getting-closer]] は、バイブコーディングを、バグが自分だけを傷つける個人用ツールにはすばらしいが、他人のためのソフトウェアを作る場合にはひどく無責任だとしている。

**構造的な限界。** 広い意味を使うページは、別の点を指摘している。

- **仕様の欠如。** [[BlogPosting/the-uncomfortable-truth-about-vibe-coding]] は、バイブコーディングで作られたプロジェクトが 3 か月ほどで壁にぶつかると報告し、その原因を仕様なしに作ることに求めている。同記事のルールは、ユニットテストや機能テストで出力を検証できるなら、その範囲はバイブでやってよいほど小さい、というものだ。
- **アーキテクチャ。** [[ScholarlyArticle/context-before-code]] は、バイブコーディングがスキャフォールディングには信頼できるが、テナント分離、アクセス制御、非同期処理については、それらを明示しない限り信頼できないことを見いだした。[[DefinedTerm/non-delegation-zone]] は、そうした領域を名指している。
- **チームへのスケーリング。** [[ScholarlyArticle/spec-driven-development-for-agentic-software-engineering]] は、5 つの限界を挙げている。再現不可能性、監査不可能性、移転不可能性、レビューの飽和、ノイズのスケーリングである。
- **実践の共有。** [[BlogPosting/pj-double-mercari-development-productivity]] は、バイブコーディングの同期的な性質のせいで、各開発者の判断がチャットログの中に取り残され、透明性も再利用性もないままになると指摘している。

ほかのページは、具体的なコストを挙げている。

- [[DefinedTerm/trust-debt]]（[[BlogPosting/stop-vibe-coding-embrace-new-software-engineering]] による）
- [[DefinedTerm/fast-integration-debt]]
- [[DefinedTerm/context-momentum]]
- [[DefinedTerm/rolling-the-dice]]
- [[DefinedTerm/review-bottleneck]]
- [[BlogPosting/the-vibesec-reckoning]] のセキュリティインシデント。これが [[DefinedTerm/security-context-file]] につながった
- [[HowTo/ai-assisted-code-review-with-antigravity-cli-and-sdk]] のセキュリティレビューの前提
- [[ScholarlyArticle/vibe-coding-kills-open-source]] がモデル化した、オープンソースのメンテナーへの影響

実践者も、自分の仕事から同じ限界を述べている。

- [[BlogPosting/making-ai-do-t-wada-style-tdd]] は、放置されたバイブコーディングが使いものにならない出力をしばしば生むことを見いだしている。
- [[BlogPosting/keep-agentic-ai-simple]] は、長期的に予想される問題を理由に、バイブコーディングを見送っている。
- [[BlogPosting/2025-ai-coding-trends-agent-10x-productivity-amplification]] は、AI が既存の習慣を増幅する様子が最もはっきり現れるのはバイブコーディングだと見ている。
- [[BlogPosting/organizing-a-development-team-in-the-age-of-ai-part-iii]] は、統制の甘いバイブコーディングを、保守の難しい「AI スロップ（AI slop）」と結びつけている。
- [[BlogPosting/acp-protocol-and-multiple-ai-coding-agents]] は、人が自分のコードに責任を持ち続けるエンタープライズの仕事を、バイブコーディングのデモと対比している。
- [[BlogPosting/taming-agents-in-the-mercari-web-monorepo]]（[[DefinedTerm/agents-md]] で再述）は、プロジェクトがバイブコーディングで書かれた CSS には頼れないと述べている。
- [[ScholarlyArticle/sdd-in-software-development-pbl]] は、アプリケーション開発を教える授業には、バイブコーディングより仕様駆動開発のほうが適していると判断している。
- [[BlogPosting/new-sdlc-vibe-coding]] は、境界線を AI の利用そのものではなく、検証に置いている。

両陣営のいくつかのページは、肯定的な論拠も示している。

- [[ScholarlyArticle/sdd-foundation-of-ai-native-enterprise-software-engineering]] は、アイデア出し、プロトタイピング、学習、アクセシビリティにおいて、バイブコーディングを正当なものと認めている。
- [[DefinedTerm/vibe-coding]] は、バイブコーディングによって非エンジニアがプロトタイプを自然言語で表現できる、という Connell の主張を記録している。

## それぞれの答えの裏づけ

狭い答えは、測定ではなく議論に基づいている。[[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]] は明確に定義をめぐる記事であり、Karpathy の文言と著者自身の実践を根拠として挙げている。

広い答えは主に経験的研究やサーベイの文献が使うものであり、その文献はまだ新しい。

- **配信されたセッションの研究。** [[ScholarlyArticle/vibe-coding-programming-through-conversation-with-artificial-intelligence]] は、プログラマー自身がそう表現した場合にのみセッションをバイブコーディングとして数えたので、測っているのは固定された定義ではなく、人々がこの語をどう使っているかである。[[ScholarlyArticle/building-software-by-rolling-the-dice]] は、自らを、何をバイブコーディングとみなすべきかの定義ではなく、スナップショットだとしている。
- **文献レビュー。** [[ScholarlyArticle/vibe-coding-multivocal-literature-review]] は、自らのコーパスを、初期段階の提案中心のものであり、その 40% がグレー文献だと説明している。[[ScholarlyArticle/a-survey-of-vibe-coding]] は、この実践についての経験的研究には縦断的な検証が欠けていると指摘している。
- **新しく、争いのある用語。** [[ScholarlyArticle/sdd-foundation-of-ai-native-enterprise-software-engineering]] と [[ScholarlyArticle/spec-driven-development-for-agentic-software-engineering]] はどちらも、自らの中心的な用語を、新しい、あるいは争いのあるものと呼んでいる。

定量的な知見は、いずれもまず定義を採用し、それに照らして測定している。

- [[ScholarlyArticle/swe-chat-coding-agent-interactions-from-real-users-in-the-wild]] は、99% のしきい値を使っている。
- [[ScholarlyArticle/vibe-coding-practice-performance-productivity-and-risk-a-state-of-the-art-review]] は、Willison の境界を使っている。

したがって、あるページの数値は、そのページ版のこの語を測ったものであり、ほかのページが使うこの語を測ったものではない。
