---
title: "Chrome DevTools MCP"
type: "schema:SoftwareApplication"
lang: ja
tags: [MCP, コーディングツール]
translated_from: ".wikicommit/entity/en/SoftwareApplication/chrome-devtools-mcp.md"
source_commit: "62375f91cd50b55903e4c7e317338dbf1f45f8fe"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "AI コーディングエージェントに、実際に動作しているブラウザ ― DOM、パフォーマンストレース、コンソールログ、ネットワークトレース ― への直接アクセスを与える MCP 連携。これにより、静的なコードだけでなく実行時のデータからバグを診断できるようになる。"
---

Chrome DevTools MCP は、ブラウザが見ているものを AI ツールにも見えるようにする [[DefinedTerm/model-context-protocol]] の連携である。エージェントに、DOM を調べたり、詳細なパフォーマンストレース、コンソールログ、ネットワークトレースを取得したりするための直接アクセスを与えるもので、[[BlogPosting/my-llm-coding-workflow-going-into-2026]] ではエージェントに「目」を与えるものと表現されている。ソースコードは GitHub の <https://github.com/chromeDevTools/chrome-devtools-mcp> にある。

## 機能

その目的は、静的なコード解析と実際のブラウザでの実行とのあいだのギャップを埋めることにある。ブラウザの実行時データをエージェントに公開することで、その情報を伝えるために人間が手作業でコンテキストを切り替える手間をなくし、UI テストを LLM を通じて直接自動化できるようにする。これにより、実際の実行時データに基づいてバグを診断・修正できるようになる。

## 採用とエコシステム

かつて自身のチームがこれを開発した Addy Osmani は、AI エージェントとともにコーディングする際のデバッグと品質のループの一部として、これを使っていると述べている。
