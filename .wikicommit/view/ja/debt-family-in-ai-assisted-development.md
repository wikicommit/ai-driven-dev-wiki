---
title: "AI 支援開発における負債のファミリー"
lang: ja
kind: pattern
review_status: pending
translated_from: .wikicommit/view/en/debt-family-in-ai-assisted-development.md
source_commit: 38743a24bda452cb3da45094b203774325b8d615
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
---

この wiki の 8 つのページは、AI 支援開発やエージェント型開発が蓄積するとされる一種の「負債」に名前を付けている。[[DefinedTerm/verification-debt]]、[[DefinedTerm/cognitive-debt]]、[[DefinedTerm/comprehension-debt]]、[[DefinedTerm/trust-debt]]、[[DefinedTerm/governance-debt]]、[[DefinedTerm/prompt-debt]]、[[DefinedTerm/fast-integration-debt]]、[[DefinedTerm/provenance-debt]] である。これらは少なくとも 6 つの別々の枠組みに由来する。Koch の統合論文、Addy Osmani の基調講演と彼の記事、並列エージェントに関する別の記事、学部生のソフトウェア工学プロジェクトの研究、エージェント型ソフトウェアエンジニアリングに関するコラム、そして 8 つのうち 4 つを命名している 1 本の多声的文献レビュー(multivocal literature review)である。このページでは、これらに繰り返し現れるものと、食い違うところを説明する。順位づけはせず、どれかについてどの名前が正しいかも決めない。

## 8 つのケース

| 用語 | 命名したソース | 蓄積するとされるもの | 負債の所在 |
|---|---|---|---|
| [[DefinedTerm/verification-debt]] | Koch、[[ScholarlyArticle/agentic-agile-v]] | 弱いテスト、隠れた退行、広範なパッチ、検証されていない依存関係、文書化されていない振る舞い、レビュアーの負担 | 検証されていない出力とチームのレビュー負荷 |
| [[DefinedTerm/cognitive-debt]] | Osmani の基調講演「Own the Outer Loop」。並列エージェントに関する別の記事では「理解の負債(comprehension debt)」と呼ばれる | 問題の解き方についてのエンジニア自身の理解の侵食 | 個々のエンジニア |
| [[DefinedTerm/comprehension-debt]] | [[ScholarlyArticle/comprehension-debt-in-genai-assisted-software-engineering-projects]] | チームがコードベースについて知っていることと、理解する必要があることとのギャップ | チームの集合的な認知。コードの中ではないと明言されている |
| [[DefinedTerm/trust-debt]] | [[BlogPosting/stop-vibe-coding-embrace-new-software-engineering]] | 信頼してよいと誰かが確認できるよりも速く出荷されたコード | コードについて誰も確認していないこと |
| [[DefinedTerm/governance-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | ハルシネーションと非決定性によって生じる、取り込んだ LLM 出力に対する継続的な監督の負担 | マージで終わらない監督 |
| [[DefinedTerm/prompt-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | 再現性を下げる、不明瞭・敏感・文書化されていないプロンプト | コードを形作るのにコードのようには管理されていないプロンプト |
| [[DefinedTerm/fast-integration-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | 適切な検証なしに採用された LLM 出力 | 採用の速さと評価の速さのギャップ |
| [[DefinedTerm/provenance-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | 生成されたコードの不明確な所有権や帰属の欠如 | 欠けている記録。法的な問題や説明責任の問題として表面化する |

同じレビューは 6 つの新しいカテゴリの中にデータ負債と倫理的負債も挙げているが、どちらもこの wiki に独自のページがないため、ここでは数えていない。

## 繰り返し現れるもの

### メカニズムとしての速度の不一致

8 つのうち 4 つのページは、ある速度が別の速度を上回ることをメカニズムとして述べており、速い側は生成である。

- [[DefinedTerm/verification-debt]]:チームは「出力量が検証能力より速く増える場合」にこれを蓄積する。
- [[DefinedTerm/trust-debt]]:エージェントが生成するコードの速さが、それが信頼に値すると確認する能力を上回る。生成がボトルネックでなくなると、人間の注意とレビューの帯域が制約となる。
- [[DefinedTerm/fast-integration-debt]]:問題は、LLM の出力を採用できる速さと、開発者がその下流への影響を評価できる速さとのギャップに由来する。
- [[DefinedTerm/cognitive-debt]]:並列エージェントの枠組みでは、人が理解できるより速くエージェントに生成させると、スレッドをまたいで複利的に増える負債が蓄積する。[[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] も同じ速度の非対称性を述べている。今やジュニアエンジニアは、シニアエンジニアが批判的に監査できるより速くコードを生成できる。

残りの 4 つはそのような形では捉えられていない。[[DefinedTerm/comprehension-debt]] は、AI ツールが認知負荷を下げるため、作業をしながら築かれたはずの理解が築かれないことにギャップの原因を求めている。[[DefinedTerm/governance-debt]] は、ハルシネーションと非決定性というモデルの性質に基づいており、それによって監督は一度きりのコストではなく継続的なものになる。[[DefinedTerm/prompt-debt]] は 2 種類の成果物の扱いの不一致に、[[DefinedTerm/provenance-debt]] はコードの出所の記録の欠如に名前を付けている。

### 通常の技術的負債との対比

いくつかのページは、従来の技術的負債と何が違うかによって自らの用語を定義しており、その境界線を引く場所はそれぞれ異なる。

- [[DefinedTerm/comprehension-debt]]:コードベースではなくチームの集合的な認知の中に存在する点で異なる。
- [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]]:技術的負債は増していく摩擦によって存在を知らせ、たいていは場所のわかっている意識的なトレードオフだが、理解の負債は誤った自信を生む — コードはきれいに見え、テストは緑である。
- [[DefinedTerm/fast-integration-debt]]:問題は特定の成果物の品質ではなく、採用と評価のギャップに由来する。
- [[DefinedTerm/provenance-debt]]:保守上の摩擦として表面化するコードの負債と違い、法的な問題や説明責任の問題として表面化する。
- [[DefinedTerm/governance-debt]]:取り込んだ出力の監督負担に範囲を絞っており、AI/ML システムにおける技術的負債に関する既存の研究とは意図的に区別されている。

### 測定されていないと明言されている

8 つのうち 4 つのページは、自らが名付ける負債が測定されていないことをはっきり述べている。

- [[DefinedTerm/verification-debt]]:Koch はそれを直接測定する方法を示しておらず、エビデンスバンドルでそれを減らせるかどうかを未解決の問いとして挙げている。
- [[DefinedTerm/trust-debt]]:一著者の捉え方であり、負債の測定もそれを観察する方法もない。
- [[DefinedTerm/fast-integration-debt]]:測定ではなく実務者の報告に基づき、グレー文献から帰納的に特定されたものである。
- [[DefinedTerm/governance-debt]]:測定されたものではなく、実務者のソースから帰納的に導かれたものである。

8 つのうち 4 つを命名している [[ScholarlyArticle/faster-code-deeper-debt]] は、これを一般的な形で述べている。調査したいずれの文献にも、LLM が生成したコードの技術的負債を評価するための標準化されたベンチマークやデータセットはなかった。[[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] は実践の側から関連する主張をしている。ベロシティ指標、DORA 指標、PR 数、カバレッジがすべて健全に見えても、不足は見えないままでありうる。

その他のページは、負債の測定には触れずに、別の種類のエビデンスを報告している。[[DefinedTerm/cognitive-debt]] は、AI を介して作業したエンジニアが理解度クイズで低い点を取ったランダム化試験(50% 対 67%)を引いている。[[DefinedTerm/comprehension-debt]] は、学部生のソフトウェア工学プロジェクトで観察された 4 つの蓄積パターンを説明している。[[DefinedTerm/prompt-debt]] は、ある研究でよく構造化されたプロンプトが観察されたコードスメルの最大 87.1% を軽減したと報告している。[[DefinedTerm/provenance-debt]] は、レビューの 104 件のソースのうち、フォーマルなもの 1 件とグレーなもの 1 件に基づいている。

## ケース間で食い違うところ

### 「理解の負債」と呼ばれる 2 つのもの

この wiki では、この名前が 2 つの異なる概念に使われている。Osmani の用法 — 存在するコードの量と、そのうち人間の誰かが理解している量とのギャップ — は [[DefinedTerm/cognitive-debt]] に記録されている。彼の基調講演はこれを認知的負債と呼び、並列エージェントに関する別の記事は同じ力学を理解の負債(comprehension debt)と呼び、Osmani は [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] でこれに「comprehension debt」を使っている。[[DefinedTerm/comprehension-debt]] は学部生プロジェクトの論文で提案された用語であり、チームの集合的な知識が、コードベースの保守に必要なものに届かない状態を指す。前者はエージェントに委任するエンジニアを軸に、後者は生成 AI ツールを導入するチームを軸に捉えられている。[[DefinedTerm/comprehension-debt]] は [[DefinedTerm/cognitive-debt]] を関連用語として挙げており、どちらのページも両者を 1 つの概念として扱ってはいない。

### 負債を抱えるのは誰か

ケースは、負債が誰の帳簿に載るかで分かれる。[[DefinedTerm/cognitive-debt]] はそれを個々のエンジニアに、[[DefinedTerm/comprehension-debt]] はチームに置く。[[DefinedTerm/verification-debt]] は成果物とレビュー負荷に、[[DefinedTerm/prompt-debt]] はコードに適用される管理の対象になっていない入力に、[[DefinedTerm/provenance-debt]] は存在しない記録に置く。[[DefinedTerm/governance-debt]] はそれを将来に置く。その決定的な特徴は、負担がマージで終わらないことである。

### ある負債が別の負債を引き起こす

根拠となるページで述べられている用語間の因果関係は 1 つだけである。[[ScholarlyArticle/faster-code-deeper-debt]] は、高速統合の慣行が、管理されないまま放置されるとガバナンス上のリスクを連鎖的に引き起こすドミノ効果を説明している。[[DefinedTerm/fast-integration-debt]] と [[DefinedTerm/governance-debt]] が伝えるレビューの説明によれば、高速統合は監督を要するコードを増やし、それがガバナンスの負債となり、さらに長期的な保守コストの増大につながる。他のページは自らの用語と近隣の用語を関連概念として結びつけている。たとえば [[DefinedTerm/trust-debt]] は、因果の順序を述べることなく、[[DefinedTerm/verification-debt]] を「検証されていない出力のすぐ隣にあるコスト」として挙げている。

### 各ソースが提案する対応

ソースが自らの用語に結びつける対応は、それぞれが負債をどこに置くかに従って、種類からして異なる。

- 生成された出力を下書きとしてレビューする — レビューの 73 件のグレーソースのうち 58 件が推奨するヒューマン・イン・ザ・ループのモデル。[[DefinedTerm/fast-integration-debt]] に対して。
- リスクに見合ったエビデンス — Koch のリスク適応型ゲートとエビデンスバンドル。[[DefinedTerm/verification-debt]] に対して。
- コードの変更ではなくチームの実践 — 検証の実践、構造化された振り返り、能動的な学習評価。[[DefinedTerm/comprehension-debt]] に対して。
- プロンプトを永続的なものにする — テンプレート、レジストリ、バージョン管理されたドキュメント。[[DefinedTerm/prompt-debt]] に対して。
- コードの出所を問う — 来歴のレビュー。[[DefinedTerm/provenance-debt]] に対して。
- 信頼エンジニアリング — コラムの後の回のテーマとして挙げられている三次元の部品表(BOM)。[[DefinedTerm/trust-debt]] に対して。

## 関連ページ

[[DefinedTerm/review-bottleneck]]、[[DefinedTerm/the-70-percent-problem]]、[[DefinedTerm/skill-atrophy]]、[[DefinedTerm/automation-bias]]、[[DefinedTerm/cognitive-surrender]]
