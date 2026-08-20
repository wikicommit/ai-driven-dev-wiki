---
title: "Codex CLI"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェンティックコーディング, CLI, AI支援プログラミング]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/codex-cli.md"
source_commit: "1804b4f09d8e8e88510a78cca5839eb041febbe0"
translated_at: "2026-08-20"
translated_by: "claude-opus-5[1m]"

properties:
  description: "OpenAI が2025年4月にリリースした、コマンドラインインターフェースを備えたエージェンティック AI コーディングツール。AGENTS.md をネイティブに読む。2,926 の GitHub リポジトリを対象とした2026年2月の研究では、これを使うリポジトリが設定をコンテキストファイルより先へ広げることはまれであると見出された。"
  applicationCategory: "エージェンティック AI コーディングツール（CLI）"
  author: "[[Organization/openai]]"
---

Codex CLI は OpenAI による、コマンドラインインターフェースを備えたエージェンティック AI コーディングツールであり、2025年4月に CLI とエージェントを公開時から利用可能な形でリリースされた。[[ScholarlyArticle/configuring-agentic-ai-coding-tools]] はこれを主要なエージェンティックコーディングツール5つのうちの一つとして収録しており、同研究のサンプル 2,926 リポジトリのうち 558 に現れた。著者らは、Codex が同じベンダーの同じモデルを用いたエージェント的ツールであることを理由に、ChatGPT に代えてこれを選んでいる。

Codex は [[SoftwareApplication/claude-code]] とともに、基盤モデルによって舵取りされる中心的なエージェントループを実装した最初期のツールの一つであり、[[SoftwareApplication/github-copilot]] や [[SoftwareApplication/cursor]] といった会話型のツールが同等の能力をエージェントモードとして加えるより前のことであった。

## 概要

Codex を使うリポジトリが設定を [[DefinedTerm/context-files]] より先へ広げることはまれである——この点で研究は Copilot のリポジトリと同じ群に位置づけており、Claude Code の広い設定のフットプリントとは対照的である。リポジトリのメタデータについては、Codex のリポジトリはコミット数とソースサイズの中央値がサンプル全体よりわずかに低かった。

## 機能

Codex は、この研究がカタログ化した8つの設定メカニズムのうち5つについて、リポジトリレベルの成果物を提供している。

- [[DefinedTerm/context-files]] — [[DefinedTerm/agents-md]] および `AGENTS.override.md`
- Settings — `.codex/config.toml`
- [[DefinedTerm/agent-skills]] — `.codex/skills/`
- Rules — `.codex/rules/`
- MCP サーバ — こちらも `.codex/config.toml` 経由で設定

[[DefinedTerm/subagents]]、Commands、Hooks のいずれも提供していない。

## 沿革

2025年5月16日の [[BlogPosting/introducing-codex]] における OpenAI 自身の記述は、CLI が「先月」に「ターミナルで動作する軽量なオープンソースのコーディングエージェント」として公開され、o3 や o4-mini といったモデルをローカルのワークフローへ持ち込んだと述べている。同じ記事は CLI への2つの変更も発表している。ひとつは o4-mini から派生した `codex-1` のより小さな版であり、指示への追従とスタイルを保ちながら低レイテンシのコード Q&A と編集に最適化され、CLI のデフォルトモデルとして、また API では `codex-mini-latest` として公開された。その基となるスナップショットは定期的に更新されるという。もうひとつは、API トークンを手動で生成・設定する代わりに ChatGPT アカウントでサインインできるようにしたことで、API キーは自動的に生成され、あわせて期間限定の無料 API クレジットが Plus ユーザーに5ドル、Pro ユーザーに50ドル提供された。

OpenAI はのちに CLI を単一の製品面へ統合した。Codex の製品ページは、ChatGPT 内の Codex、Codex の IDE 拡張、Codex CLI にまたがって「あなたがコードを書くあらゆる場所で同じエージェント」を提示し、それらはユーザーの ChatGPT アカウントによってつながる。したがって CLI はいまや別個のツールではなく、[[SoftwareApplication/codex]] への3つの入口の一つとして位置づけられている。ローンチ記事はすでにこの方向を見越しており、Codex CLI からタスクを割り当てられるようにすることをロードマップの項目として挙げていた。

Codex CLI は2025年4月にリリースされた。研究は、これがネイティブに読むツール非依存のコンテキストファイルの慣習である AGENTS.md 自体が OpenAI によって導入されたものであることを指摘し、Codex を Cursor とともに、すでに AGENTS.md のネイティブサポートを提供しているツールとして挙げている。著者らは、この慣習がツール横断の標準へと収束していくにつれ、これがベンダーにとって当然の前提になっていくかもしれないと示唆している。
