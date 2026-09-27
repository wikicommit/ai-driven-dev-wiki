---
title: "エージェントのルールをプロンプトから外し、決定論的な強制へ移す"
lang: ja
kind: pattern
review_status: pending
translated_from: ".wikicommit/view/en/moving-agent-rules-out-of-the-prompt.md"
source_commit: "29ecbc94374a9d0eab10c3e9db2c5bb06b9bd80f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
---

このウィキの多くのページが、同じ動きを記述している。AI エージェントに従わせたいルールは、最初はそのコンテキスト内のテキストとして始まる。[[DefinedTerm/claude-md]] や [[DefinedTerm/agents-md]] の 1 行、Markdown のルール文書、ツールの docstring、システムプロンプトなどである。そしてどの記述も、そのテキストが確実には守られないことに行き当たる。毎回必ず成り立たなければならないルールは、コンテキストから取り出され、それを実行するかどうかをモデルが決めることのない仕組みへと移される。フック、パーミッションルール、CI チェック、テスト、スクリプト、あるいはアプリケーションコード内のポリシーエンジンである。本ページは、この繰り返し現れる形、各ページがその理由として挙げるもの、どのルールを移しどのルールをそのまま残すのか、そして各ページが記録している限界を記述する。

## その形と、それが現れる場所

このビューの背後には 21 のページがある。そのうち 15 ページは、それぞれ自身の出典からこの形を述べている。

1. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]]: コンテキストウィンドウを通じて与えられるものはすべて「提案であって保証ではない」（"is a suggestion, not a guarantee"）。フックが決定論的な層として示されるのは、フックを実行するかどうかをモデルではなくランタイムが決めるからである。
2. [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]]: docstring やシステムプロンプトに書かれたビジネスルールは、モデルが解釈し、呼び出しのたびに判断し直すコンテキストである。呼び出しをキャンセルするフレームワークレベルのフックが、その強制として示される。
3. [[BlogPosting/claude-code-hooks-complete-guide]]: 「システムプロンプトは依頼である。フックは保証である。」（"A system prompt is a request. A hook is a guarantee."）
4. [[BlogPosting/steering-claude-code]]: 「X のときは毎回、必ず Y をする」（"every time X, always do Y"）はフックに置くべきものであり、「これは決してするな」（"never do this"）は指示に任せる仕事ではない。フックとパーミッションが決定論的な強制手段として挙げられる。
5. [[BlogPosting/writing-a-good-claude-md]]: 「Claude はリンターではない」（"Claude is not a linter"）。その仕事は、ファイル内の指示ではなく、たとえば `Stop` フックから実行される決定論的なフォーマッターやリンターが担う。
6. [[BlogPosting/skill-issue-harness-engineering-for-coding-agents]]: コーディングエージェントが指示を無視するのを 1 年間見てきた末に書かれたこの記事は、決定論的な制御フローの役割をフックに与える。その例のフックは、Claude が停止したときにフォーマッターと型チェックを実行し、失敗すると終了コード 2 を返す。こうしてハーネスがエージェントにエラーを修正させる。
7. [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]]: エージェント向けに Markdown で書かれたコーディングルールは、構造として表現できる範囲で ArchUnit テストへとコンパイルされ、必須の CI ゲートとして実行される。
8. [[DefinedTerm/deterministic-quality-gate]]: テストが通っていないままプルリクエストがマージされたことを受けて、テストはエージェント自身のワークフローの一ステップとしてではなく、`SubagentStop` フックと GitHub Action によって実行されるようになる。
9. [[SoftwareApplication/agent-governance-toolkit]]: プロンプトレベルの安全性は「確率的なシステムへの丁寧なお願い」（"a polite request to a stochastic system"）と表現される。ポリシーは、すべてのツール呼び出し、メッセージ、委任を傍受する決定論的なアプリケーションコードの中で強制される。
10. [[ScholarlyArticle/agentspec]]: ドメイン固有言語であり、そのルールはエージェントの意思決定ループにフックする強制層によって評価される。論文はこれを、自然言語による制約を対話レベルで適用する NVIDIA の NeMo や、制約の解釈を LLM に頼る GuardAgent と対比している。AgentSpec は強制をモデルの外部に保つ。
11. [[DefinedTerm/fides]]: Microsoft のアーキテクチャ決定記録（ADR）は、プロンプトインジェクションに対するプロンプトエンジニアリングによる防御を、非決定論的で回避可能だとして退け、呼び出しの実行前にポリシーをチェックするミドルウェアによって強制されるラベルを提案している。
12. [[BlogPosting/entering-the-software-3-0-era]]: ブランチ命名規約のような決定論的なロジックはスクリプトに移すべきであり、そうすればモデルは毎回その規約を解釈してトークンを費やす代わりにスクリプトを実行する。
13. [[DefinedTerm/security-context-file]]: すべてのセッションに読み込まれるセキュリティルールのファイルは、デプロイ前に通過しなければならない SAST、認証情報スキャン、インフラ検証と組み合わされ、「プロンプトの指示だけに頼ることはない」（"with no reliance on prompt instructions alone"）。
14. [[ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities]]: オープンソースコミュニティが明文化している AI コントリビューションのルールをコーディングエージェントがどう扱うかを測定したうえで、著者らは、禁止ルールと人間の承認を求めるルールをエージェントの外で強制することを推奨する。マージをブロックする CI チェック、必須の人間によるレビュー、あるいは AI が作成したプルリクエストを閉じるボットである。
15. [[BlogPosting/custom-code-review-rules-for-codex]]: `AGENTS.md` に書かれたリポジトリのルールは、テストやリンターを置き換えるものではなく補完するものと位置づけられる。決定論的かつ機械的なチェックはそうしたツールと CI に残り、テスト、ブランチ保護、必須の承認が引き続きハードな強制を担う。

3 つのページは複数の出典からこの形をまとめたものであり、別個の事例を加えるのではなく証拠を再掲している。

16. [[DefinedTerm/agent-hooks]] は、上記のいくつかのページから議論を集めている。このページが付け加えるのは、CLAUDE.md の指示は助言的であり、フックは決定論的だと 1 行で述べる Anthropic の Claude Code ドキュメントである。
17. [[DefinedTerm/claude-md]] は、[[BlogPosting/steering-claude-code]]、[[BlogPosting/writing-a-good-claude-md]]、Claude Code のメモリに関するドキュメントに依拠している。このページがそのドキュメントから付け加えるのは、CLAUDE.md は強制される設定としてではなくコンテキストとして読み込まれること、そして毎回のコミット前のような決まった時点で実行されなければならない指示は、代わりにフックとして書くべきだということである。
18. [[DefinedTerm/neurosymbolic-validation]] は、[[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] に現れるパターンに名前を与えたもので、その 1 本の記事から作られている。

残る 3 ページは、この形を述べてはいないが、それに関係している。

19. [[DefinedTerm/guides-and-sensors]] は、この形のための語彙を提供する。これはどのルールを移すかについての節で記述する。
20. [[BlogPosting/making-ai-follow-team-rules]] は一つの変形であり、後述の独立した節で記述する。これはチームのルールをセッションの冒頭からフックへと移すが、フックが届けるものは依然として、エージェントが従うことも無視することもできるテキストである。
21. [[BlogPosting/build-zero-trust-ai-agents-that-judge-intent]] は、決定論的な制御がどこで止まるかを記録している。これはモデルの外での強制についての節で記述する。

各ページの出典は種類がさまざまである。実務者のブログ、DEV Community 上の AWS の記事、自社製品についての Anthropic と OpenAI 自身のガイダンス、HumanLayer の記事、自分たちの実践についての 2 つのチームの記事（うち 1 つは Toss Bank のもの）、2 つのインフラプロジェクトについての 1 人のエンジニアの記事、Microsoft のリポジトリと Microsoft のアーキテクチャ決定記録、Google Cloud の記事、ICSE 2026 の論文、そして北京大学による実証研究である。そのうちのいくつかは [[SoftwareApplication/claude-code]] を中心としており、それらが記述するフックの慣習は、大部分がこのツールのものである。

## 各ページが指示を提案として扱う理由

各ページは、コンテキスト内の指示には拘束力がないという点で一致している。その理由として挙げるものは異なる。

- **指示の届けられ方。** [[DefinedTerm/claude-md]] は、CLAUDE.md の内容はシステムプロンプトの後にユーザーメッセージとして届けられるため、とりわけ曖昧な指示や互いに矛盾する指示については厳密な遵守が保証されない、と説明する Claude Code のドキュメントを記録している。[[BlogPosting/writing-a-good-claude-md]] は、このファイルが「関連するかもしれないし、しないかもしれない」と告げるシステムリマインダーとともに注入されるため、Claude は現在のタスクに無関係だと判断した内容を無視する、と報告している。
- **セッション中の劣化。** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、CLAUDE.md の規約、スキル、プロンプトがモデルの注意を奪い合うため、セッションが長くなるにつれて遵守率が下がる傾向があると述べる。[[BlogPosting/making-ai-follow-team-rules]] は、エージェントがルートの指示ファイルにあるルールをセッションの序盤には守り、後半には守らなくなったと報告し、これを [[DefinedTerm/lost-in-the-middle]] に帰している。
- **指示が多すぎる。** [[BlogPosting/writing-a-good-claude-md]] は、モデルが一貫して従える指示の数には限りがあり、指示を増やすとそのすべてにわたって指示追従が悪化すると論じる。[[BlogPosting/steering-claude-code]] は、持ち主のいない、膨らみ続ける CLAUDE.md は、重要な指示への遵守を薄めると述べる。
- **モデルは呼び出しのたびにルールを解釈し直す。** [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] は具体例を示す。支払いを先に確認しなければならないと書かれた docstring を読んだエージェントが、それでも予約を確定し、成功を報告したのである。[[BlogPosting/entering-the-software-3-0-era]] は同じ論点のコスト面の版を示す。規約を解釈するたびにトークンが費やされる。
- **エージェントがルールを読みもしない。** [[ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities]] では、アンカーなし・支援なしの 347 回の実行のうち、リポジトリのポリシーファイルが開かれたのは 12 回であり、支援なしでの違反 248 件のうち 242 件は、そのファイルが一度も開かれないまま起きた。
- **読まれても抵抗されるルールがある。** 同じ研究は、`AGENTS.md` に禁止事項をそのまま引用しても、4 つのエージェントのうち 3 つでは拒否率が 0% のままで、4 つ目も 10% に上がっただけであり、違反を名指しするフィードバックを 1 回与えても拒否率は最大 23% までしか上がらなかったことを見出した。著者らはこのパターンを、エージェントは自分の作業を広げる指示には従うが、作業を取り消す指示には抵抗する、とまとめている。
- **圧力、曖昧さ、インジェクション。** [[BlogPosting/steering-claude-code]] は、プロンプトで与えたルールが守られなくなる状況として、圧力、長いセッション、曖昧な状況、そしてモデルが読むファイルに仕込まれたプロンプトインジェクションを挙げる。[[SoftwareApplication/agent-governance-toolkit]] は、モデル層の防御が確率的なままであることの証拠として、プロンプトインジェクションに関するガイダンスと適応型攻撃の結果を挙げる。[[DefinedTerm/fides]] はプロンプトエンジニアリングによる防御を回避可能だとして退け、[[DefinedTerm/security-context-file]] は、プロンプトは上書きされ、誤解され、無視されうると述べる。
- **レビュアーへの負荷。** [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] は別の論点を示す。エージェントはコードを素早く生成するので、違反も同じ速さでやってくる。そして目視での確認では、レビュアーの負荷が際限なく増えていく。この記事の主張は、実行可能なルールによって検証が生成に追いつけるようになる、というものである。[[DefinedTerm/deterministic-quality-gate]] も同様に、レビュアーがテストが通ったことを手作業で確認する必要がなくなったと報告している。

## ルールの移し先

各ページを通じて、移し先は、ワークフローのどの時点でルールが成り立たなければならないかによって異なる。

- **ツール呼び出しの前。** Claude Code の `PreToolUse` フックや [[SoftwareApplication/strands-agents]] の `BeforeToolCallEvent` フックは、保留中の呼び出しを見て、それをブロックできる。[[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、フックがガードレールとして持つ価値の大半をこの時点に帰している。[[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] と [[DefinedTerm/neurosymbolic-validation]] は、実行前にキャンセルすればロールバックすべきものが何も残らないと指摘する。
- **ターンまたはサブエージェントの終了時。** `Stop` フックと `SubagentStop` フックは、テストスイート、ビルド、型チェック、リンターを、エージェントと作業の完了との間に置く（[[DefinedTerm/deterministic-quality-gate]]、[[BlogPosting/writing-a-good-claude-md]]、[[BlogPosting/skill-issue-harness-engineering-for-coding-agents]]、[[DefinedTerm/agent-hooks]]）。
- **パーミッションシステムと管理設定の中。** [[BlogPosting/steering-claude-code]] は、組織全体のガードレールを強制する唯一の方法として管理設定を挙げる。[[BlogPosting/claude-code-hooks-complete-guide]] は、これらの層を「`CLAUDE.md` は説得し、パーミッションはふるいにかけ、フックは強制して反応する」（"`CLAUDE.md` persuades, permissions filter, hooks enforce-and-react"）と表現し、堅牢化した構成では 3 つすべてを動かす。
- **スクリプトの中。** [[BlogPosting/entering-the-software-3-0-era]] は、決定論的なロジックをモデルが実行するスクリプトへと移す。ロジックは解釈されなくなるが、この記述では、スクリプトを実行するのは依然としてモデルである。
- **CI とマージの段階。** [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] は、ルールをチェックするジョブを必須のステータスチェックにし、違反のあるプルリクエストをマージできないようにする。[[DefinedTerm/deterministic-quality-gate]] はマージ前に GitHub Action でテストを実行する。[[DefinedTerm/security-context-file]] はデプロイ前にスキャンのゲートを置き、[[ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities]] は、マージをブロックする CI チェック、必須の人間によるレビュー、あるいは AI が作成したプルリクエストを閉じるボットを推奨する。
- **アプリケーションのミドルウェアまたはランタイムの強制層の中。** [[SoftwareApplication/agent-governance-toolkit]] は、ツール関数を YAML のポリシーで包み、そのポリシーを呼び出しのたびに評価し、各判断を監査証跡に書き込み、ポリシーがアクションを拒否したときには例外を送出する。[[DefinedTerm/fides]] は、呼び出しの実行前にミドルウェアでポリシーをチェックする。[[ScholarlyArticle/agentspec]] は、アクションの実行前、観測を生成した後、そしてエージェントがタスクを完了したときに、エージェントの反復ステップにフックする。

移し先によって、ルールを誰が持つかも異なる。[[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、フックの配置をそのスコープとして扱う。個人的なセーフティネットにはユーザー設定、チームの標準にはプロジェクトの設定、組織のガードレールには管理ポリシー設定である。[[BlogPosting/build-zero-trust-ai-agents-that-judge-intent]] は、チェックをプラットフォームで強制すると、その所有権がエージェント開発者とは別の、プラットフォーム管理者やセキュリティ管理者に移ると論じる。

## 移すルールと残すルール

すべてのルールを移すページは一つもない。いくつかのページは明示的に線を引いており、その線を引く場所はそれぞれ異なる。

- **守られなかったときのコストによって。** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、フックを破壊的なコマンド、シークレット、機密性の高いパス、そして 1 つか 2 つの CI/CD の標準のために取っておき、それ以外はすべてプロンプトとスキルに任せる。[[BlogPosting/claude-code-hooks-complete-guide]] は、たまに守られなくても損失が小さい好みまでフックにしすぎることを落とし穴として挙げる。[[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] は、推奨の範囲を予約、支払い、キャンセルといった影響の大きい操作に限定している。
- **ルールを機械的にチェックできるかどうかによって。** [[BlogPosting/custom-code-review-rules-for-codex]] は、フォーマットやその他の機械的なチェックを CI に残し、互換性の要件やデータの境界など、コード化しにくい判断のために `AGENTS.md` のルールを用いる。[[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] は、パッケージ構造とクラス間の関係に関する制約だけをコンパイルし、各ルール文書に、その制約のうちどれがすでにテストされ、どれが依然としてレビューに頼っているかを記載させる。
- **ルールの種類によって。** [[ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities]] は、開示と検証に関するルールは、エージェントがセッション開始時に読むファイルに残し、フィードバックループと組み合わせることを推奨する。4 つのエージェントのうち 3 つで、1 回のフィードバックにより Verify が 90〜100%、Disclose が 81〜97% に上がったからである。エージェントの外へ送るのは、フィードバックでほとんど動かなかった禁止ルールと人間の承認を求めるルールである。
- **欠陥が見えるようになる時点によって。** [[BlogPosting/making-ai-follow-team-rules]] は、コードの形から見分けられる欠陥をトリガー型のルールにし、N+1 クエリのように実行時にしか現れない欠陥は、常に読み込まれるコンテキストに残す。

[[DefinedTerm/guides-and-sensors]] は、これらの線に合う語彙を与える。これはハーネスの制御を、エージェントが行動する前に誘導するガイドと、事後に観測するセンサーとに分け、それぞれを計算的なもの（決定論的：テスト、リンター、型チェッカー）と推論的なもの（AI レビュー、LLM-as-a-Judge）とに分ける。`AGENTS.md` の規約は推論的ガイドの例であり、ArchUnit テストを実行するフックは計算的センサーの例である。その説明では両方が必要だとされる。フィードバックだけでは同じ間違いを繰り返し続けるエージェントになり、フィードフォワードだけではルールを書き込みはしても、それが機能したかどうかを知ることのないエージェントになる。[[DefinedTerm/security-context-file]] も同じ用語を使う。このファイルは推論的ガイドであり、エージェントが従い損ねたものは、決定論的なチェックとデプロイのゲートがやはり捕捉しなければならない。

いくつかのページは、強制と並んで指示にも役割を残している。[[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、より良い指示は役に立ち、コンテキスト内のドメイン知識は依然として影響が大きいと述べる。[[BlogPosting/claude-code-hooks-complete-guide]] は、CLAUDE.md、パーミッション、フックに同じ要件を共同で担わせる。

## 各ページが記録する限界

各ページは、この移行そのものについて次の限界を記録している。

- **決定論的なルールは、そのコード化の出来以上には良くならない。** [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] では、リフレクションを禁じるルールをそのまま素直にコード化したところ、リフレクション API を一度も呼んでいない生成コードまで捕捉してしまい、書き直さなければならなかった。同じページは、ルール文書、テスト、コードが互いに乖離していく様子を記述し、それらの整合性を保つことを未解決の問題として記録している。[[ScholarlyArticle/agentspec]] では、LLM が生成したルールが、曖昧な要件に対して過度に硬直的になることがあった。ある例では、観葉植物への水やりまで含めて、注ぐ行為を全面的に禁止してしまった。
- **真偽値のルールではすべてを表現できない。** [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] と [[DefinedTerm/neurosymbolic-validation]] は、ルールが真偽値であること、ファジーな論理や確率的な論理を表現できないこと、保護する操作ごとにルールを書く必要があることを指摘する。[[ScholarlyArticle/agentspec]] は、離散的なチェックポイントで強制するものであり、一連のアクションがもたらす長期的な帰結については推論しないと指摘する。
- **決定論的なチェックは、事前に指定されたものしか捕捉しない。** [[BlogPosting/build-zero-trust-ai-agents-that-judge-intent]] はこの限界から出発する。丁寧で構文的に正しい返金リクエストは、あらゆる決定論的なゲートを通過する。そして、個々には許可された返金からなる複数ターンにわたる悪用は、リクエストを 1 件ずつ評価するチェックからは見えない。
- **強制はフェイルオープンになりうる。** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] と [[DefinedTerm/agent-hooks]] は、Claude Code において、不正な形式の JSON で応答したフックは一度もパースされず、そのため呼び出しが通ってしまう一方、`exit 2` は呼び出しをブロックする、という仕組みを記述している。[[BlogPosting/claude-code-hooks-complete-guide]] は、`1` で終了するガードを落とし穴の一つに挙げる。アクションを通してしまうからである。[[DefinedTerm/agent-hooks]] は、Gemini API がクラッシュしたフックやタイムアウトしたフックを承認として扱うことを記録している。
- **すべてのフックがハードストップになるわけではない。** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、ブロックされた `Stop` を保証ではなく強い後押しと呼ぶ。理由をモデルに返して続行を求めるだけだからである。[[DefinedTerm/agent-hooks]] は、Claude Code は 8 回連続でブロックされるとそれでもターンを終了させる、という Anthropic のドキュメントの記述を記録している。
- **この仕組みにはコストがある。** 条件に一致するツール呼び出しのたびに、フックスクリプトを起動するコストがかかる（[[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]]）。[[DefinedTerm/fides]] は、すべてのツール呼び出しに加わるレイテンシ、手作業で設定するポリシー、そして過度に保守的になりうるラベル伝播を挙げる。これに対して [[ScholarlyArticle/agentspec]] は、数秒かかるエージェントの実行に対して、そのオーバーヘッドがミリ秒単位であると報告している。
- **この仕組みは攻撃対象になる。** フックは、ユーザーの権限で自動的に実行されるコードである。[[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、悪意のある `SessionStart` フックを仕込んだ PyPI のワームを挙げる。[[BlogPosting/claude-code-hooks-complete-guide]] は、クローンしたリポジトリ内のフックを `Makefile` や `postinstall` スクリプトと同様に扱い、自身の正規表現ベースのガードを、完全な境界ではなく多層防御の一部と呼ぶ。
- **強制は、コードがある場所で行われる。** [[SoftwareApplication/agent-governance-toolkit]] は、OS カーネルではなくアプリケーションのミドルウェア層で強制するため、ポリシーエンジンとそれが統制するエージェントが同じプロセスを共有すると指摘する。

## モデルの外は、常に決定論的とは限らない

各ページはたいてい、2 つの性質を一つのものとして扱っている。ルールがモデル自身の判断の外で評価されること、そしてその評価が決定論的であることである。いくつかのページは、前者の性質を持ちながら後者を持たない仕組みを記録している。

- [[DefinedTerm/agent-hooks]] は、Claude Code の prompt 型と agent 型のフックは決定論的にトリガーされるが、その出力の決定にはモデルの判断を用いることを記録している。[[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、Cursor が、高速なモデルに自然言語の条件を評価させるプロンプトベースのフックを追加したと報告し、LLM のプロンプトフックは本質的に非決定論的であり、それはガードレールには許されないことだと述べる。
- [[ScholarlyArticle/agentspec]] は、あらかじめ定義された強制手段の一つとして、ユーザーによる確認、事前定義されたアクション、停止と並んで、LLM による自己点検を挙げている。
- [[BlogPosting/build-zero-trust-ai-agents-that-judge-intent]] は、ゲートウェイに LLM ベースの自然言語ポリシーエンジンを追加する。これは提案された各ツール呼び出しを、実行前に平文のビジネスルールに照らして評価する。記事はこれを、同じシリーズの以前の記事で示した決定論的な制御の代替としてではなく、それと並ぶ多層防御として提示している。その主張はベンダー自身による説明であり、1 件のサンプル取引で実演されたものである。

これらの場合、ルールは自然言語に戻るが、それを読むのは、そのルールが統制する行動の主体であるエージェントではなく、呼び出しを止めることのできる別個のチェックである。

## 変形：ルールを強制するのではなく届けるフック

[[BlogPosting/making-ai-follow-team-rules]] は同じ観察から出発する。ルートの指示ファイルにあるルールは、セッションが長くなるにつれて守られなくなる。そして同じ仕組みである [[DefinedTerm/agent-hooks]] に手を伸ばすが、その使い方が異なる。このプラグイン [[SoftwareApplication/pfmls-stylepack]] は、ファイルが書き込まれた直後の時点と、エージェントが終了しようとする時点にフックする。それぞれの時点で、該当する規約ルールをいくつか、それが適用されるコードの隣にテキストとして注入する。何もブロックはせず、ループ終了時のテキストは自らを、ハードな失敗ではなくレビューを促すリマインダーだと述べている。このページは、自らの問題を、ルールを*いつ*、*いくつ*提示するかの問題として捉えている。ここで移されるのは、ルールがコンテキストに入る場所であって、それが守られるかどうかを誰が決めるかではない。

このページは、上で挙げた限界のうち 2 つに突き当たっている。そのフックがファイル名パターンと正規表現でルールを選ぶのは、モデルベースの関連性チェックでは 1 リクエストあたり約 10 秒が加わったからである。またこのページは、緩い条件でトリガーされるルールが 21 のセッションで発火したにもかかわらず、一度もコードの変更につながらなかったと報告し、誤ったフィードバックはエージェントにルールを軽視することを教えてしまうと論じている。

## 証拠の強さ

証拠の大半は、1 つのチームまたは 1 人の著者による記述である。[[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] は、2 つの無効なケースと 1 つの有効なケースからなる、目的に合わせて作った例で結果を報告しており、それを独立した証拠ではなく具体的な例示だと述べている。[[DefinedTerm/deterministic-quality-gate]] は、2 つのプロジェクトについての 1 人のエンジニアの報告である。[[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] は導入前後の測定値を報告しておらず、[[BlogPosting/making-ai-follow-team-rules]] の数値はそのチーム自身のログに由来する。[[BlogPosting/steering-claude-code]] は自社製品についての Anthropic のガイダンスであり、[[BlogPosting/custom-code-review-rules-for-codex]] にある 98% 対 58.3% という数値は、レビューを導くルールについての OpenAI の社内評価であって、プロンプトから外に移されたルールについてのものではない。[[DefinedTerm/fides]] はステータスが *proposed*（提案中）のアーキテクチャ決定記録であり、[[DefinedTerm/guides-and-sensors]] は 1 人の著者によるメンタルモデルである。

測定を報告しているページは 2 つあり、それぞれがこのパターンの一部しか扱っていない。[[ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities]] が測定しているのは前提のほうである。すなわち、4 組のエージェントとモデルの組み合わせが、単純なイシューにおいて、リポジトリのファイルに置かれた AI コントリビューションのルールにどれだけ従うかである。この研究は、自らが推奨する CI チェック、レビュー、ボットについては測定していない。[[ScholarlyArticle/agentspec]] が測定しているのはランタイムでの強制である。リスクのあるコード実行を 90% 超のケースで阻止したこと、身体性を持つエージェントの危険なタスクを 0% に減らした一方で、安全なタスクの完了率が 58.62% から 54.26% に下がったこと、そしてテストした運転シナリオで 100% の遵守を達成したことを報告している。これらの結果は、チームのコーディングルールではなく、コード、身体性、運転の各エージェントに対する安全上の制約に関するものである。

これをパターンたらしめているのは、同じ形が別々に書かれた出典にわたって繰り返し現れる頻度であり（[[DefinedTerm/agent-hooks]]、[[DefinedTerm/claude-md]]、[[DefinedTerm/neurosymbolic-validation]] は、それぞれ他のページからまとめられたものなので例外である）、ルールを移すことが一般に機能するという測定された証拠ではない。
