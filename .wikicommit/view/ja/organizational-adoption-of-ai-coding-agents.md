---
title: "AI コーディングエージェントの組織的な導入"
lang: ja
kind: practice
translated_from: ".wikicommit/view/en/organizational-adoption-of-ai-coding-agents.md"
source_commit: "287c3c8dd1a323646ab8734f4e9947e53060f58f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending
---

本ページは、AI コーディングエージェントを、一部の個人がうまく使いこなすものではなく、エンジニアリング組織全体の働き方の一部にしようとする組織の試みについて、このウィキが記録していることを並べて示す。当事者による記述は、[[Organization/cyberagent]]、[[Organization/mercari]]、[[Organization/zozo]]、[[Organization/zalando]]、[[Organization/github]]、[[Organization/microsoft]]、[[Organization/dmm]]、そして Toss によるものである。その周りには、別の種類の研究や報告がある。ランダム化比較試験を中心に据えた GitHub と Accenture の研究、Microsoft 自身の展開に関するテレメトリ研究、ある企業の「2 倍」の [[DefinedTerm/ai-mandate]] に関する縦断的事例研究、実務者へのアンケート調査、そして Google のサーベイに基づく [[DefinedTerm/dora-ai-capabilities-model]] である。当事者による記述の大半は組織が自らについて書いたものであり、それぞれをどこまで一般化できるかには限りがある。最後の節では、各記述をその背後にある証拠の種類で分類する。

## 各記述の出発点となる問題

いくつかの記述は同じ出発点を描いており、それは利用の広がりの不足ではない。ZOZO では、全社的なプログラムのもとで開発 AI エージェントがすべてのエンジニアに提供されている。難しさとして語られているのはばらつきである。ツールをうまく使ったエンジニアは生産性を高めたが、その知見は個人の実践の中にとどまり、利用が広がっても組織の最低水準はなかなか上がらなかった。同じ懸念はチームレベルでも述べられている。各チームが作った資産はそのチームの中にとどまり、チーム間の差を広げた（[[Organization/zozo]]）。基幹システム部門の記事は、プロンプト、レビュー基準、どこまで任せるかという各自の感覚が人によってばらばらになり、上限は上がったが下限はそのままだったと記述している（[[BlogPosting/ai-driven-development-two-commands]]）。

特定の企業の記述を離れると、あるエンジニアの記事は、同じばらつきをコーディング能力の差ではなくツールを制御するノウハウの差と捉え、それを個人の適性に任せることを組織が負う損失と呼んでいる。そしてその対応を [[DefinedTerm/raising-the-floor]] と名付けている（[[BlogPosting/raising-productivity-floor-with-harness]]）。

メルカリの記述は、同じ話をいくつかの角度から語っている。2025 年初頭、AI ツールと MCP サーバーは、同社が「Divergence（発散）」フェーズと呼ぶ時期にボトムアップで導入された。一部の開発者は劇的に生産性を高め、AI をうまく使える人と使えない人の間に差が開き、共有される実践はローカルなコツや共有ルールファイルのレベルにとどまった（[[Organization/mercari]]）。pj-double はこれを [[DefinedTerm/vibe-coding]] の同期的・対話的な性質に帰している。状況に応じた判断は各開発者のチャットログの中にとどまってしまう（[[BlogPosting/pj-double-mercari-development-productivity]]）。CTO の記事は、プロンプトの質のばらつき、コンテキスト収集の難しさ、コード品質のばらつき、さまざまなツールの乱立を挙げる。そしてこの 4 つすべてを、AI の使い方に関する共通の規範がないことに帰している（[[BlogPosting/choosing-ai-native-mercari-guiding-principles]]）。

他の記述は、成果のばらつきではなく、浸透のばらつきから出発している。Toss では、プロダクト、デザイン、スタッフ職の人々がそれぞれの領域で AI の使い方を模索していたが、一部のメンバーはまだ AI を遠いものと感じており、非開発職の人々は不安を募らせていた（[[BlogPosting/toss-ai-surf-day]]）。サイバーエージェントのナレッジ共有に関する記事は、全社的な投資とリスキリングによって個人には共通のスタートラインが与えられたが、多くのチームはまだ手探りの状態だったと記述している（[[BlogPosting/ai-knowledge-sharing-sessions-96-products]]）。あるサイバーエージェントのエンジニアは、そもそもツールを広めることの障害を記述している。連結で 8,000 人を超える従業員を抱える会社で、チームごとに Slack ワークスペースが分かれ、技術選定も独立しており、トップダウンで「明日から全員このツールを使う」ということがめったに起きないボトムアップの文化がある（[[BlogPosting/ai-code-agents-matsuri-seven-techniques]]）。

2 つの出典は一般的な状況を枠づけている。GitHub のプレイブックは、企業が AI ツールに投資しても、利用が少数の初期の熱心な人々にとどまるのを目にするだけだと述べる。その記述によれば、企業が失敗するのは、導入が変革マネジメントの問題であるのに技術の問題として扱うからである（[[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]）。実務者へのアンケート調査は、組織がトレーニング、ポリシー、目標よりもツールへのアクセスを配ることの方がはるかに得意であることを見出している。所属組織が生成 AI の利用を支援していると回答した人のうち、支援の形としてツールへのアクセスを挙げたのは 81.06% であるのに対し、トレーニングは 45.47%、公開されたポリシーは 41.08%、生成 AI の利用に結びついた目標や KPI は 19.08% だった（[[ScholarlyArticle/generative-ai-adoption-in-software-engineering]]）。

## 導入がどう広がると報告されているか

最初の利用がどう広がるかを測定しているのは 1 つの記述だけである。Microsoft のテレメトリ研究は、Copilot CLI の導入が大部分において社会的なものであることを見出した。スキップレベルの同僚の多くが使っていたエンジニアは、それを試すオッズが 216% 高かった。直属のマネージャーが使っていることは、試すオッズが 82% 高いこと、そして使い続けるオッズが 22% 高いことと関連していた。多忙なエンジニアほど試しやすく使い続けやすい一方、キャリアの段階や在籍年数はほとんど関係がなかった。著者らは、この研究設計では同僚の影響と同類性（homophily）を切り分けられないと述べている（[[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]]）。

他の記述は、人から人へ実践を運ぶための意図的な経路を記述している。それぞれ対象とする人が異なる。

- **自発的なアドボケイト。** GitHub のプレイブックは、ボランティアを募るだけで AI アドボケイトを集める。彼らは身近な専門家として働き、ユースケースを紹介し、チームの意見を吸い上げ、トレーニングの共同運営を手伝う。これを「Train the Trainer」アプローチで支える（[[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]）。
- **推薦されたエバンジェリスト。** Toss は同僚からの推薦によって 142 人のエバンジェリストを選んだ。この仕組みは、技術的に最も使いこなしている人ではなく、チームに AI を広めることに最も熱心な人を選んだ。組織のために AI をうまく使うことはチームのワークフローを再設計することだ、という考えによる（[[BlogPosting/toss-ai-surf-day]]）。
- **プロダクトごとのキーパーソン。** サイバーエージェントのナレッジ共有会は、すべてのエンジニアに薄く届けるのではなく、推薦されたプロダクトのテックリードなど、チームで AI 活用をリードできる人を対象とした。6 か月間で 96 のプロダクトのキーパーソンが参加した（[[BlogPosting/ai-knowledge-sharing-sessions-96-products]]）。
- **外からの注目。** サイバーエージェントの AI Driven 推進室のメンバーは、社内での講演やデモへの反応が乏しかったため、外部イベント [[Event/ai-code-agents-matsuri-2025-winter]] を企画した。外からの情報の方が社内の組織の壁を越えるという考えである。記事によれば、執筆時点で、著者が 2024 年 9 月に 1 人で始めた社内の Cursor チャンネルは 500 人を超えるメンバーを抱え、会社全体では職種を問わず約 1,000 人の Cursor アクティブユーザーがいた（[[BlogPosting/ai-code-agents-matsuri-seven-techniques]]）。
- **定例の場。** Zalando は、毎週のナレッジ共有会を持つ LLM ギルド、テーマ別のハッカソン、約 20 人規模のオンサイトの GenAI Labs、そして以前の Lab 参加者からトレーナーを募る月例トレーニングを記述している（[[Organization/zalando]]）。Toss は 4 月から 6 月まで毎週金曜日を AI の試行に充て、プログラム開始とともに約 200 の社員運営のクラブが作られた（[[BlogPosting/toss-ai-surf-day]]）。Microsoft は社内で「Agentic Engineering Day」を開催した（[[Organization/microsoft]]）。GitHub は、1 つの AI チャンネルではなく、それぞれに憲章と指名されたリーダーを持つ別個の実践コミュニティを推奨している（[[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]）。

## 各記述が行っていること

### ツールの選択：自由にしておくか、収束させるか

各記述が最も目に見えて異なるのは、ツールそのものを標準化するかどうかである。Zalando は単一のコーディングツールを中央から義務付けたことは一度もない。200 を超えるチームがエコシステムを探索している中で、標準化するにはまだあまりに早すぎると述べ、ベンダー非依存を重要な点と位置付けている（[[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]）。メルカリのある記事も同じ姿勢を記述しており、誰もが自分で選んだツールを導入できるようになっていた。一方でそのコストも報告している。それらのツールの有効性と成果は、同じチーム内でさえ大きくばらついた（[[Organization/mercari]]）。CTO の記事は、同じ発散を会社レベルから記述している。まず Cursor が全社展開され、その後エンジニアが Claude Code などの新しいアシスタントに移ったため、ベストプラクティスを集約しにくくなった（[[BlogPosting/choosing-ai-native-mercari-guiding-principles]]）。ZOZO のプログラムは幅広いツールを対象としており（[[Organization/zozo]]）、サイバーエージェントは Claude Code と Codex をエンタープライズプランで導入し、Cursor を検討中だった（[[BlogPosting/ai-code-agents-matsuri-seven-techniques]]）。

単一のツールへ向かっているのは Microsoft の記述だけである。同社のエンジニアには 2026 年初頭の時点で、認可されたコマンドラインエージェントが 2 つあった。2026 年 4 月 29 日の直後、社内告知により、ほとんどのエンジニアについて Claude Code のライセンスを打ち切り、Copilot CLI を使うよう指示することが示された（[[Organization/microsoft]]）。同社の研究では、単一ツールの利用者の間で、Copilot CLI を使った週にはマージされたプルリクエストが +24.9% 増加したのに対し、Claude Code では +11.4% だった。著者らは、タスク構成の違いと Microsoft が GitHub を所有していることを仮説として挙げている（[[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]]）。

### 標準ツールではなく標準プロセス

標準化を行う記述では、いくつかがツールから独立したプロセスを標準化している。メルカリの pj-double は、3 か月間にわたって 30 を超えるバックエンドプロジェクトと協働し、2025 年 9 月に [[DefinedTerm/agent-spec-driven-development]]（ASDD）を提案した。この手法は、最も成果を上げている開発者に共通する 3 つの実践を制度化することを目的としていた。AI に一次情報を最初に与えること、目的・手順・完了条件を明示すること、AI の作業コンテキストを簡潔に保つことである。10 月からプロジェクトは全社に拡大した（[[BlogPosting/pj-double-mercari-development-productivity]]）。CTO の記事は ASDD を開発プロセスの中核と位置付け、その品質は Agent Spec を書く際に与えられるコンテキストに依存することを強調している（[[BlogPosting/choosing-ai-native-mercari-guiding-principles]]）。

ZOZO の基幹システム部門は、Claude Code と Codex を組み合わせた 2 つの標準コマンド、`/dev-init` と `/dev-resume` を作った。ユーザーが触れる面はこの 2 つのコマンドに固定したまま、その背後にあるプロンプト、スキル、レビュー基準、連携を更新していくので、エンジニアがインターフェースを学び直すことなく、組織として新しい実践へ移行できる。著者は各チームが独自のワークフローを作ることに反対しており、記事によればそれは局所的な自律性を高めるが、組織の下限には手を付けないままにするからである（[[BlogPosting/ai-driven-development-two-commands]]）。サイバーエージェントの共有会は、AI が計画を下書きし、人間がそれをレビューし、AI が修正して実行し、人間が結果を確認するという中核的な流れを教えた。その第 4 回では、プロジェクト単位の AI 駆動開発への 9 ステップの移行が紹介された（[[BlogPosting/ai-knowledge-sharing-sessions-96-products]]）。

### チーム間で共有される資産

いくつかの記述は、他のチームがインストールできるように作業方法をパッケージ化している。ZOZO は 2025 年後半から、チームをまたいで単一の [[DefinedTerm/claude-code-plugin-marketplace]] を運用している。約 10 か月後、チーム間での具体的な再利用と、新メンバーの立ち上がりの短縮を報告している（[[Organization/zozo]]）。Zalando は、プラグインにまとめられた [[DefinedTerm/agent-skills]] の中央集約的なコレクションを維持しており、その中では移行（マイグレーション）用のスキルが広く人気のある種類である（[[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]）。メルカリでは、チームごとに Devin Organization を分離したことでノウハウの共有が難しくなり、社内の Terraform プロバイダーで Devin Knowledge を管理できるようにしたことで、チーム間で配布できるようになった（[[BlogPosting/enabling-ai-usage-at-mercari-with-secure-devin-management]]）。このアプローチの論拠を最も詳しく述べているのは [[BlogPosting/raising-productivity-floor-with-harness]] である。そこでは、1 つのスラッシュコマンドが優れたエンジニアのワークフロー全体を運び、誰が実行しても同じ品質になるようにしており、プラグインの知識は全社、ドメイン、リポジトリの層に分けて重ねられている。著者はこれを成果ではなく方向性として、そして大部分は仮説として示している。

### ポリシー、ガバナンス、プラットフォーム

GitHub は、IT、人事、セキュリティ、法務と共同で策定する利用規定を前提条件として扱う。審査済みリストにないツールは公開のものとして扱う段階的なモデルを推奨している（[[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]）。DORA は、部門横断のワーキンググループによるリスクベースのポリシーを推奨する。そのポリシーは用途を、禁止、ガードレール付きで許可、許可の 3 つに分類し、随時更新される文書として公開される（[[Report/dora-ai-capabilities-model-2025]]）。Zalando はガバナンスを既存の仕組みで扱っている。Tech Radar に AI の項目を加え、デプロイされた Docker イメージをスキャンして AI モデルの利用を自動検出している（[[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]）。

2 つの記述は、組織全体への展開に必要だったプラットフォームの作業を記述している。Zalando の ML プラットフォームチームは 2024 年 1 月に [[SoftwareApplication/litellm]] ベースのプロキシをデプロイし、これによってプラットフォームチームは導入状況を測定する単一の地点を得た（[[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]）。メルカリの AI Security チームは、10 を超える Organization にわたる Devin のための Terraform プロバイダーと自動化を構築した。これはメンバーと権限の管理、チームごとの利用上限、シークレットの一括ローテーション、API キーの有効期限、監査ログを扱い、その大半は標準機能が存在しなかったために作られた（[[BlogPosting/enabling-ai-usage-at-mercari-with-secure-devin-management]]）。プラットフォームに関する DORA の知見は、社内プラットフォームの品質が低いと AI 導入が組織のパフォーマンスに与える効果は無視できるほど小さく、品質が高いとその効果は強くプラスになるというものである（[[Report/dora-ai-capabilities-model-2025]]）。

### マンデートと目標

いくつかの記述は数値目標を掲げている。サイバーエージェントの経営陣は、2028 年までに開発プロセスを完全に自動化すること（AI 成熟度レベル 4 に相当）を目標に掲げた（[[BlogPosting/engineering-organization-reform-toward-full-development-automation-by-2028]]）。メルカリの Double プロジェクトは、生産性を 2 倍にするという目標にちなんで名付けられている（[[BlogPosting/pj-double-mercari-development-productivity]]）。マンデートに関する事例研究の対象企業は、CTO のメモで、12 か月間でエンジニアリングの生産性を 2 倍にするという目標を設定し、エンジニア 1 人あたり月あたりのマージされたプルリクエスト数を指標とした（[[ScholarlyArticle/ai-writes-faster-than-humans-can-review]]）。

[[DefinedTerm/ai-mandate]] は、そうしたコミットメントがとりうる幅を記録している。効果的な AI 活用を全従業員に対する「基本的な期待」とした Shopify から、導入しなかったエンジニアを解雇した Coinbase までである。事例研究は、スループットの向上のうちマンデートそのものに残る寄与はわずかであり、その大部分は導入と、利用の蓄積とともに大きくなるリターンによるものだと見出している。そのため著者らは、マンデートを直接生産的なものではなく触媒的なものと呼び、「ツールの展開ではなく、プロセス再設計の問題」と記述している。[[DefinedTerm/productivity-pressure-paradox]] は、スキルが蓄積される前に目標を要求することとこの論文が結びつける失敗を名指している。論文はまた、広く告知された目標は指標の水増しを招き、それを自らの研究設計では真の加速と完全には切り分けられないと警告している。

GitHub のプレイブックは、目標とは別の手段を記述している。リーダーが日々の仕事の観点から「なぜ」を説明し、AI が仕事を変えることについて率直であることである（[[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]）。DORA は、明確に伝えられた AI に対する姿勢を 7 つのケイパビリティの 1 つに挙げている（[[DefinedTerm/dora-ai-capabilities-model]]）。

### 役割、キャリア、スキル

キャリアに最も踏み込んでいるのはサイバーエージェントの記述である。同社の役員の記事は、2028 年のビジョンに対するエンジニアの反応を 5 つの不安、すなわちキャリア、スキルの劣化、不公平な評価、エンジニアの価値の変化、チーム間の格差に整理し、それぞれに施策を対応させている。その施策とは、4 つのキャリアラダーを軸にした評価制度の刷新、若手エンジニアの育成強化、エンジニア向けの AI ランキング、そして AI Driven 推進室である（[[BlogPosting/engineering-organization-reform-toward-full-development-automation-by-2028]]）。GitHub はシニアの個人貢献者に 2 つの使命を与えている。自身の仕事で AI を使うことと、AI を使いこなす力を他の人に広げることである（[[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]）。

2 つの記述はエンジニアリングの外にまで及んでいる。メルカリの AI Task Force は会社を 33 のドメインに分け、約 100 人のメンバーに拡大し、約 4,000 のワークフローを棚卸しした。その理由として述べられているのは、法務、セキュリティ、コンプライアンスのチェックが人を待ったままなら、コーディングが速くなるだけではリリースは速くならないということである（[[BlogPosting/choosing-ai-native-mercari-guiding-principles]]）。Toss のプログラムは当初から非開発職が感じていた隔たりを軸に組み立てられており、OpenAI との共同デーでは開発者向けとあわせて非開発者向けのハンズオンセッションが開かれた（[[BlogPosting/toss-ai-surf-day]]）。

スキル育成について、Zalando は、スキルを身につけるためのセッションで参加者がコーディングエージェントを近道として使いたいという強い誘惑に駆られ、それが通常は学習を妨げると報告している（[[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]）。アンケート調査では、非利用者の間で最も多い障壁は、必要なスキルの不足または時間の制約だった（[[ScholarlyArticle/generative-ai-adoption-in-software-engineering]]）。

## 各記述はそれをどう測定しているか

各記述が測定しているものは異なり、いくつかは導入と効果を分けている。

- **導入の広さと深さ。** GitHub のプレイブックは 3 段階で測定する。広さ（月間アクティブユーザーとエンゲージしたユーザー）、深さ（月あたりの利用日数によるユーザーの区分）、そしてビジネスへの効果である（[[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]）。Accenture の研究は、開発者の 81.4% がライセンスを受け取ったその日に拡張機能をインストールしたと報告している（[[Report/quantifying-github-copilots-impact-in-the-enterprise-with-accenture]]）。
- **組織の準備度。** ZOZO の All ZOZO AI Readiness Score（AZARS）は、個人がどこまで AI を仕事に組み込んでいるか、そして組織が AI を前提としたプロセスを仕組みに落とし込んでいるかを見る（[[Organization/zozo]]）。サイバーエージェントは AI 活用の 5 段階の定義を用いている。それを測定したあるグループ会社では平均が 6 か月で 1.23 から 3.27 に上がり、同社はこの測定を全社に広げつつある（[[BlogPosting/ai-knowledge-sharing-sessions-96-products]]）。
- **2 か月後の活用。** サイバーエージェントの共有会は、2 か月後の「アウトプット報告」で締めくくられ、そこでは会の感想ではなく、知見が実際にどれだけ使われたかを問う（[[BlogPosting/ai-knowledge-sharing-sessions-96-products]]）。
- **スループット。** Accenture の RCT は、プルリクエストが 8.69%、成功したビルドが 84% 増加したと報告している（[[Report/quantifying-github-copilots-impact-in-the-enterprise-with-accenture]]）。Microsoft は、早期導入者についてマージされたプルリクエストが +24.0% 増加したと推定している（[[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]]）。マンデートの研究は、アクティブな開発者 1 人あたりのプルリクエストが 2.09 倍になったと報告している（[[ScholarlyArticle/ai-writes-faster-than-humans-can-review]]）。メルカリは各プロジェクトの工数見積もりと実績工数を比較し、仕様駆動開発を用いたプロジェクトで 150% を超える改善を報告している（[[BlogPosting/pj-double-mercari-development-productivity]]）。
- **品質のガード。** メルカリは DX ツールでリバート率と MTTR を監視している（[[BlogPosting/pj-double-mercari-development-productivity]]）。Zalando は 4 つのコードベースでプルリクエストのサイズ分布と循環的複雑度を追跡している（[[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]）。GitHub のプレイブックは、AI によってプルリクエストが大きくなりうるため、プルリクエストのサイズは注視する価値があると指摘している（[[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]）。

いくつかの出典は、自らが選んだ指標が何を見落とすかを率直に述べている。Microsoft の著者らは、マージされたプルリクエストは小さく頻繁な PR を有利にし、品質面のコストを見落としうる不完全な代理指標だと述べている（[[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]]）。マンデートの研究は、速度中心のフレームワークはコードを書く速さの向上は捉えるが、押し出された作業がどこへ行ったかを見落とすと論じている（[[ScholarlyArticle/ai-writes-faster-than-humans-can-review]]）。アンケート調査では、回答者の 58.15% が規模、生産性、品質について客観的な指標を何も使っておらず、著者らは報告された改善を認識として扱っている（[[ScholarlyArticle/generative-ai-adoption-in-software-engineering]]）。

## 各記述が報告している不十分な点

**プログラム後も成果にばらつきがある。** サイバーエージェントの第 4 回の報告では、活用度を 4 以上と評価したプロダクトは 30% を少し超える程度で、約 30% は効果がなかったと報告した。記事の解釈は、共有会がすでに進んでいるチームには物足りず、遅れているチームにはハードルが高すぎたというものである（[[BlogPosting/ai-knowledge-sharing-sessions-96-products]]）。

**レビューの段階。** マンデートの研究では、プルリクエストの量が 3.1 倍に増えた一方、レビュアーの数は 1.5 倍にしか増えなかった。自動化された AI レビューが約 84% に増えるにつれ、人間のレビューを受けたプルリクエストの割合は 89% から 68% に下がり、人間のレビューは形だけの承認へと薄れていった（[[ScholarlyArticle/ai-writes-faster-than-humans-can-review]]）。DMM は、2025 年に全社で AI エージェントの導入が進むにつれて、コードレビューの負荷が急増したと報告している（[[Organization/dmm]]）。メルカリの pj-double は、レビューの負担の原因を、コードが AI によって書かれたことではなくプルリクエストのサイズに見出し、作業を 1 タスク 1 PR に分割することでそれを解消したと報告している（[[BlogPosting/pj-double-mercari-development-productivity]]）。Zalando は、大きなプルリクエストの増加や、レビュアーのやる気を削ぐような PR に夢中になるチームを報告し、低リスクと分類した 33% の PR を自動承認するリスクベースの承認ボットを記述している（[[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]）。このパターンについてのこのウィキのページは [[DefinedTerm/review-bottleneck]] を参照。

**効果が及ばないところ。** マンデートの研究は、効果が新しいリポジトリに集中しており、レガシーなリポジトリでは有意でないことを見出している（[[ScholarlyArticle/ai-writes-faster-than-humans-can-review]]）。Zalando は、報告されているスループット向上の多くがモノレポによるものである一方、自社はマイクロサービスのために主に個別のリポジトリを使っていると指摘している（[[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]）。メルカリの CTO は、従業員の 95% が AI ツールを使っているにもかかわらず、コーディングの生産性だけでは組織全体の生産性は上がらないため、同社はまだ自らを AI-Native とは見なしていないと述べている（[[BlogPosting/choosing-ai-native-mercari-guiding-principles]]）。

**標準プロセスの限界。** pj-double は、Agent Spec は仕様と設計がすでに合意されていることを前提としているが、合意に至ることこそが最も時間のかかる部分だったと報告している。チーム自身の診断は、AI と一緒に考えて決めるべき作業を、AI に委ねる作業として扱ってしまったというものである（[[BlogPosting/pj-double-mercari-development-productivity]]）。また、リッチな UI を持つ初期の社内 QA ツールを、手法の改善を難しくした「ビルドトラップ」として記述している。ZOZO の 2 コマンドに関する記事は、効果測定がまだ済んでいないと報告している（[[BlogPosting/ai-driven-development-two-commands]]）。

**並行する取り組みの間での共有。** メルカリの AI Task Force は、33 のドメインを独立して運営したことで意思決定は速くなったが、ベストプラクティスや振り返りがドメイン間で十分に共有されなかったと報告している（[[BlogPosting/choosing-ai-native-mercari-guiding-principles]]）。同社自身の記事は、ツールの自由、チームごとの分離、全社的なプロセス標準を、互いに調整することなく記述している（[[Organization/mercari]]）。

**すでにあるものを増幅する。** DORA の中心的な主張は、AI は高業績の組織の強みを、苦戦している組織の機能不全を増幅するというものである。ユーザー中心性が低い場合、AI 導入はチームのパフォーマンスの低下と関連している（[[Report/dora-ai-capabilities-model-2025]]）。Zalando の締めくくりのテーマも同じで、AI は既存の良い実践も悪い実践も増幅する（[[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]）。Microsoft の研究では、IDE の Copilot を以前から使っていたことは新しい CLI ツールを試すオッズを高めたが、継続率の低さと関連していた。著者らはこれを、エンジニアに慣れた代替手段があったためと解釈している（[[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]]）。

## 各記述の背後にある証拠の種類

| 記述 | 書き手 | 証拠の種類 |
|---|---|---|
| [[BlogPosting/engineering-organization-reform-toward-full-development-automation-by-2028]] | サイバーエージェントの技術担当役員 | 方針と意図の表明。施策を記述しており、効果は記述していない |
| [[BlogPosting/ai-knowledge-sharing-sessions-96-products]] | サイバーエージェントでプログラムを運営するスタッフ | プログラムの報告。効果の数値は参加プロダクトの自己申告 |
| [[BlogPosting/ai-code-agents-matsuri-seven-techniques]] | 取り組みを推進したサイバーエージェントのエンジニア | 一人称の記述。数値は著者自身のもの。手法は検証された方法ではなく経験 |
| [[BlogPosting/pj-double-mercari-development-productivity]] | メルペイ VPoE 室のマネージャー | 社内の測定。生産性の数値は見積もりと実績の主観的な比較に基づく |
| [[BlogPosting/choosing-ai-native-mercari-guiding-principles]] | メルカリの CTO | 方向性の表明。数値は同社自身のもの |
| [[BlogPosting/enabling-ai-usage-at-mercari-with-secure-devin-management]] | メルカリの AI Security エンジニア | 構築したツールについての運用者の記述。成果の測定はない |
| [[BlogPosting/ai-driven-development-two-commands]] | ZOZO の 1 部門の立場から執筆 | 1 部門での展開。効果測定は未実施 |
| [[BlogPosting/agentic-engineering-at-zalando-a-snapshot]] | Zalando の Executive Principal Engineer | 自社リポジトリについての同社の分析。行動の変化については明示的に逸話的 |
| [[BlogPosting/toss-ai-surf-day]] | Toss の Developer Relations Manager | 当事者の記述。測定された成果ではなく参加者の発言の引用 |
| [[Organization/dmm]] | DMM の 1 グループが自らのブログで | そのグループが自らの組織をどう説明しているか |
| [[BlogPosting/raising-productivity-floor-with-harness]] | 1 人のエンジニア | 方向性として、大部分は仮説として示された主張 |
| [[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]] | GitHub 社内の「AI for Everyone」イニシアチブのプログラムマネージャー・ディレクター | 自社プログラムについての GitHub の記述。成果の数値はない |
| [[Report/quantifying-github-copilots-impact-in-the-enterprise-with-accenture]] | GitHub と Accenture および Microsoft の研究者 | ランダム化比較試験、導入分析、ユーザー調査。製品のベンダーが実施・公表 |
| [[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]] | Microsoft の研究者 | 開発者単位のテレメトリ、合成コントロール法と固定効果。1 社・1 期間であり、著者らはツール販売元との近さを開示している |
| [[ScholarlyArticle/ai-writes-faster-than-humans-can-review]] | カーネギーメロン大学とスタンフォード大学の研究者 | 1 社の縦断的パネル。展開はランダム化されていない。対象は理想に近い環境と記述されており、上限を示すもの |
| [[ScholarlyArticle/generative-ai-adoption-in-software-engineering]] | 学術研究者 | 実務者 204 人へのアンケート。非確率的サンプル。利点は認識によるもの |
| [[Report/dora-ai-capabilities-model-2025]] | Google の DORA プログラム | 約 5,000 人の専門家へのサーベイと定性データ。最初のモデル |

成果を測定している 3 つの研究のうち、Accenture の RCT と Microsoft のテレメトリ研究は、いずれも測定対象のツールを販売する企業が実施したもの、あるいはその企業に近いものである。独立した学術的な事例研究は 1 社を対象としており、著者らはその対象を代表的なものではなく理想に近いものと記述している。組織的な施策そのものについての詳細の大半は当事者による記述が担っているが、そのほぼすべては自社の数値を報告しているか、数値を報告していないかのいずれかである。
