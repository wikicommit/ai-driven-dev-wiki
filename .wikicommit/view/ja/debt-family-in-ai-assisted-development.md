---
title: "AI 支援開発における負債のファミリー"
lang: ja
kind: pattern
review_status: pending
translated_from: ".wikicommit/view/en/debt-family-in-ai-assisted-development.md"
source_commit: "2bc91f0f7b78294f861e552d41d5dd2a701e039f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
---

この wiki の 8 つのページは、AI 支援開発やエージェント型のソフトウェア開発において蓄積するとされる一種の「負債」に名前を付けている。[[DefinedTerm/verification-debt]]、[[DefinedTerm/cognitive-debt]]、[[DefinedTerm/comprehension-debt]]、[[DefinedTerm/trust-debt]]、[[DefinedTerm/governance-debt]]、[[DefinedTerm/prompt-debt]]、[[DefinedTerm/fast-integration-debt]]、[[DefinedTerm/provenance-debt]] である。このうち 4 つは 1 本の多声的文献レビュー（multivocal literature review）である [[ScholarlyArticle/faster-code-deeper-debt]] に由来する。残りの 4 つは、Koch による統合論文、Addy Osmani の講演と記事、学部生のソフトウェア工学プロジェクトの研究、そしてある著者のコラムの初回に由来する。このページでは、8 つに繰り返し現れる形と、それらが食い違うところを説明する。用語に順位をつけることはせず、どれかについてどの名前が正しいかを決めることもしない。

## 8 つのケース

| 用語 | wiki のどこに記録されているか | 何が蓄積するとされるか | 誰の帳簿に載るか |
|---|---|---|---|
| [[DefinedTerm/verification-debt]] | Koch、[[ScholarlyArticle/agentic-agile-v]] | 弱いテスト、隠れた回帰、広範なパッチ、検証されていない依存関係、文書化されていない振る舞い、レビュアーの負担増 | チームの未検証の出力とレビュー負荷 |
| [[DefinedTerm/cognitive-debt]] | Osmani の基調講演「Own the Outer Loop」、並列エージェントに関する別の記事、[[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] | 問題をどう解くかについてのエンジニア自身の理解の侵食 | 個々のエンジニア |
| [[DefinedTerm/comprehension-debt]] | [[ScholarlyArticle/comprehension-debt-in-genai-assisted-software-engineering-projects]] | チームがコードベースについて知っていることと、それを保守するために理解している必要があることとのギャップ | チームの集合的な認知（コードではないと明示されている） |
| [[DefinedTerm/trust-debt]] | [[BlogPosting/stop-vibe-coding-embrace-new-software-engineering]] | 信頼に値することを誰かが確かめられるより速く出荷されるコード | コードについて誰も確かめていないこと |
| [[DefinedTerm/governance-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | ハルシネーションと非決定性によって生じる、取り込まれた LLM 出力に対する継続的な監督の負担 | マージで終わらない監督 |
| [[DefinedTerm/prompt-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | 再現性とコード品質を低下させる、不明瞭で影響を受けやすい、あるいは文書化されていないプロンプト | コードを形作るのにコードのようには管理されないプロンプト |
| [[DefinedTerm/fast-integration-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | 適切な検証なしに統合された LLM 出力 | 採用の速さと評価の速さのギャップ |
| [[DefinedTerm/provenance-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | 生成されたコードの不明確な所有権や帰属表示の欠如 | 欠けている記録（法的な問題や説明責任の問題として表面化する） |

同じレビューは、さらに 2 つの新たなカテゴリとしてデータの負債（data debt）と倫理的負債（ethical debt）を挙げている。どちらもこの wiki に独自のページがないため、8 つには数えていない。

## 繰り返し現れる形

### 一方の速度が他方を上回る

8 つのうち 4 つのページは、仕組みを速度の不一致として記述しており、生成や採用の側が速い側にある。

- [[DefinedTerm/verification-debt]] — 出力量が検証能力より速く増えると、チームはこれを蓄積する。
- [[DefinedTerm/trust-debt]] — エージェントが生成するコードの速さが、そのコードが信頼に値することを確かめる能力を上回る。生成がボトルネックでなくなると、人間の注意力とレビューの帯域幅が制約となる。
- [[DefinedTerm/fast-integration-debt]] — 問題は、LLM の出力を採用できる速さと、開発者がその下流への影響を評価できる速さとのギャップから生じる。
- [[DefinedTerm/cognitive-debt]] — 並列エージェントに関する記事では、人が理解できるより速くエージェントに生成させると負債が蓄積し、それがスレッドをまたいで複利的に膨らむ。[[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] は同じ非対称性を逆転として述べている。ジュニアエンジニアが、シニアエンジニアが批判的に監査できるより速くコードを生成できるようになったというのである。

残りの 4 つは、2 つの速度の競争としては捉えられていない。[[DefinedTerm/comprehension-debt]] は、ギャップの原因を AI ツールが認知負荷を下げることに求めている。その結果、作業をする中で築かれたはずの理解が築かれない。[[DefinedTerm/governance-debt]] はモデルの性質、すなわちハルシネーションと非決定性に基づいており、これらによって監督は一度きりのコストではなく継続的なものになる。[[DefinedTerm/prompt-debt]] は 2 種類の成果物の扱われ方の不一致を名指しし、[[DefinedTerm/provenance-debt]] はコードがどこから来たかの記録の欠如を名指ししている。

### 通常の技術的負債との対比による定義

根拠となるページのうち 4 つは、用語を部分的に従来の技術的負債との違いによって定義しており、それぞれが異なる場所に線を引いている。

- [[DefinedTerm/comprehension-debt]] — コードベースではなく、チームの集合的な認知の中に存在する。
- [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] — 技術的負債は積み重なる摩擦を通じて自らの存在を知らせ、通常は場所のわかった意識的なトレードオフである。これに対して理解の負債は、コードがきれいに見え、テストがグリーンであるために、誤った自信を生む。
- [[DefinedTerm/fast-integration-debt]] — 問題は特定の成果物の品質からではなく、採用と評価のギャップから生じる。
- [[DefinedTerm/provenance-debt]] — コードの負債は保守の摩擦として表面化するが、これは法的な問題や説明責任の問題として表面化する。

[[DefinedTerm/governance-debt]] は別の線を引いている。取り込まれた出力に対する監督の負担に範囲を限定し、従来の技術的負債からではなく、AI・ML システムにおける技術的負債に関する既存の文献から意図的に切り離している。

### 後になって現れるコスト

根拠となる 4 つのページ（8 つの用語ページのうち 3 つと Osmani の記事）は、コードが取り込まれた時点ではコストが見えないことを強調している。

- [[DefinedTerm/fast-integration-debt]] — ある実務者の報告では、スプリント中はベロシティの指標が非常に良く見えていたが、バグ報告は数週間後に、AI が考慮していなかったエッジケースで届いた。
- [[DefinedTerm/governance-debt]] — その決定的な特徴は、負担がマージで終わらないことである。
- [[DefinedTerm/provenance-debt]] — コストは、あるロジックについて誰が責任を負うのか、あるいはどのような条件で配布してよいのかを誰かが確定する必要が生じる時点まで先送りされる。
- [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] — 清算の時が来るまで、コードベースはきれいに見え、テストはグリーンである。

### 測定されていないと明言されている

8 つのうち 4 つのページは、自らが名指す負債が測定されていないことを明言している。

- [[DefinedTerm/verification-debt]] — Koch はこれを直接測定する方法を示しておらず、証拠バンドルでこれを減らせるかどうかを未解決の問いとして挙げている。
- [[DefinedTerm/trust-debt]] — 1 人の著者による捉え方であり、負債の測定も、それを観察する方法も示されていない。
- [[DefinedTerm/fast-integration-debt]] — グレー文献から帰納的に特定されたもので、測定ではなく実務者の報告に依拠している。
- [[DefinedTerm/governance-debt]] — 測定されたものではなく、実務者の情報源から帰納的に導かれたものである。

[[ScholarlyArticle/faster-code-deeper-debt]] は一般的な状況を述べている。調査した 2 つの文献群のいずれにも、LLM が生成したコードの技術的負債を評価するための標準化されたベンチマークやデータセットは含まれていなかった。[[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] は実務の観点から関連する主張をしている。ベロシティの指標、DORA メトリクス、PR の数、カバレッジがすべて健全に見える一方で、理解の不足は見えないままでありうるというのである。

残りのページは、負債そのものの測定には触れずに、別の種類の証拠を報告している。[[DefinedTerm/cognitive-debt]] は、AI を介して作業したエンジニアが理解度クイズで 50% の得点だったのに対し、そうでないエンジニアは 67% だったというランダム化試験を引用している。[[DefinedTerm/comprehension-debt]] は、学部生のプロジェクトで観察された 4 つの蓄積パターンを記述している。[[DefinedTerm/prompt-debt]] は、よく構造化された具体的なプロンプトが、観察されたコードスメルの最大 87.1% を緩和したという研究を報告している。そして [[DefinedTerm/provenance-debt]] は、レビューの 104 の情報源のうち、1 つのフォーマルな情報源と 1 つのグレーな情報源に依拠している。

## ケースが食い違うところ

### 「理解の負債」と呼ばれる 2 つの概念

同じ名前が 2 つの異なる概念に付けられている。Osmani の用法、すなわち存在するコードの量と、そのうち人間が理解している量とのギャップは、[[DefinedTerm/cognitive-debt]] に記録されている。彼の基調講演はこれを認知的負債と呼び、並列エージェントに関する記事は同じ力学を理解の負債（comprehension debt）と呼び、[[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] もこれに「理解の負債」（comprehension debt）という語を用いている。[[DefinedTerm/comprehension-debt]] は、学部生のプロジェクトの論文で提案された用語であり、チームの集合的な知識がコードベースの保守に必要なものに届かないことを指す。前者はエージェントに委任するエンジニアを中心に捉えられ、後者は生成 AI ツールを採用するチームを中心に捉えられている。[[DefinedTerm/comprehension-debt]] は [[DefinedTerm/cognitive-debt]] を関連用語として挙げており、どちらのページも両者を 1 つの概念としては扱っていない。

### 負債がどこに抱えられるか

8 つは、負債が誰の帳簿に載るかについて異なる。[[DefinedTerm/cognitive-debt]] はそれを 1 人のエンジニアに置き、[[DefinedTerm/comprehension-debt]] はチームに置く。[[DefinedTerm/verification-debt]] は出力とレビュー負荷に、[[DefinedTerm/prompt-debt]] はコードに適用される管理の下にない入力に、[[DefinedTerm/provenance-debt]] は存在しない記録に置く。[[DefinedTerm/trust-debt]] はコードについて誰も確かめていないことに置き、[[DefinedTerm/governance-debt]] はコードがマージされた後も続く監督に置く。

### 用語の裏付けの強さ

[[ScholarlyArticle/faster-code-deeper-debt]] に由来する 4 つの用語には情報源の数が付いており、その数は大きく異なる。[[DefinedTerm/governance-debt]] は 19 のグレーな情報源に現れ、フォーマルな情報源には現れない。[[DefinedTerm/fast-integration-debt]] は 13 のグレーな情報源に現れ、フォーマルな情報源には現れない。[[DefinedTerm/prompt-debt]] は 8 つのフォーマルな情報源と 5 つのグレーな情報源に現れ、フォーマルな文献における LLM 特有の負債の主要な源泉と報告されている。[[DefinedTerm/provenance-debt]] は 1 つのフォーマルな情報源と 1 つのグレーな情報源に現れる。残りの 4 つの用語は、いずれも 1 人の著者または 1 つの研究による捉え方に依拠している。[[DefinedTerm/verification-debt]] は統合論文、[[DefinedTerm/cognitive-debt]] は基調講演と記事、[[DefinedTerm/comprehension-debt]] は学部生のプロジェクトの研究、[[DefinedTerm/trust-debt]] はコラムの初回である。

### 1 つの因果関係

根拠となるページで用語間の因果関係が述べられているのは 1 つだけである。[[ScholarlyArticle/faster-code-deeper-debt]] はドミノ効果を記述しており、そこでは高速統合の慣行が、管理されないまま放置されると連鎖的なガバナンス上のリスクを引き起こす。[[DefinedTerm/fast-integration-debt]] と [[DefinedTerm/governance-debt]] が伝えるところでは、高速統合によって監督を要するコードが増え、それがガバナンスの負債となり、さらに長期的な保守コストの増大につながる。他のページは、自らの用語を近隣の用語と関連概念としてしか関係づけていない。たとえば [[DefinedTerm/trust-debt]] は、[[DefinedTerm/verification-debt]] を未検証の出力に伴うすぐ隣のコストとして挙げているが、因果の順序は述べていない。

### 各情報源が対応として提案するもの

各用語に付けられた対応策は、それぞれが負債をどこに置くかに応じて、種類が異なる。

- [[DefinedTerm/fast-integration-debt]] — ヒューマン・イン・ザ・ループのモデル。レビューの 73 のグレーな情報源のうち 58 で推奨されており、LLM の出力をレビューと改良を要する下書きとして扱う。
- [[DefinedTerm/governance-debt]] — 継続的な開発者の研修、コードベースへの AI の関与の文書化、長期的な保守性の優先。これにコード品質ツールと多層的なレビューが加わる。
- [[DefinedTerm/verification-debt]] — [[DefinedTerm/agentic-agile-v]] のリスク適応型ゲートと証拠バンドルによる、リスクに見合った証拠に基づく受け入れ、そしてテストをエージェントのループの内側に保つこと。
- [[DefinedTerm/comprehension-debt]] — コードの変更ではなく実践。検証の実践、構造化された振り返り、能動的な学習評価である。
- [[DefinedTerm/prompt-debt]] — プロンプトを永続的なものにすること。テンプレート、構造化されたプロンプト、プロンプトのレジストリ、バージョン管理された文書化である。
- [[DefinedTerm/provenance-debt]] — コードがどこから来たかを問う来歴レビュー。これにガバナンスのチェックとプロンプトの文書化が加わる。
- [[DefinedTerm/trust-debt]] — 信頼エンジニアリング。AI 時代のための 3 次元の部品表（bill of materials）が、コラムの後の回の主題として挙げられている。
- [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] — 代替手段はない。この記事は、テストも仕様もそれぞれ理解の代わりとしては上限があり、理解する作業こそが仕事であると論じている。

## 関連ページ

[[DefinedTerm/review-bottleneck]]、[[DefinedTerm/skill-atrophy]]、[[DefinedTerm/automation-bias]]、[[DefinedTerm/cognitive-surrender]]、[[DefinedTerm/orchestration-tax]]、[[DefinedTerm/vibe-coding]]
