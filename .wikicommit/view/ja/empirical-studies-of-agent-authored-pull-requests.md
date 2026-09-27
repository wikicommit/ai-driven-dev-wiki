---
title: "エージェントが作成したプルリクエストの実証研究"
lang: ja
kind: comparison
translated_from: ".wikicommit/view/en/empirical-studies-of-agent-authored-pull-requests.md"
source_commit: "38743a24bda452cb3da45094b203774325b8d615"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending
---

このウィキにある 6 つの研究は、GitHub 上で AI コーディングエージェントが作成したプルリクエスト、すなわち [[DefinedTerm/agentic-pull-request]] を取り上げ、それがどうなったのかを問うている。マージされたのか、誰がレビューしたのか、コードをどのように変更したのか、そしてエージェントの導入がリポジトリに何をもたらしたのか、である。7 つ目の研究も同種の問いを立てているが、このウィキ上のページでは数値を報告していない。7 つの研究はいずれも [[Dataset/aidev]] という 1 つのデータセットに依拠しているが、その切り出し方も、何を結果（アウトカム）として数えるかも、記録に残らない空白をどう読むかもそれぞれ異なる。本ページはそうした違いが見えるように研究を並べて示すものであり、研究を順位付けしたり、数値を統合したりはしない。

## 共通の土台

[[ScholarlyArticle/aidev]]（MSR '26）は AIDev を、72,189 人の開発者による 116,211 リポジトリの 932,791 件のエージェント作成プルリクエストとして紹介している。作成したのは 5 つのエージェント、[[SoftwareApplication/openai-codex]]、[[SoftwareApplication/devin]]、[[SoftwareApplication/github-copilot]]、[[SoftwareApplication/cursor]]、[[SoftwareApplication/claude-code]] であり、カットオフは 2025 年 8 月 1 日である。スター数が 100 を超える 2,807 リポジトリの 33,596 件のプルリクエストからなるキュレーション済みサブセットには、全体セットにはないレビューコメント、コミットの差分、Issue へのリンク、イベントのタイムラインが含まれる。この論文はデータセットを記述し、採用、コードパッチの特性、テスト、レビューの力学、失敗パターンに関するリサーチクエスチョンを提案しているが、それらに答えてはいない。以下の研究は、事実上、そうした問いの一部への回答である。

## 研究の比較

| 研究 | 発表先 | AIDev のどの部分か | 問い | 手法 |
|---|---|---|---|---|
| [[ScholarlyArticle/where-do-ai-coding-agents-fail]] | MSR 2026（ショートペーパー） | キュレーション済み PR 33,596 件すべて。却下 PR 600 件を手作業でコーディング | どの PR 特性がマージを予測するか、エージェント型 PR はなぜ却下されるか | Cliff's delta、ロジスティック回帰、4 階層の却下分類法 |
| [[ScholarlyArticle/why-are-agentic-pull-requests-merged-or-rejected]] | MSR '26 | スター数 500 以上のリポジトリのクローズ済み PR 11,048 件を、人間のコメントがある 9,799 件に絞り込み。うち 717 件を手作業で検査 | マージ・却下のラベルはエージェントの能力を反映しているか | PR ごとに 2 名のアノテーターがインタラクションの痕跡をコーディング |
| [[ScholarlyArticle/how-ai-coding-agents-modify-code]] | MSR '26 | MSR 2026 Mining Challenge 版のマージ済みエージェント型 PR 24,014 件と人間の PR 5,081 件 | エージェント型 PR と人間の PR は構造がどう異なり、説明文は差分とどの程度一致するか | Mann–Whitney U 検定、Cliff's delta、語彙的類似度と埋め込み類似度 |
| [[ScholarlyArticle/these-arent-the-reviews-youre-looking-for]] | EASE 2026（ショートペーパー） | スター数 100 以上のリポジトリにおけるエージェント作成 PR と人間作成 PR を、同じリポジトリ内で比較 | 人間はエージェント作成 PR をどのようにレビューしているか | レビューコメントのルールベース分類器（検証サンプルで精度 96.5%） |
| [[ScholarlyArticle/from-industry-claims-to-empirical-reality]] | MSR '26 | 実際のコードレビューエージェントがレビューした PR 3,109 件。うち 2,456 件が Commented レビュー条件 | レビュアーの構成はマージ結果と関係するか | カイ二乗検定、キーワードベースの [[DefinedTerm/signal-to-noise-ratio]] |
| [[ScholarlyArticle/ai-ides-or-autonomous-agents]] | MSR '26 | AIDev v3。2024 年 1 月から 2025 年 11 月までの PR を再解析。エージェント先行 401 リポジトリと IDE 先行 117 リポジトリ、およびマッチングした対照群 | コーディングエージェントの導入はリポジトリの開発速度と品質に何をもたらすか | 傾向スコアマッチングを伴うスタッガード型差分の差分法、SonarQube の指標 |
| [[ScholarlyArticle/how-do-ai-coding-agents-contribute-to-software-development]] | arXiv（2607.21832） | AIDev | エージェント型 PR と人間の PR のマージ率、タスク種別、PR 特性が開発の四半期を通じてどう変化するか | 縦断的比較 |

## 違いのあるところ

### 何を結果（アウトカム）とみなすか

3 つの研究はマージの判断を説明すべき対象として扱うが、その扱い方は同じではない。4 つ目はマージ済み PR だけを見ている。

- [[ScholarlyArticle/where-do-ai-coding-agents-fail]] はマージされたか否かを結果とし、何がそれを予測するかを問う。キュレーション済みの 33,596 件の PR 全体で 71.48% がマージされたと報告し、失敗した CI チェックが 1 つ増えるごとにマージのオッズが約 15% 低下することを見出している。これは同研究が測定した中で単一要因として最大の効果である。
- [[ScholarlyArticle/why-are-agentic-pull-requests-merged-or-rejected]] は、その結果がそもそもエージェントの能力を測っているのかを疑問視する。検査した却下 PR 353 件のうち、35.7% に観察可能なエージェント側の失敗が見られ、31.2% は重複や別の変更で置き換えられたといったワークフロー上の理由でクローズされ、33.1% は分類できなかった。マージされた PR 364 件のうち、明示的なレビュアーの関与があったのは 15.4% である。著者らは、結果ベースの指標はエージェントの能力とリポジトリのワークフローを混同していると論じている。
- [[ScholarlyArticle/from-industry-claims-to-empirical-reality]] はマージを別の変数、すなわち誰が PR をレビューしたかの結果として用い、コードレビューエージェントのみがレビューした PR のマージ率 45.20% に対し、人間のみがレビューした PR では 68.37% だったと報告している。著者らは、カイ二乗検定の結果が示すのは関連であって因果ではないと述べている。
- [[ScholarlyArticle/how-ai-coding-agents-modify-code]] は結果をモデル化しない。マージ済み PR だけを残して、その構造を比較している。

[[ScholarlyArticle/ai-ides-or-autonomous-agents]] は分析単位をプルリクエストからリポジトリ・月へ移している。その結果変数は、最初のエージェント生成 PR の後に、リポジトリのコミット数、追加行数、静的解析の警告、認知的複雑度がどう推移するかである。

### 記録上の沈黙をどう読むか

人間のコメントが記録されないままクローズまたはマージされたプルリクエストは 3 つの研究に登場し、それぞれ扱いが異なる。

- [[ScholarlyArticle/where-do-ai-coding-agents-fail]] は、意味のある人間のやり取りなしにクローズされた PR を「レビュアーによる放棄」として却下パターンに数えており、これは同研究の分類法で最も多いパターンである（228 件、コーディングしたサンプルの 38%）。
- [[ScholarlyArticle/why-are-agentic-pull-requests-merged-or-rejected]] は、沈黙のままのクローズを原因ではなく「不明」カテゴリに置き、評価はその不確実性を明示的に表すべきだと論じている。また、サンプリングの前に人間のコメントがない PR を除外している。
- [[ScholarlyArticle/these-arent-the-reviews-youre-looking-for]] はコメントのない PR をすべて未レビューに分類する一方、メンテナーが痕跡を残さずに PR を確認することもありうるため、これは監督の不在を立証するものではないと述べている。そのうえで、エージェント作成 PR 33,596 件の 61.38% に記録されたレビューがなかったと報告している。

### エージェントと人間の比較

3 つの研究がエージェント作成 PR を人間作成 PR と比較しており、それぞれ異なる性質を比べている。

- [[ScholarlyArticle/how-ai-coding-agents-modify-code]] はコードの構造を比較する。エージェント型 PR は、より少ないファイルとコミットにわたって、より小さく局所的な編集を行い、差が最も大きいのはコミット数である（Cliff's δ = 0.5429）。その説明文は、4 つの類似度指標のすべてで、人間の PR よりもわずかに差分とよく一致している。
- [[ScholarlyArticle/these-arent-the-reviews-youre-looking-for]] はレビューを比較する。同じリポジトリ内では、観察可能な人間の関与はほぼ同じ（エージェント作成 PR で 30.1%、人間作成 PR で 30.8%）だが、その形が異なる。[[DefinedTerm/agent-steering]] は、エージェント作成 PR に対する人間のコメントの 25.92% を占めるのに対し、人間作成 PR では 1.63% である。
- [[ScholarlyArticle/how-do-ai-coding-agents-contribute-to-software-development]] は、マージ率、タスク種別、PR 特性を開発の四半期ごとに比較する。このウィキにある同論文のページは問いと研究設計を記録しているが、数値は記録していない。

### エージェント同士の比較

研究が結果をエージェント別に分けている箇所では、5 つのエージェントは同じようには振る舞っていない。

- [[ScholarlyArticle/where-do-ai-coding-agents-fail]] は、OpenAI Codex の 82.59% から GitHub Copilot の 43.04% までのマージ率を報告しており、Cursor、Claude Code、Devin はその間に位置する。
- [[ScholarlyArticle/why-are-agentic-pull-requests-merged-or-rejected]] は、サンプル中でフィードバックループまたは人間の介入を要したマージ済み PR 56 件のうち 54 件を Copilot と Devin が占める一方、Codex と Cursor の PR は通常、最小限のやり取りでマージされていたことを見出している。同研究はこれを、より厳格な CI ゲートなど、それらのエージェントが使われているリポジトリの性質にも一部帰しており、観察された結果はエージェントそのものと同じくらい導入の文脈を反映しているとする。
- [[ScholarlyArticle/how-ai-coding-agents-modify-code]] は、Claude Code と Codex は変更規模のばらつきが大きく、Devin、Cursor、そしてとりわけ Copilot は一貫して小さく局所的な変更を行うと報告している。

### 却下の原因

却下 PR を手作業でコーディングした 2 つの研究は異なる分類体系を用いているため、数値を 1 対 1 で突き合わせて読むことはできない。

- [[ScholarlyArticle/where-do-ai-coding-agents-fail]] は Reviewer、Pull Request、Code、Agentic の 4 階層を用い、エージェント階層の原因が最も少ないことを見出している（13 件、2%）。これは、エージェントがレビュアーの指示を繰り返し無視したり、コントリビューションポリシーに違反したりするケースである。レビュアーによる放棄に次いで大きいパターンは、重複 PR（23%）と CI/テストの失敗（17%）である。
- [[ScholarlyArticle/why-are-agentic-pull-requests-merged-or-rejected]] は却下 PR に対して、エージェント側の失敗、エージェント以外の失敗、不明の 3 カテゴリを用い、チェックやテストの失敗をエージェント側の失敗のシグナルとして数えている。

したがって、CI の失敗は一方の体系では Code 階層に位置し、もう一方ではエージェント側の失敗として数えられる。

### 開発速度と品質

[[ScholarlyArticle/ai-ides-or-autonomous-agents]] は、ここに挙げた中で、リポジトリに時間とともに何が起こるかを測定している唯一の研究であり、リポジトリを過去の AI ツール利用で分けている。エージェントが観察可能な最初の AI ツールだった場合、導入後にコミット数は平均 36.3%、追加行数は平均 76.6% 増加した。AI IDE が先行していた場合、効果は短命で、後にマイナスに転じた。静的解析の警告（約 +18%）と認知的複雑度（約 +39%）は両グループで上昇した。著者らは、この蓄積していく複雑さを「エージェント起因の複雑性負債（agent-induced complexity debt）」と呼んでいる。

## 各研究はデータセットのラベルをどう扱ったか

いくつかの研究は AIDev のラベルをそのまま受け取らず、それぞれ異なる点を修正している。

- [[ScholarlyArticle/these-arent-the-reviews-youre-looking-for]] は、人間作成とラベル付けされていたが実際にはエージェントが作成していた PR 1,044 件を除外し、アカウント種別が誤って記録されていたレビューコメントを修正した。
- [[ScholarlyArticle/from-industry-claims-to-empirical-reality]] は、`Bot` アカウントを手作業で分類しなければならなかった。この種別はコードレビューエージェントだけでなく CI/CD ランナーも含むためである。
- [[ScholarlyArticle/ai-ides-or-autonomous-agents]] は、ブランチ名のプレフィックス、作成者のログイン名、コミットの作成者、共同作成者の文字列から PR をエージェントに再帰属させ、それによって元のデータセットにおける誤分類や欠落した PR が見つかったと報告している。
- [[ScholarlyArticle/how-ai-coding-agents-modify-code]] は、使用したバージョンに人間の PR のコミット単位のデータがなかったため、GitHub REST API を通じてそれらのコミットと差分を再構築した。

## 共通する限界

各研究は自らの限界を述べており、その多くは重なっている。

- 知見はオープンソースの GitHub リポジトリと、AIDev が対象とする 5 つのエージェントに限られる。
- いくつかの研究は、さらにスター数の閾値を超えるリポジトリに対象を限定している。
- 記録されたやり取りは、判断の背後にある理由づけと同じではない。

[[Dataset/aidev]] は、データセットそのものについて同じ境界を記している。そこから導かれた知見は、プロプライエタリなリポジトリ、他のプラットフォーム、他のエージェント、あるいはカットオフ以降の活動には自動的には拡張されない。
