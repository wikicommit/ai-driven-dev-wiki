---
title: "カスタムエージェント（GitHub Copilot）"
type: "schema:DefinedTerm"
lang: ja
aliases: ["Copilot custom agents", "Copilot カスタムエージェント", "Agent profile", "エージェントプロファイル"]
tags: [コーディングエージェント, エージェント設定]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/github-copilot-custom-agents.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "リポジトリに保存された Markdown のエージェントプロファイルによって定義される Copilot エージェント。プロファイルはエージェントの役割、使用してよいツール、従うべきガードレールを指定し、どこで実行しても同じように振る舞うようにする。"
---

[[SoftwareApplication/github-copilot]] におけるカスタムエージェント（custom agent）とは、汎用的な振る舞いに頼るのではなく、Markdown ファイル — エージェントプロファイル（agent profile） — によって定義される Copilot エージェントである。プロファイルには、エージェントの役割と専門領域、アクセスできるツール、従わなければならない標準とガードレール、そして生成すべき出力が記述され、その結果としてエージェントはどこで実行しても一貫して振る舞うとされる。GitHub はこれを、汎用のコーディングエージェントを専門化されたエージェントに変える方法として位置づけている。汎用エージェントならコードの整理方法を提案するにとどまるかもしれないところを、カスタムエージェントはチーム独自のフォーマットルール、ツール、アクセシビリティ標準、レビュー要件、安全要件を毎回適用する。

## 使われ方

エージェントプロファイルは、YAML フロントマター — `name`、`description`、`tools`、そして GitHub の例の 1 つでは `model` といったフィールド — に続けてエージェントへの指示を記述した Markdown ファイルである。[[SoftwareApplication/github-copilot-cli]] では、プロファイルはファイル名が `.agent.md` で終わる形でリポジトリの `.github/agents` ディレクトリに追加され、エージェントは `/agent` スラッシュコマンドで選択される。プロファイルがリポジトリ内に置かれるため、チームはそれをコードと同じようにレビューし、バージョン管理し、共有できる、というのが GitHub の説明である。これにより、同じ期待がターミナルから IDE、そしてプルリクエストへと作業に付いていく。

GitHub は、チームが自ら書くカスタムエージェントと、JFrog、Dynatrace、Octopus Deploy、Arm などのパートナーと共に構築された既製のエージェントとを区別している。最小限のセットアップで動作するエージェントを試したい場合や、特定ツールのベストプラクティスを得たい場合にはパートナーエージェントを、チームの規約、社内ツール、正確な技術スタックに毎回従わせる必要がある場合にはチーム独自のカスタムエージェントを勧めており、チームはしばしばパートナーエージェントから始めてそれを調整すると付け加えている。この仕組みに適したワークフローの例として挙げられているのは、セキュリティ監査、Infrastructure as Code のコンプライアンスレビュー、リリースノート、インシデントの一次調査レポートである（[[BlogPosting/custom-agents-in-github-copilot-cli]]）。
