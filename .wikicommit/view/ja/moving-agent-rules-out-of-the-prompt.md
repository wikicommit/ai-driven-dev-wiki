---
title: "エージェントのルールをプロンプトから決定論的な強制へ移す"
lang: ja
kind: pattern
translated_from: ".wikicommit/view/en/moving-agent-rules-out-of-the-prompt.md"
source_commit: "0ce453edce84e501a06ee6011d772f2c1202bd39"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending
---

このウィキのいくつかのページは、同じ動きを記述している。AI エージェントに従わせたいルールは、最初はそのコンテキスト内のテキストとして置かれる。[[DefinedTerm/claude-md]] の 1 行、Markdown のルール文書、ツールの docstring、システムプロンプトなどである。そしてどの記述も、そのテキストが確実には守られないことに気づく。毎回必ず成り立たなければならないルールは、コンテキストから取り出され、実行するかどうかをモデルが決められない仕組み、すなわちフック、パーミッションルール、CI チェック、テスト、あるいはアプリケーションコード内のポリシーエンジンへと移される。本ページは、この繰り返し現れる形と、各ページが挙げるその理由、そして各ページが記録している限界を記述する。

## その形と、現れる場所

このビューの元になっている 10 ページのうち 9 ページはこの形を直接述べており、1 ページはその変形を記述している。

1. [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]]：コンテキストウィンドウを通じて与えられるものはすべて「提案であって、保証ではない」。フックが決定論的な層として示されるのは、フックを実行するかどうかをモデルではなくランタイムが決めるからである。
2. [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]]：docstring やシステムプロンプトに書かれたビジネスルールは、モデルが呼び出しのたびに解釈し、判断し直すコンテキストである。呼び出しを取り消すフレームワークレベルのフックが、強制の手段として示される。
3. [[BlogPosting/claude-code-hooks-complete-guide]]：「システムプロンプトはお願いである。フックは保証である。」
4. [[BlogPosting/steering-claude-code]]：「X のたびに必ず Y をする」はフックに置くべきものであり、「これは決してするな」は指示に任せる仕事ではない。フックとパーミッションが決定論的な強制手段として挙げられている。
5. [[BlogPosting/writing-a-good-claude-md]]：「Claude はリンターではない」。その仕事は、ファイル内の指示ではなく、たとえば `Stop` フックから実行される決定論的なフォーマッターやリンターが担う。
6. [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]]：エージェント向けに Markdown で書かれたコーディングルールを、構造的に表現できる範囲で ArchUnit のテストへとコンパイルし、必須の CI ゲートとして実行する。
7. [[DefinedTerm/deterministic-quality-gate]]：テストが通らないままプルリクエストがマージされたことを受けて、テストをエージェント自身のワークフローの一手順とするのをやめ、`SubagentStop` フックと GitHub Action で実行するようにした。
8. [[SoftwareApplication/agent-governance-toolkit]]：プロンプトレベルの安全策は「確率的なシステムへの丁寧なお願い」と表現される。ポリシーは、あらゆるツール呼び出し、メッセージ、委譲を横取りする決定論的なアプリケーションコードで強制される。
9. [[DefinedTerm/agent-hooks]]：このページは上記のいくつかのページから議論を集めたものなので、別個の事例を加えるのではなく、それらの証拠を再掲している。このページが加えているのは、Anthropic の Claude Code ドキュメントが、CLAUDE.md の指示は助言的であるのに対してフックは決定論的であると 1 行で述べていることの記録である。
10. [[BlogPosting/making-ai-follow-team-rules]] は、最後の節で記述する変形である。チームのルールをセッション開始時からフックへと移すが、フックが届けるのは依然として、エージェントが従うことも無視することもできるテキストである。

これらのページの出典の種類はさまざまである。DEV Community 上の AWS の投稿、実務者のブログ、自社製品に関する Anthropic 自身のガイダンス、HumanLayer の投稿、ZOZO と Toss のエンジニアリング記事、2 つのインフラプロジェクトでの経験に基づく 1 人のエンジニアの投稿、そして Microsoft のリポジトリである。いくつかは [[SoftwareApplication/claude-code]] を中心としており、そこで記述されるフックの慣習は主にこのツールのものである。

## 各ページが指示を提案として扱う理由

各ページは、コンテキスト内の指示には拘束力がないという点で一致している。その理由はそれぞれ異なる。

- **セッションが進むにつれての劣化。** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、CLAUDE.md の規約、スキル、プロンプトがモデルの注意を奪い合うため、セッションが長くなるほど遵守率が下がる傾向にあると述べる。[[BlogPosting/making-ai-follow-team-rules]] は、エージェントがセッションの初期にはルートの指示ファイルのルールに従っていたが後には従わなくなったと報告し、これを [[DefinedTerm/lost-in-the-middle]] に帰している。
- **指示が多すぎる。** [[BlogPosting/writing-a-good-claude-md]] は、モデルが一貫して従える指示の数には限りがあり、指示を増やすとすべての指示への追従が悪化すると論じる。[[BlogPosting/steering-claude-code]] は、管理者のいないまま膨らんでいく CLAUDE.md は、重要な指示への遵守を薄めてしまうと述べる。
- **モデルは呼び出しのたびにルールを解釈し直す。** [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] は具体例を示している。エージェントは、支払いを先に確認しなければならないと書かれた docstring を読みながら、それでも予約を確定し、成功と報告した。
- **圧力、曖昧さ、インジェクション。** [[BlogPosting/steering-claude-code]] は、プロンプトで与えたルールが破られうる状況として、圧力、長いセッション、曖昧な状況、モデルが読むファイル内のプロンプトインジェクションを挙げる。[[SoftwareApplication/agent-governance-toolkit]] は、プロンプトインジェクションに関するガイダンスと適応的攻撃の結果を、モデル層の防御は確率的なままであることの証拠として挙げる。
- **レビュアーへの負荷。** [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] は別の議論をしている。エージェントはコードを速く生成するので違反も同じ速さで届き、目視での確認ではレビュアーの負荷が際限なく増える。実行可能なルールによって検証が生成に追いつけるというのがその主張である。[[DefinedTerm/deterministic-quality-gate]] も同様に、レビュアーがテストの通過を手作業で確認する必要がなくなったと報告している。

## ルールの移し先

各ページを通じて、移し先は、ワークフローのどこでルールが成り立たなければならないかによって変わる。

- **ツール呼び出しの前。** Claude Code の `PreToolUse` フックや [[SoftwareApplication/strands-agents]] の `BeforeToolCallEvent` フックは、実行待ちの呼び出しを見てブロックできる。[[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、フックのガードレールとしての価値の大半がこの地点にあるとする。[[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] は、実行前に取り消せばロールバックすべきものが何も残らないと指摘する。
- **ターンまたはサブエージェントの終了時。** `Stop` フックと `SubagentStop` フックは、エージェントと完了の間にテストスイート、ビルド、リンターを挟む（[[DefinedTerm/deterministic-quality-gate]]、[[BlogPosting/writing-a-good-claude-md]]、[[DefinedTerm/agent-hooks]]）。
- **パーミッションシステムと管理設定。** [[BlogPosting/steering-claude-code]] は、組織全体のガードレールを強制する唯一の方法として管理設定（managed settings）を挙げる。[[BlogPosting/claude-code-hooks-complete-guide]] はこれらの層を「`CLAUDE.md` は説得し、パーミッションはふるいにかけ、フックは強制して反応する」と表現し、堅牢な構成では 3 つすべてを動かすとしている。
- **CI。** [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] は、ルールを検査するジョブを必須のステータスチェックにして、違反のあるプルリクエストがマージできないようにする。[[DefinedTerm/deterministic-quality-gate]] は、マージ前に GitHub Action でテストを実行する。
- **アプリケーションのミドルウェア。** [[SoftwareApplication/agent-governance-toolkit]] は、ツール関数を、呼び出しのたびに評価される YAML ポリシーで包む。各判断を監査証跡に書き込み、ポリシーがその操作を拒否すると例外を送出する。

移し先によって、ルールの所有者も異なる。[[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、フックを置く場所をそのスコープとして扱う。個人のセーフティネットにはユーザー設定、チームの標準にはプロジェクトの設定、組織のガードレールには管理ポリシー設定である。

## 各ページが記録している限界

どのページも、この移行を完全なものとしては示していない。各ページは次のような限界を記録している。

- **移されるルールはごく一部である。** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、該当するツール呼び出しのたびにスクリプト起動のコストがかかるため、フックを破壊的なコマンド、シークレット、機密パス、そして 1 つか 2 つの CI/CD 標準に限っている。[[BlogPosting/claude-code-hooks-complete-guide]] は、たまに守られなくても損失の小さい好みまでフック化しすぎることを落とし穴として挙げる。[[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] は、推奨の範囲を影響の大きい操作に限っている。
- **すべてのルールを機械化できるわけではない。** [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] は、その手法が扱えるのはパッケージ構造やクラス間の関係に関する制約であり、自然言語のあらゆるルールではないと明言している。各ルール文書に、どの制約がすでにテストされ、どれがまだレビューに頼っているかを明記させている。[[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] は、そのルールは真偽値であり、曖昧なロジックは表現できないと指摘する。
- **決定論的なチェック自体が誤りうる。** [[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] では、リフレクションを禁じるルールを素直にエンコードしたところ、リフレクション API を一度も呼ばない生成コードまで検出してしまい、書き直す必要があった。同じページは、ルール文書、テスト、コードが互いにずれていく様子を記述し、それらの整合を保つことを未解決の問題として記録している。
- **強制がフェイルオープンになりうる。** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] と [[DefinedTerm/agent-hooks]] は、Claude Code では、不正な JSON を返したフックの応答はパースされないため呼び出しがそのまま通ってしまう一方、`exit 2` は呼び出しをブロックすることを記述している。[[BlogPosting/claude-code-hooks-complete-guide]] は、`1` で終了するガードを、操作を通してしまうため落とし穴の 1 つに挙げている。[[DefinedTerm/agent-hooks]] は、Gemini API がクラッシュまたはタイムアウトしたフックを承認として扱うことを記録している。
- **すべてのフックが強制停止になるわけではない。** [[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、ブロックされた `Stop` を保証ではなく強い後押しと呼ぶ。理由をフィードバックしてモデルに続行を求めるだけだからである。[[DefinedTerm/agent-hooks]] は、Claude Code は 8 回連続でブロックされるとそれでもターンを終了するという Anthropic のドキュメントの記述を記録している。[[DefinedTerm/agent-hooks]] はまた、prompt 型と agent 型のフックは出力の決定にモデルの判断を用いることも記録している。[[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、その種のハンドラーを本質的に非決定論的だと呼んでいる。
- **仕組みそのものが攻撃対象面になる。** フックはユーザーの権限で自動的に実行されるコードである。[[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、悪意ある `SessionStart` フックを仕込んだ PyPI のワームを挙げている。[[BlogPosting/claude-code-hooks-complete-guide]] は、クローンしたリポジトリ内のフックを `Makefile` や `postinstall` スクリプトと同様に扱い、自らの正規表現ベースのガードを完全な境界ではなく多層防御の一部と位置付けている。
- **強制はコードのある場所で行われる。** [[SoftwareApplication/agent-governance-toolkit]] は、自らが強制を行うのは OS カーネルではなくアプリケーションのミドルウェア層であり、ポリシーエンジンとそれが統制するエージェントは同じプロセスを共有していると指摘する。

いくつかのページは、指示にも役割を残している。[[BlogPosting/agentic-coding-hooks-deterministic-ai-guardrails]] は、より良い指示は役に立ち、コンテキスト内のドメイン知識は依然として効果が大きいと述べる。[[BlogPosting/claude-code-hooks-complete-guide]] は、同じ要件を CLAUDE.md、パーミッション、フックが協力して担うようにしている。

## 変形：ルールを強制するのではなく届けるフック

[[BlogPosting/making-ai-follow-team-rules]] は、同じ観察、すなわちルートの指示ファイルにあるルールがセッションが長くなるにつれて守られなくなるという観察から出発する。同じ仕組みである [[DefinedTerm/agent-hooks]] を使うが、使い方が異なる。そのプラグイン [[SoftwareApplication/pfmls-stylepack]] は、ファイルが書き込まれた直後の地点と、エージェントが終了しようとする地点にフックする。それぞれの地点で、該当する規約ルールをいくつか、それが適用されるコードの隣にテキストとして注入する。何もブロックせず、ループ終了時のテキストは自らを強制的な失敗ではなくレビューを促すリマインダーと称している。このページは自らの課題を、ルールを*いつ*、*いくつ*提示するかの問題として捉えている。ここで移動するのは、ルールがコンテキストに入る場所であって、ルールが成り立つかどうかを誰が決めるかではない。

このページは、上記の限界のうち 2 つに突き当たっている。モデルベースの関連性判定ではリクエストごとに約 10 秒が加わったため、フックはファイル名パターンと正規表現でルールを選択している。また、条件が緩く設定されたルールが 21 セッションで発火したにもかかわらず、一度もコード変更につながらなかったことを報告し、誤ったフィードバックはエージェントにルールを無視することを教えてしまうと論じている。

## 証拠の強さ

証拠の大半は、1 つのチームあるいは 1 人の著者による報告である。[[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]] は、2 つの無効ケースと 1 つの有効ケースからなる目的に合わせて作った例で結果を報告しており、それを独立した証拠ではなく具体的な例示だと述べている。[[DefinedTerm/deterministic-quality-gate]] は、2 つのプロジェクトでの 1 人のエンジニアの報告である。[[BlogPosting/verify-ai-agent-coding-rules-with-archunit]] は導入前後の測定値を報告しておらず、[[BlogPosting/making-ai-follow-team-rules]] の数値はそのチーム自身のログに基づく。[[BlogPosting/steering-claude-code]] は自社製品に関する Anthropic のガイダンスである。これをパターンたらしめているのは、別々に書かれた出典に同じ形が繰り返し現れる頻度であり（[[DefinedTerm/agent-hooks]] は他のいくつかのページから編纂されているため例外である）、ルールを移すことが有効だという測定された証拠ではない。
