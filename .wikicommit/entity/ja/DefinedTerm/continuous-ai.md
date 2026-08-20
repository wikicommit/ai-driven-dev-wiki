---
title: "Continuous AI"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェンティックコーディング, 自動化, CI/CD, 用語]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/continuous-ai.md"
source_commit: "1804b4f09d8e8e88510a78cca5839eb041febbe0"
translated_at: "2026-08-20"
translated_by: "claude-opus-5[1m]"

properties:
  description: "AI をソフトウェア開発ライフサイクルに統合し、継続的インテグレーションおよび継続的デプロイの実践と同じように自動化とコラボレーションを高めることに、GitHub が与えた名前。GitHub はこれを既存の CI/CD を置き換えるものではなく補強するものとして提示し、従来の CI/CD では表現しにくいタスクへ継続的な自動化を広げるものだとしている。"
---

Continuous AI は、「AI を SDLC に統合し、継続的インテグレーションおよび継続的デプロイ（CI/CD）の実践と同様に自動化とコラボレーションを高めること」に GitHub が与えた名前である。この語は GitHub 自身のもの——「我々はこれを Continuous AI と呼ぶ」——であり、[[BlogPosting/automate-repository-tasks-with-github-agentic-workflows]] において [[SoftwareApplication/github-agentic-workflows]] とともに、その機能が可能にするものの呼び名として導入された。これは業界で確立された用語ではなくベンダーによる造語であり、この wiki もそのように記録する。

## 用法

CI/CD との類比が定義の実質であり、GitHub はそれをどこまで広げるかについて慎重である。Continuous AI とエージェンティックワークフローは「既存の CI/CD を置き換えるのではなく補強するように設計されている」。ビルド、テスト、リリースのパイプラインを代替するものではなく、GitHub の説明によればそのユースケースは決定論的な CI/CD ワークフローとはほとんど重ならない。GitHub の助言は、Continuous AI を「CI/CD と組み合わせて」用い、Actions の YAML ワークフローの代替とはしないことである。GitHub の説明において、それが加えるものは、このアプローチが「従来の CI/CD では表現しにくい、より主観的で反復的なタスクへ継続的な自動化を広げる」という点にある。

GitHub が例として挙げる6つのカテゴリは、いずれも CI/CD の系譜から「継続的」という接頭辞を借りている。**継続的トリアージ**——新しい Issue を自動的に要約し、ラベルを付け、振り分ける。**継続的ドキュメンテーション**——README とドキュメントをコードの変更に合わせ続ける。**継続的なコードの簡素化**——改善点を繰り返し見つけ、そのためのプルリクエストを開く。**継続的なテストの改善**——カバレッジを評価し、価値の高いテストを追加する。**継続的な品質の衛生管理**——CI の失敗を調査し、的を絞った修正を提案する。そして **継続的なレポーティング**——リポジトリの健全性、活動、傾向についての定期的なレポートを生成する。GitHub の主張は、これらはいずれも「従来の YAML ワークフローだけでは困難あるいは不可能だろう」というものである。

これを他所ではなく GitHub Actions 上で動かす理由として GitHub が挙げるのは、インフラに関するものである。Actions はすでに、パーミッション、ロギング、監査、サンドボックス化された実行、豊かなリポジトリの文脈を提供している場所だからだ。これは定義にとって重要である。GitHub の枠づけにおいて継続的な運用を実用的にするのは、エージェントの能力ではなくその周囲のガードレールだからである——「このようなガードレールがあってこそ、エージェントを一度きりの実験としてではなく継続的に動かすことが実用的になる」。

GitHub は、自社のチームが「ほぼ毎日」新しい使い道を見つけ、自分たちのためのカスタムツールを数分で作り、「雑務を知性で置き換えたり、適切な情報を適切な場所に適切なタイミングで揃えることで人間が仕事を進める道を舗装したりしている」と報告している。これは自社の社内実践についてのベンダーの説明であり、独立した観察ではない。

## 関連用語

GitHub がこれのために出荷している実装が [[SoftwareApplication/github-agentic-workflows]] である。作業を実行するエージェントは [[DefinedTerm/coding-agent]] で、それが収まるより広い実践は [[DefinedTerm/agentic-coding]] と [[DefinedTerm/ai-assisted-software-development]] で扱われている。
