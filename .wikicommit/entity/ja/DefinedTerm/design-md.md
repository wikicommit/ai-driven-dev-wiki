---
title: "DESIGN.md"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント設定, デザインシステム]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/design-md.md"
source_commit: "07f44d78c36c0f3ef8211927eac4fa818f178ac1"
translated_at: "2026-09-22"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "デザインシステムを AI エージェントが読める形で記述するために Google Labs が 2026 年 4 月に公開したファイルフォーマット。先頭の YAML に機械可読なデザイントークンを、Markdown の本文に人間可読なデザインの意図を置き、結果を lint する CLI を伴う。"
---

`DESIGN.md` は、ユーザーインターフェースを生成する AI エージェントが拠り所とする固定された仕様を持てるよう、
デザインシステムを記述するためのファイルフォーマットである。単一のファイルがその仕様の両半分を収める。すなわち、
先頭の YAML ブロックに置かれる機械可読なデザイントークン——色、タイポグラフィ、スペーシング、コンポーネント——と、
その下の Markdown 本文に置かれる、それらの背後にある人間可読なデザインの意図である。Google Labs は 2026 年 4 月、
`google-labs-code/design.md` というリポジトリからこのフォーマットを公開した。同社の AI による UI 生成プロダクト
Google Stitch のリファレンス実装としてであり、仕様書そのものは Stitch 側で公開されている。

## 用法

このフォーマットをスタイルガイドから区別するのは、チェッカーが同梱されている点である。`npx @google/design.md lint`
として起動される CLI が、`DESIGN.md` をトークン参照の一貫性、WCAG のコントラスト比、そしてフォーマットの構造上の
規約への適合について検証し、その結果を JSON として返す——これが CI で実行してプルリクエストごとに報告することを
可能にしている。付属の `diff` コマンドは 2 つの `DESIGN.md` ファイルを比較し、その間のトークンレベルの変更を
構造化された形で返すことで、デザインシステムのバージョン管理を機械的な基盤の上に置く。

[[BlogPosting/division-of-labor-in-ai-instruction-files]] はこのフォーマットを、AI エージェントに渡される指示ファイルの
3 層のうちの一つ、見た目を担う層として位置づけ、エージェントの前提を担う [[DefinedTerm/agents-md]] と、個々のタスクを
担う `SKILL.md` と並べている。またこれは、同記事が機械可読な内容と人間可読な内容の分離を最も明示的に体現していると
扱う層でもある。フロントマターと本文が両者を混ぜるのではなく別々に担っているからである。同記事の枠組みでは、この
フォーマットの役割は、Figma ファイルやスタイルガイドの PDF に散らばっていたデザインシステムを、両様に読める一つの
ファイルへ集めることにある。

同記事はまた、日本語のインターフェースについての欠落も記録している。日本語に固有のタイポグラフィ要件——CJK
フォントのフォールバック、行の高さ、字間、禁則処理、和欧混植——は Google Labs 自身のサンプルでは定義されておらず、
別のコミュニティリポジトリ（`kzhrknt/awesome-design-md-jp`）が、いくつもの日本のサービスについてそれらを扱う
`DESIGN.md` ファイルを公開している。そこで示されている提案は、どちらか一方だけを使うのではなく両者を併用する
ことである。

ツール類はこのフォーマットを複数ある出力形式の一つとして扱い始めている。同記事は、仕様を `SKILL.md` 形式でも
`DESIGN.md` 形式でも生成・更新できる CLI を挙げ、それを層が別物であるという前提の上に築かれたツールチェーンの
兆候として読んでいる。

## 関連用語

[[DefinedTerm/agents-md]], [[DefinedTerm/agent-skills]], [[DefinedTerm/ai-ide-rules]],
[[DefinedTerm/spec-driven-development]]
