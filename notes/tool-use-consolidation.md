# tool use 関連ページの統合メモ（引き継ぎ用）

作成日: 2026-09-29／ブランチ: `claude/charming-pasteur-f5x6ra`

後日、別のセッションで作業するための現状整理です。このメモの作成時点では、Wiki のページはまだ何も変更していません。

## 1. 問題

「tool use（ツール呼び出し）」という同じ概念について、3 つの DefinedTerm ページが別の名前で存在している。さらに、まだ存在しない 4 つ目の名前へのリンクもある。

| ページ（en / ja とも存在） | 定義の視点 | 被リンク | ソース数 | 行数(en) |
|---|---|---|---|---|
| `DefinedTerm/function-calling` | API の機能として。`aliases: ["Tool calling"]` | 12 | 1 | 64 |
| `DefinedTerm/agentic-tool-use` | エージェントの仕組みとして | 20 | 1 | 91 |
| `DefinedTerm/tool-use-design-pattern` | 設計パターンとして。`aliases` に "Function calling" を含む | 48 | 6 | 275 |
| `DefinedTerm/tool-use` | **未作成**。WANTED（6 ページからリンク） | 6 | – | – |

- 3 ページの定義は実質同じ（ツール定義を渡す → モデルが呼び出しと引数を出力する → アプリが実行して結果を返す）。
- `tool-use-design-pattern` の別名 "Function calling" は `function-calling` のタイトルと衝突している。`check_orphans.py` の重複検出はタイトル同士しか比べないため、検出されていない。
- 独自の内容と言えるのは `tool-use-design-pattern` の「Designing Tools for Agents」節くらい。
- `.wikicommit/schema/DefinedTerm.md:8` のルール「別名や表記ゆれは別ページにせず `aliases` に書く」に反する状態。
- 原因：WikiCommit はソースごとにページを作るため、別々のソースが同じ概念を別の名前で呼ぶと、ページがそのぶん分かれる。

### 未作成リンク `[[DefinedTerm/tool-use]]` のリンク元（6 ファイル）

- `.wikicommit/entity/{en,ja}/DefinedTerm/ai-coding-agent.md`
- `.wikicommit/entity/{en,ja}/DefinedTerm/plan-act-observe-loop.md`
- `.wikicommit/entity/{en,ja}/DefinedTerm/sandboxing.md`

どれも関連用語として名前を並べているだけで、元のソースでも定義されていない。

## 2. 3 ページのソース（重複を除いて 10 件）

- https://arxiv.org/pdf/2604.00835
- https://blog.dagworks.io/p/agentic-design-pattern-1-tool-calling
- https://blog.langchain.com/tool-calling-with-langchain/
- https://docs.aws.amazon.com/prescriptive-guidance/latest/agentic-ai-patterns/tool-based-agents-for-calling-functions.html
- https://docs.claude.com/en/docs/agents-and-tools/tool-use/implement-tool-use
- https://leehanchung.github.io/blogs/2024/05/09/tools-for-llms/
- https://microsoft.github.io/ai-agents-for-beginners/04-tool-use/
- https://platform.openai.com/docs/guides/function-calling
- https://www.anthropic.com/engineering/writing-tools-for-agents
- https://www.deeplearning.ai/the-batch/agentic-design-patterns-part-3-tool-use

## 3. 統合の方針（おすすめ案、未実施）

`DefinedTerm/tool-use`（タイトル "Tool use"）に 1 本化する。

1. `tool-use.md` を en で新しく作る。
   `aliases: ["Tool calling", "Function calling", "Agentic tool use", "Tool use design pattern"]`
2. 3 ページの本文と上の 10 件のソースを統合する。ツール設計の話は 1 つの節として残す。
   DefinedTerm スキーマのルールに従い、特定ベンダーの定義を代表扱いせず、複数の定義は並べて書く。
3. 3 ページへのリンクを `[[DefinedTerm/tool-use]]` に書き換える。
   対象は en/ja 合わせて約 70 ファイル（管理ファイル `.wikicommit/source/` にはリンクなし）。
4. 古い 3 ページ（en/ja）を削除し、ja 版は翻訳し直す。
5. `/wikicommit-merge` のチェック（リンク切れ・重複・ソース整合性）を通す。

書き換えを減らしたい場合は、被リンクが一番多い `tool-use-design-pattern` に寄せる案もある。書き換えは約 30 ファイル減るが、タイトルが「設計パターン」のままで、概念全体の名前としては狭い。

### 注意点

- `aliases` は公開サイトでの検索・表示と、転送ページの生成（`quartz.config.yaml:124` の alias-redirects プラグイン）には効く。
- ただし Wiki 内の `[[Type/slug]]` リンクはファイル名（slug）で相手を探すため、別名を書いてもリンク先にはならない。古いページを消すなら、手順 3 の書き換えが必須。
- WikiCommit にはページ統合の専用機能がないので、手作業で編集する。

## 4. 関連：今回登録したソース（未生成）

`/wikicommit-collect` で次の 15 件を `status: pending` のまま登録済み（コミット済み）。

- tool use 系：codepointer.dev、mathspp.com、jannesklaas.github.io、OpenAI の Programmatic Tool Calling ドキュメント、arXiv の 2605.09252 / 2608.26623 / 2507.21504 / 2511.18538、promptingguide.ai、github.com/zeke-john/codecall
- SASE / SE 3.0 系：arXiv の 2410.06107 / 2507.15003 / 2608.12311 / 2608.02582、ICSE 2026 Technical Briefing

統合を先に済ませてから `/wikicommit-generate` を実行すると、tool use 系のソースは新しい `tool-use` ページへの `update` として取り込まれ、4 つ目・5 つ目の重複ページが生まれにくくなる。arXiv 2511.18538 は非常に長いので、単独で処理すること。
