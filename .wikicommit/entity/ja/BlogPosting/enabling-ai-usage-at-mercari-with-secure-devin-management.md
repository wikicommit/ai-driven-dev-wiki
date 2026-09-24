---
title: "セキュアな Devin 管理によるメルカリでの AI 活用の実現"
type: "schema:BlogPosting"
lang: ja
tags: [エージェント, エージェントセキュリティ, シークレット管理, Infrastructure as Code]
review_status: pending
translated_from: ".wikicommit/entity/en/BlogPosting/enabling-ai-usage-at-mercari-with-secure-devin-management.md"
source_commit: "dd9449729978a2bb341016b5d35f2f19ff11a7a4"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "メルカリの AI Security チームによる、Devin Enterprise を 10 を超える Organization にわたってスケールさせた取り組みの報告。独自の Terraform プロバイダと、Devin の v2・v3 API 上に構築した一連の自動管理ツールによって、メンバーと権限の管理、シークレットのローテーション、API キーのライフサイクル、監査を扱う。"
  author: ["Hiroki Akamatsu"]
  datePublished: "2026-04-03"
  publisher: "[[Organization/mercari]]"
---

この記事が扱うのは、自律型コーディングエージェントが何をするかではなく、それを組織全体に展開した後に必要となる管理面である。メルカリは [[SoftwareApplication/devin]] を社内の複数チームに展開しており、この記事は AI Security のエンジニアが AI Agent Platform チームと共に行った作業を記述したもので、その規模で Devin を運用するために構築したツール群を示している。記事は、企業全体で Devin を安全に展開・運用するための青写真となることを期待していると述べている。

同社が Enterprise プランを採用している理由は、リモート環境で動く AI エージェントを組織規模で運用するための一連の要件として説明されている。すなわち、Okta による SSO、監査ログ、権限管理、そしてチームごとの環境分離である。このプランでは、複数の Organization が 1 つを共有するのではなく Enterprise レイヤーを通じて一元管理される。メルカリは各チームの情報を分離・保護する必要があるため、チームや目的ごとに Organization を割り当てている。

この構成が Organization 数 10 超、多数のユーザーという規模に達すると、3 種類の問題が生じ、記事はそれらを直接挙げている。メンバーの割り当ては手作業に依存し、誰がどこに所属しているかの追跡が難しいこと。サードパーティの認証情報は Organization ごとに個別に設定する必要があり、手作業でのローテーションに時間がかかること。そして Devin は API キーの有効期限管理を標準機能として提供していないため、長期間ローテーションされないキーが蓄積するリスクがあること。状況を変えたのは、Devin が 2025 年後半に Enterprise API v3 をリリースし、ほとんどの管理操作が自動化可能になったことである。そこでチームは Go と GitHub Actions で社内の管理プラットフォームを構築した。

## 要点

- 管理プラットフォームの中核は独自の Terraform プロバイダであり、Terraform Plugin Framework で構築された。Terraform がメルカリにおける Infrastructure as Code の標準であり、公式の Devin プロバイダが存在しないためである。記事が述べる利点は、Devin を IaC で管理することでメンバー追加や権限変更に PR レビューが挟まり、Organization とメンバーの状態がコードとして可視化されることであり、`terraform plan` によって誰がどの Organization に追加・削除されるかを実行前に確認できる。
- ACU（Agent Compute Unit）の上限も同じ Terraform 定義の中で設定され、チームごとの使用量を制御する。`max_cycle_acu_limit` は Organization 全体を、`max_session_acu_limit` は単一セッションを上限づけるもので、記事はこれを予期しないコスト超過の防止と位置づけている。
- プロバイダは Devin Knowledge も管理する。記事によれば、これは Devin の中で Agent Skills と同様に機能するものである。記事は自らの分離がもたらした緊張関係を指摘している。各チームは別々の Organization に属し互いの利用状況を見られないため、実践的なノウハウの共有が難しく、Knowledge をプロバイダで管理可能にしたことで、そのノウハウをチーム横断で配布できるようになった。
- シークレットは Organization ごとではなく一括でローテーションされる。Devin はセッションごとに独立した仮想マシンを起動するため、ソースコード管理以外のものに接続するには個別に設定された認証情報が必要となる。記事が述べるリスクは、AI エージェントは与えられた API キーを自由に使えること、そして Organization 内のメンバーはセッション内のファイルシステムやシェルにアクセスできることであり、そのためメルカリはそれらのキーを一元管理し、短い間隔でローテーションしている。手順は次のとおりである。管理者が各サービスで認証情報をローテーションし、新しい値を Google Cloud Secret Manager に格納し、GitHub Actions が自動化処理を起動し、ローテーション処理がそれらをすべての Organization に配布する。新しい Organization が作成されても追加の手間はかからない。
- Google Cloud のサービスアカウントキーは意図的な例外として扱われる。Devin には Workload Identity Federation を利用可能にする OIDC トークン発行機能がないため、サービスアカウントキーが必要となる。一方でメルカリは Organization Policy により全社的にその発行を禁止している。解決策は、そのポリシーから除外した専用の Google Cloud プロジェクトを用意し、補償的統制として `iam.serviceAccountKeyExpiryHours` を設定することであった。これにより、自動化が停止してもキーは一定期間後に自動的に無効化される。
- 監査ログは v3 の Enterprise Audit Logs エンドポイント（ページネーションがあるため v2 のエンドポイントではなくこちらが選ばれた）を通じて Cloud Run Job によって取得され、新しいログが PubSub トピックに転送され、そこから分析されて BigQuery に保存される。社内のセキュリティ監視基盤とのこの連携は、Threat Detection and Response チームと協働する同僚の功績とされており、監査ログはそもそも Devin Enterprise を採用する要件の 1 つとして挙げられている。
- API キーの有効期限は、Devin が提供しないため自動化によって強制される。あるジョブが Enterprise 全体のすべてのキーを取得し、所定の期間を超えたものを無効化する。記事が述べる動機は、これらのキーが主に Devin MCP への接続に使われ、それを通じてソースコードを間接的に取得できること、そして複数のエージェントがある環境では、使われていないエージェントの設定に認証情報が残り続けたり、社内で共有されるカスタムエージェントに個人のキーとして設定されたりしうることである。
- Devin Wiki は、チームごとの開発用 Organization とは別の専用の Organization で動作し、Devin MCP を通じてリポジトリ内容の取得や自然言語での検索を可能にしている。ソースコードの探索をこれに委ねる理由として記事が挙げるのはコンテキストの節約であり、AI エージェントがソースコードを直接探索すると大量のコンテキストを消費するからである。有効期限の自動化は社内エージェントが必要とするキーまで無効化してしまうため、別の自動化がそれらのキーを短い間隔で再作成して Google Cloud Secret Manager に保存し、特定のエージェントのサービスアカウントに Terraform でアクセス権を付与している。
- すべては Google Cloud ではなく GitHub Actions 上で動作しており、記事はその理由として保守性を挙げている。リポジトリ内の自動化はデプロイなしで動き、クラウドリソースを持たないことでコストを低く抑え引き継ぎ時の心理的負担を減らせ、組織変更を経ても長期的に保守していくには依存を小さくすべきだという。定期実行に加えて、緊急時に即座にローテーションするための `workflow_dispatch` も用意されている。Actions は自由に実行できてしまうため、チームは権限とブランチ保護を厳格に設定し、サービスアカウントや Secret Manager へのアクセスには Google Cloud Workload Identity Federation を用いている。
- v2 API を使うのは API キー管理のみであり、v3 API は Enterprise と Organization の両レベルでメンバー、ロール、シークレット、ナレッジをカバーする。記事は v3 API に Enterprise 管理に必要なエンドポイントがすでに揃っていると報告しており、Devin の機能拡張に合わせて、より広範なリソースの安全な管理を引き続き自動化していく意向を述べている。

## 背景

この記事はベンダーではなく運用者の立場から書かれており、記述されている仕組みの大半は、標準機能が存在しないがゆえに存在している。公式のものがないから Terraform プロバイダがあり、Devin が有効期限管理を提供しないからキーの有効期限ジョブがあり、Devin が OIDC トークンを発行できないからサービスアカウントキーの例外がある。記事全体を通じた枠組みは、Enterprise プランの管理要件は標準機能だけではカバーしきれず、独自ツールで補ったというものである。

記事は成果の測定値を報告しておらず、代わりに以前は手作業だったものが今は自動化されていることを記述している。記事は特定の選択の根拠として Devin の公式 API ドキュメントと、サービスアカウントキーに関する Google Cloud 自身のベストプラクティスのガイダンスに言及し、また同社の検知エンジニアリング基盤についての以前の記事にも触れているが、いずれについても自らの説明の中で果たす役割以上のことは述べていない。
