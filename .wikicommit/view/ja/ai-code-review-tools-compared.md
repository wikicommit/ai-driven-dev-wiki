---
title: "AI コードレビューツールの比較"
lang: ja
kind: comparison
review_status: pending
translated_from: .wikicommit/view/en/ai-code-review-tools-compared.md
source_commit: f291846dff67d5179c6b1d4d336ea47e69d2e0e4
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
---

このページでは、この wiki のページ上で、コード変更に対する AI レビュアーが主要な機能の一部として説明されている 18 のツールを比較する。

- 専用のレビューツール:[[SoftwareApplication/coderabbit]]、[[SoftwareApplication/greptile]]、[[SoftwareApplication/sourcery]]、[[SoftwareApplication/pr-agent]]、[[SoftwareApplication/codestrike]]、[[SoftwareApplication/open-code-review]]、[[SoftwareApplication/asyncreview]]
- より大きな製品のレビュー機能:[[SoftwareApplication/github-copilot-code-review]]、[[SoftwareApplication/codex-code-review]]、[[SoftwareApplication/claude-code-security-review]]、そして Alibaba Cloud のガイドが Qoder CN と呼ぶ製品向けに説明している Code Review エージェント([[SoftwareApplication/qoder]] のページに記録)
- レビューを行うように設定できるツール:[[SoftwareApplication/claude-code-action]]、[[SoftwareApplication/antigravity-sdk]]、[[SoftwareApplication/devin]]
- レビュー段階を持つ、より広範なエージェントやワークフロー:[[SoftwareApplication/open-swe]]、[[SoftwareApplication/unit-mesh-auto-dev]]、[[SoftwareApplication/conductor-gemini-cli-extension]]、[[SoftwareApplication/compound-engineering-plugin]]

[[SoftwareApplication/ast-grep]] は、それ自体がレビュアーとしてではなく、これらのうちの 1 つが使う構成要素として以下に登場する。Qoder のページは、Qoder CN が別名の Qoder なのか、地域版なのか、別の製品なのかは未確定であり、ガイドが Qoder CN について述べていることを Qoder について確立された事実として読むべきではないとしている。したがって、このレビューエージェントに関する以下の記述はすべて、ガイドが説明する Qoder CN に帰属させている。

これらのツールはいくつかの点で異なる。

- レビュアーがどこで動くか
- リポジトリのどこまでを読むか
- ノイズをどう抑えるか
- チームが何を重視するかをどう伝えるか
- コメントするだけで止まるかどうか
- そのツールについて語られていることの裏付けがどのような種類のエビデンスか

このページはそれらの違いを並べて示す。ツールの順位づけはしない。依拠するページもそれを支持しない。記録されている内容の大半は、各プロジェクト自身の説明か、1 つのチームの印象だからである。

## レビュアーの居場所

ツールは、レビュー対象のコードにまったく異なる経路でたどり着く。

- **プルリクエスト上のボットアカウントやサービス。** CodeRabbit は、ベンダーが管理する独自のログイン `coderabbitai[bot]` で、行単位のコメントとレビューの判定を投稿する。Greptile は、プルリクエストにコメントし、そこで問い合わせられると返信するサービスとして記録されている。
- **フォージ自体の機能。** GitHub Copilot コードレビューは [[SoftwareApplication/github-copilot]] の一部である。手動でリクエストすることも自動でトリガーすることもでき、GitHub.com、GitHub CLI、GitHub Mobile、いくつかの IDE から使える。エージェント的な機能は GitHub Actions のランナー上で動く。
- **リポジトリで有効化するコーディングエージェントの機能。** Codex Code Review は [[SoftwareApplication/openai-codex]] のコードレビュー機能である。GitHub リポジトリで有効にするもので、`@codex review` でレビューをリクエストすることもできる。
- **エージェントを実行する CI ステップ。**
  - Claude Code Action は、[[SoftwareApplication/claude-code]] のエージェントをプルリクエスト上に置く GitHub Action である。そこでレビュー、CI 失敗の診断、レビューコメントへの対応ができる。
  - Claude Code Security Review は、プルリクエストが作成されたときに実行され、脆弱性についてインラインでコメントする GitHub Action として提供されている。
  - Google のあるコードラボでは、Antigravity SDK で構築した読み取り専用のレビューエージェントを、プルリクエストごとに GitHub Actions のワークフローで実行し、指摘をコメントとして投稿する。
  - 弥生のあるチームは Devin をレビュアーとして GitHub Actions に組み込んでいる。プルリクエストが作成・更新・再オープンされると Devin の API でレビューセッションを作成し、Devin が指摘をコメントとして投稿する。
- **コーディングエージェント内のコマンド。**
  - Claude Code Security Review は、コードをコミットする前に Claude Code で実行する `/security-review` コマンドとしても存在する。
  - ガイドの説明によれば、Qoder CN の Code Review エージェントはエージェントモードで `/code-review` または自然言語のリクエストで呼び出し、対象はプロジェクト全体、特定のファイル、Git の差分、プルリクエストのいずれかに絞れる。
  - Compound Engineering Plugin は Claude Code に `/workflows:review` を追加する。
  - Conductor は、コーディングエージェントがタスクを終えた後に、実装後レポートとしてレビューを出力する。
- **単体のコマンドラインツール。**
  - Open Code Review は `ocr` として呼び出す CLI である。ワークスペースの変更、ブランチの範囲、単一のコミットをレビューする。
  - codestrike はプルリクエストの URL を指定して `codestrike review` で起動する。CI パイプラインや webhook から呼び出す HTTP サービスとしても動かせる。
  - PR-Agent はスラッシュコマンド(`/describe`、`/review`、`/improve`、`/ask`)を提供し、プルリクエストのコメントとしても CLI からも実行できる。
  - AutoDev の CLI は `autodev review` でレビューを実行する。
- **より広範なエージェントプラットフォームの 1 つの役割。** Open SWE は、コードを書くエージェントとは別に Reviewer のエントリポイントを備えている。オンデマンドまたは自動で、読み取り専用のプルリクエストレビューを実行する。
- **別のエージェントがインストールする機能。**
  - AsyncReview は `npx` で実行され、他のコーディングエージェントがスキルとしてインストールできる。
  - Open Code Review は、いくつかのコーディングエージェント向けのプラグインと可搬なスキルを提供している。
  - codestrike は [[SoftwareApplication/cursor]] のプラグインとして提供されている。
  - Conductor は Gemini CLI 以外のツールからも使えるプラグインになった。
  - Open Code Review の委譲モードは、この関係を逆転させる。ユーザー自身のコーディングエージェントが自分のモデルでレビューを行い、`ocr` はファイルの選択とルールの解決を担う。

フォージ間の移植性について、PR-Agent のページは GitHub、GitLab、BitBucket、Azure DevOps、Gitea と、CLI、GitHub Action、Docker、セルフホスト、webhook でのデプロイを挙げている。Open Code Review は GitHub Actions、GitLab CI、GitFlic CI、Gerrit との CI 連携を文書化している。

## 差分のどこまで先を読むか

ページには、差分だけを見るものからリポジトリを探索するものまで、幅のあるレビュアーが記録されている。

- codestrike はデフォルトで差分をレビューする。フラグを指定するとファイル全体の内容を取得するようになり、そのページはこれを、より情報が豊富だが遅くトークンを多く消費すると説明している。
- PR-Agent は、`/review`、`/improve`、`/ask` はそれぞれ 1 回の LLM 呼び出しで実行されると述べている。小さなプルリクエストにも大きなプルリクエストにも対応できるのは PR 圧縮戦略のおかげだとしている。
- AutoDev のレビューは、まず静的な情報を集める。Git の差分から変更されたハンク、CodeGraph などのツールで特定した影響を受けるクラスやメソッド、リンターの結果、関連する issue やテストである。そのうえで初めて LLM が分析する。リポジトリ全体の調査は CodebaseInvestigatorAgent が担う。
- Open Code Review のエージェントは、ファイル全体を読み、コードベースを検索し、変更された他のファイルを調べることができる。意味のある差分がない場合は、`ocr scan` モードでファイル全体をレビューする。
- Copilot コードレビューは 2026 年 3 月にエージェント的なツール呼び出しのアーキテクチャに移行した。リポジトリを探索し、リンクされた issue やプルリクエストを読み、読みながら問題を記録し、レビューをまたいでメモリを保持できる。
- AsyncReview のループは Python コードを生成し、それをサンドボックス化された REPL で実行し、ファイル取得や検索の呼び出しは GitHub API から応答させ、回答するまでこれを繰り返す。
- Conductor は新しいコードをプロジェクトの `plan.md` と `spec.md` に照らしてチェックし、レビューの一部として関連するユニットテストと統合テストを実行する。
- Claude Code Security Review のコマンドは、潜在的な脆弱性を求めてコードベースを検索する。
- Qoder CN のレビュー範囲は開発者のリクエストで決まり、ガイドは大きな変更についてはより細かいフィードバックを得るためにモジュールごとにレビューすることを勧めている。
- コードラボの Antigravity SDK のレビューエージェントは 2 層で制限されている。ポリシーがまずすべてを拒否し、そのうえでファイル読み取りツール、コマンド実行、`finish` を許可する。さらにその上で、ツール実行前のフックが `git` で始まらないコマンドをすべて拒否する。
- Claude Code Action の深さは、チームが書くフロー次第である。あるチームのフローは、どのサブエージェントがレビューするよりも前に、PR のメタデータ、解決対象の issue、作成者、開発領域、適用されるガイドラインを収集する。

すべてのページがこの軸上に自分のツールを位置づけているわけではない。CodeRabbit、Greptile、Codex Code Review、Devin、Open SWE、Compound Engineering Plugin のページは、レビュアーが周囲のコードをどれだけ読むかについて何も述べていない。Sourcery のページは、各チャンクが必要な周辺の行で拡張されるとしか述べていない。

## ノイズをどう抑えるか

いくつかのツールは、不要なコメントを設計上の主な対策対象として扱っており、その対策を置く場所はそれぞれ異なる。

- **モデルの前に行う決定的な処理。**
  - Sourcery は差分をアトミックなチャンクに分割し、新しい import のように複雑さに影響しえないとヒューリスティクスで判断できるものは、LLM を呼ばずに捨てる。
  - Open Code Review は、ファイルの選択、バンドル、ルールのマッチング、コメントの位置決めを、モデルではなく通常のコードに担わせている。
  - CodeRabbit は、AST パターンに基づくレビュー指示のために内部で [[SoftwareApplication/ast-grep]] を使っている。CodeRabbit の記事を要約したある章は、決定的なマッチングが生成 AI 単独のノイズとばらつきを減らすものとして紹介している。
- **コメントに対する 2 回目のパス。**
  - Sourcery は生成した各コメントを別の LLM リクエストに送り、一般的すぎるものは破棄する。そのページによれば、Sourcery の実験ではこれで誤検知の大半が取り除かれた。
  - Open Code Review にはコメントのリフレクションモジュールがある。
  - Claude Code Action のページに記録されているチームのフローは、重大度評価のサブエージェントを加えている。各コメントが妥当で捏造されていないかを確認し、重大度の高い指摘だけをインラインでコメントし、他のエージェントがすでに述べたことは抑制する。
  - Claude Code Security Review の Action は、カスタマイズ可能なルールを適用して誤検知や既知の問題を除外する。
  - Open SWE は、指摘を GitHub に公開する前に差分に根拠づけられた状態に保つと説明されている。
- **黙っていること。** GitHub は、Copilot コードレビューはレビューの 71% で対応可能なフィードバックを示し、残りでは何も言わないと報告している。また、1 つのパターンが繰り返し現れる場合は 1 つのコメントにまとめる。
- **再現率と引き換えに適合率を取る。** Open Code Review は、ノイズより適合率を優先する意図的なトレードオフとして、低い再現率を受け入れると述べている。
- **モデルの後で決定的な指摘と統合する。** AutoDev は、lint の指摘と AI の指摘をまとめて統合・優先順位づけし、ユーザーが編集できる 1 つの修正計画にする。
- **指摘の等級づけ。**
  - Conductor は指摘を High、Medium、Low に等級づけし、それぞれに正確なファイルパスを付ける。
  - Qoder CN のガイドは、エラー、警告、提案に分類されたレポートを説明している。

Devin のページは、仕組みではなく問題を記録している。弥生のチームは、プロジェクトのコンテキストの把握が不十分なことによる的外れな指摘や、プロジェクトが意図的に受け入れている事項に対する誤検知を報告している。そうしたケースを記録する場所として Devin の Knowledge 機能を挙げているが、これは確立された実践ではなく、方針として述べられているものである。

CodeRabbit のページには、ノイズを減らす方法としては提示されていない、コメントに関する記録もある。CodeRabbit は実質的なコメントに Refactor suggestion、Potential issue、Nitpick などのヘッダーを付けており、研究者はそのヘッダーを解析できる。それをレビュー内容の尺度として用いた研究は、これらのヘッダーは検証されたものではなく自己申告であること、重大度の順序づけはしていないこと、そして問題の種類、正しさ、コード品質を独立に検証した尺度ではないことを明言している。

## チームが何を重視するかをどう伝えるか

カスタマイズの手段は、程度だけでなく種類からして異なる。

| ツール | ページにカスタマイズ手段として記録されているもの |
|---|---|
| Codex Code Review | ルートおよびネストした [[DefinedTerm/agents-md]] ファイル内のルール。変更されたファイルに適用され、各指摘で引用される |
| Copilot コードレビュー | head ブランチから読まれる `.github/copilot-instructions.md`、パススコープの `*.instructions.md`、`AGENTS.md`、リポジトリのエージェントスキル。レビュー中に使える MCP サーバー。Lite と Balanced の工数レベル |
| Devin | 弥生のチームによれば Devin が自動的に参照する `AGENTS.md`。リポジトリにコミットされたレビュー観点のファイル。呼び出し側がセッションごとに組み立てるプロンプト |
| codestrike | システムプロンプト、トーン、ガードレール、トークン予算を設定する YAML ファイル。プロンプトファイルに対応づけたレビューペルソナ。CLAUDE.md、AGENTS.md、Cursor のルールの任意の読み込み |
| PR-Agent | 設定ファイルでカスタマイズできる JSON ベースのプロンプト |
| Open Code Review | テンプレートエンジンで各ファイルにマッチさせるレビュールール |
| CodeRabbit | ast-grep のルール設定による、AST パターンに基づくレビュー指示 |
| Greptile | 受け取ったコメントやリアクションから自動生成され、すべてのリポジトリに適用されるカスタムルール |
| Open SWE | 別の Analyzer が過去のフィードバックから学習したリポジトリ固有のレビューの好み。組織全体のレビューガイドライン。設定可能なモデルと推論の度合い |
| Conductor | 計画時に生成されるプロジェクトの `plan.md`、`spec.md`、スタイルガイド、ガイドラインファイル |
| AutoDev | 選択するレビュー種別:包括的、パフォーマンス、セキュリティ、スタイル |
| Compound Engineering Plugin | セキュリティ、パフォーマンス、アーキテクチャ、複雑さに特化したレビュアー |
| Claude Code Security Review | セキュリティに特化したプロンプト。カスタマイズ可能なルールとチームのセキュリティポリシー |
| Qoder CN(ガイドによる) | 開発者がリクエストの中で説明する業務上の背景 |
| Antigravity SDK | コードラボのエージェントにおける許可/拒否ポリシー、フック、エージェントスキル、レスポンススキーマ |
| Claude Code Action | チームがフェーズとサブエージェントとして書くレビューフローそのもの |
| Sourcery、AsyncReview | ページにカスタマイズ手段の記録なし |

モデルの選択も同じ軸に沿ってばらつきがある。

- Copilot コードレビューは意図的にモデルの切り替えをサポートしていない。
- codestrike は OpenAI 互換の任意のエンドポイントを受け付ける。
- PR-Agent はいくつかのベンダーと、[[SoftwareApplication/litellm]] 経由で到達できるあらゆるものを挙げている。
- Open Code Review はプロバイダーとモデルを設定できる。
- AsyncReview には Gemini の API キーが必要である。
- Antigravity SDK は Gemini または Vertex AI に対して認証し、ローカルモデルでエージェントを動かすこともできる。

## コメントだけで止まるか

これらのツールのほとんどはコメントし、次のステップを人に委ねる。いくつかのページはそれ以上のことを記録している。

- **修正する。**
  - AutoDev は CodingAgent によって、ロールバックや反復が可能なパッチとして修正を生成する。
  - Claude Code Security Review には、見つけた各問題の修正を実装するよう依頼できる。
  - Copilot コードレビューは提案を Copilot のクラウドエージェントに渡し、それを適用したプルリクエストを作成させることができる。
  - Conductor では、指摘に取り組むためのトラックを開始できる。
- **承認する。**
  - Copilot コードレビューはすべてのレビューに承認の評価を含める。デフォルトでは必須の承認数には数えられない。
  - Copilot による承認(パブリックプレビュー)を有効にすると、Copilot は必須承認のルールを満たす承認レビューを提出できる。新しいコミットがプッシュされると、その承認は取り消される。
  - DMM のあるチームは、Claude Code Action を使ってプルリクエストを 4 つの軸で採点し、閾値を超えると自動で承認していた。ページによれば、精度は実用に耐えたものの、この仕組みはそのチームに定着しなかった。チームが挙げる理由は、レビューは意図を共有するための対話でもあるということである。
- **読み取り専用にとどまる。**
  - Open SWE の Reviewer は読み取り専用である。
  - コードラボの Antigravity SDK のレビューエージェントは読み取り専用として構築されている。
  - Codex Code Review のページは、このツールは追加のレビュアーであって強制の仕組みではなく、テスト、ブランチ保護、必須承認が厳格なゲートであり続けると述べている。
  - Cognition は、Devin のプルリクエストレビューの役割を明らかな問題を拾う一次チェックに限定しており、人間によるレビューは依然として必要だとしている。

## それぞれの説明の裏付け

これらのページの裏付けとなるエビデンスにはばらつきがあり、ページ自身もそう述べている。

- **ベンダーのドキュメントと発表。**
  - Copilot コードレビューは GitHub のドキュメント、ブログ、変更履歴に基づく。
  - Codex Code Review は OpenAI の発表に基づく。OpenAI は、主要な評価スイートにおいて、ルールに導かれたバリアントが必要なカスタム指摘の 98% を回収し、ベースラインの対照群は 58.3% だったと報告している。
  - Claude Code Security Review は Anthropic の発表に基づき、その発表は Anthropic 自身のコードでこの Action が見つけた 2 つの脆弱性を挙げている。
  - Conductor のページは、その機能は測定結果ではなく Google 自身による説明だと注記している。
  - Qoder CN のレビューエージェントは Alibaba Cloud のユーザーガイドで説明されている。そのガイド自体が製品の最新機能を反映していない可能性があると注記しており、Qoder のページもそれを Qoder について確立されたものとして扱っていない。
  - Antigravity SDK のレビュー用途は、Google のコードラボのチュートリアルに由来する。
- **プロジェクトの README。**
  - Open Code Review、codestrike、PR-Agent、AsyncReview、Open SWE は、それぞれ自身のリポジトリに基づく。
  - Open Code Review のベンチマーク結果は、自前のデータセット [[Dataset/aacr-bench]] 上での自身の結果であり、数値は画像でしか示されていない。
  - AsyncReview は評価を報告していない。
  - codestrike は自らを、まだ本番利用を想定していないパブリックプレビューと説明している。
  - Open SWE は自らを活発に開発中と説明している。
- **著者や書籍による説明。**
  - Sourcery と ast-grep のページは、ベンダーの記事を要約した書籍の章に基づく。
  - AutoDev のレビューは、その作者自身のブログで説明されている。
  - Compound Engineering Plugin のページは、それを推薦する第三者のブログ記事に基づく。
- **ツールを使っているチームのエンジニアリングブログ。**
  - Greptile のページはそのような記事 1 本に、Claude Code Action のページは 2 本に基づく。そこでの比較評価は測定ではなくそのチームの印象である。最初の記事のチームは、1 つを選ぶのではなく Greptile、Claude Code Action、Copilot を並行して運用している。
  - Devin のレビュー用途は弥生のチームの記事に由来する。Devin のページは、Cognition 自身によるこのエージェントの評価も引いている。
- **公開 GitHub のマイニング研究。** これらのページにあるレビュー用途の説明のうち、第三者の研究に基づいているのは CodeRabbit のものだけである。その研究では、CodeRabbit は十分な量と機械的に解析できるラベルを持つ唯一の専用レビュアーボットだった。研究は、ラベルの構成がプルリクエストをどのエージェントが作成したかによって異なることを見出したが、その理由を特定することは控えている。

これらのツールが具体化している、より広い概念は [[DefinedTerm/agentic-code-review]] である。
