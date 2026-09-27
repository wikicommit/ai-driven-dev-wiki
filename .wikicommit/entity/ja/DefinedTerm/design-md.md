---
title: "DESIGN.md"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント設定, デザインシステム]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/design-md.md"
source_commit: "07f44d78c36c0f3ef8211927eac4fa818f178ac1"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "デザインシステムを AI エージェントが読める形で記述するために、Google Labs が 2026 年 4 月に公開したファイル形式。機械可読なデザイントークンを先頭の YAML に、人間が読むデザインの意図を Markdown 本文に記述し、その結果を lint する CLI を備える。"
---

`DESIGN.md` は、ユーザーインターフェースを生成する AI エージェントが拠り所とする確定した仕様を持てるよう、デザインシステムを記述するためのファイル形式である。1 つのファイルがその仕様の両面を保持する。色、タイポグラフィ、余白、コンポーネントといった機械可読なデザイントークンを先頭の YAML ブロックに、その背後にある人間が読むためのデザインの意図をその下の Markdown 本文に記述する。Google Labs は 2026 年 4 月、`google-labs-code/design.md` という名前のリポジトリから、同社の AI による UI 生成製品 Google Stitch のリファレンス実装としてこの形式を公開した。仕様書そのものは Stitch 側で公開されている。

## 用法

この形式をスタイルガイドと区別するのは、チェッカーが同梱されている点である。`npx @google/design.md lint` として呼び出す CLI は、`DESIGN.md` についてトークン参照の整合性、WCAG のコントラスト比、形式の構造上の規約への適合を検証し、結果を JSON で返す。これにより CI で実行し、プルリクエストごとに報告することが可能になる。付属の `diff` コマンドは 2 つの `DESIGN.md` ファイルを比較し、両者のトークンレベルの差分を構造化された形で返すことで、デザインシステムのバージョン管理を機械的な基盤に乗せる。

[[BlogPosting/division-of-labor-in-ai-instruction-files]] は、この形式を AI エージェントに渡す指示ファイルの 3 つの層の一つ、すなわち見た目を担う層として位置づけている。残りの 2 つは、エージェントの前提を担う [[DefinedTerm/agents-md]] と、個々のタスクを担う `SKILL.md` である。同記事はまた、この層を、機械可読な内容と人間が読む内容が最も明確に分かれている層として扱っている。フロントマターと本文がそれぞれを別々に担い、両者を混在させないためである。同記事の捉え方では、この形式の役割は、Figma ファイルやスタイルガイドの PDF に散らばっていたデザインシステムを、どちらの読み手にも読める 1 つのファイルにまとめることにある。

同記事は、日本語のインターフェースについての欠落も記録している。日本語特有のタイポグラフィ上の要件 — CJK フォントのフォールバック、行の高さ、字間、改行規則、和欧混植 — は Google Labs 自身のサンプルでは定義されておらず、別のコミュニティリポジトリ（`kzhrknt/awesome-design-md-jp`）が、いくつかの日本のサービスについてそれらを扱った `DESIGN.md` ファイルを公開している。同記事での提案は、どちらか一方だけでなく両者を併用することである。

ツール側も、この形式を複数ある出力の一つとして扱い始めている。同記事は、仕様を `SKILL.md` と `DESIGN.md` のいずれの形式でも生成・更新できる CLI を挙げ、それを各層が別個のものであるという前提に立ったツールチェーンの兆しと読んでいる。

## 関連用語

[[DefinedTerm/agents-md]]、[[DefinedTerm/agent-skills]]、[[DefinedTerm/ai-ide-rules]]、[[DefinedTerm/spec-driven-development]]
