# 企業の人事データの置き場と、外から読める API

## 結論

- 従業員、組織、勤怠は、調べた多くのサービスで API から読める。給与と評価は、読めるサービスと読めないサービスに分かれる。
- 権限の形は 2 つある。人に紐づく OAuth(その人の権限を引き継ぐ)と、管理者が発行するトークン(サービス用の利用者)だ。
- 2026 年に MCP が広がった。Workday は一般提供、freee は公開済み、BambooHR と HiBob はベータや段階的な提供の段階にある。
- 項目や対象者で絞れるのは HiBob、SmartHR、Rippling など一部だ。統合 API(Merge、Finch)は「データの種類」単位で、粗い。
- API の操作が監査ログに残ると公開文書で確かめられたのは、SAP SuccessFactors と Merge Agent Handler だけだった。Workday は会社の発表で「監査の記録に従う」としている。

## 比べる表

| サービス | 国 | API で読める主なデータ | 認証 | スコープの細かさ | API の監査ログ | MCP、AI と提供の段階 | 出典 | 見た日 |
|---|---|---|---|---|---|---|---|---|
| SmartHR | 国内 | 従業員、部署、役職、雇用形態など | アクセストークン(管理者が発行)、OAuth(SmartHR Plus 経由) | エンドポイントごとに参照/更新、従業員項目ごとの許可 | 見つからなかった | 公式 MCP は見つからなかった。AI エージェントは 2026 年度に提供の計画(報道) | https://developer.smarthr.jp/api/about_api | 2026-11-11 |
| freee人事労務 | 国内 | 従業員、勤怠、給与明細、賞与明細、年末調整、部門、役職、申請 | OAuth 2.0 | アプリの権限と利用者の権限の組み合わせ。多くの API は管理者のみ | 見つからなかった | 公式 freee-mcp を公開(ローカル版 2026-03、リモート版 2026-03) | https://github.com/freee/freee-mcp | 2026-11-11 |
| KING OF TIME | 国内 | 従業員、所属、日別/月別勤怠、打刻、休暇、申請 | アクセストークン(Bearer)。給与連携では OAuth にも対応 | 連携希望項目とエンドポイントの対応表がある | 見つからなかった | 見つからなかった | https://developer.kingoftime.jp/ | 2026-11-11 |
| カオナビ | 国内 | メンバー基本情報、シート、所属ツリー、ユーザー、ロール | Consumer Key/Secret からアクセストークン | 見つからなかった | API 実行結果を管理画面で確認できる | 公式 MCP は見つからなかった | https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933 | 2026-11-11 |
| Workday HCM | 海外 | コア HR、給与、勤怠、タレント、採用など | 公開文書では確かめられなかった | 利用者の Workday の権限を引き継ぐ(会社の発表) | 監査の記録に従う(会社の発表) | Agent-Ready Tools(MCP)一般提供 2026-10-13 | https://en-sg.newsroom.workday.com/2026-10-13-Workdays-Trusted-Agent-Platform-Now-Delivers-Headless-Access-to-HR-and-Finance,-Letting-Customers-Build-and-Run-Lawful-AI-Agents | 2026-11-11 |
| SAP SuccessFactors | 海外 | Employee Central ほか(OData API) | OAuth 2.0 ほか | ロールごとの権限(RBP)。ただし抜け道の権限がある | OData API Audit Log あり | Joule の Assistant を 2026 年後半に提供。公式 MCP は見つからなかった | https://userapps.support.sap.com/sap/support/knowledge/en/2639949 | 2026-11-11 |
| BambooHR | 海外 | 従業員、休暇、目標、採用、レポート | 利用者ごとの API キー、OAuth | 利用者の権限と同じ。OAuth はスコープあり | 見つからなかった | 公式 MCP とClaude コネクタがベータ(2026-10-08 発表) | https://documentation.bamboohr.com/docs/mcp-server | 2026-11-11 |
| Rippling | 海外 | 従業員、報酬、勤怠、休暇、採用、評価、部署 | API トークン(Bearer) | オブジェクトごとのスコープ × 作った人の権限 | 見つからなかった(トークンの最終利用日時は見える) | Rippling AI(段階不明)。Rippling MCP の記載あり(段階不明) | https://developer.rippling.com/documentation/rest-api/essentials/api-tokens | 2026-11-11 |
| HiBob | 海外 | 人事データ、休暇、勤怠、評価、目標、報酬など | サービス用の利用者(ID とトークン)、MCP は OAuth | 機能、項目ごとの閲覧/編集、対象者の範囲 | 見つからなかった | 公式 MCP。OAuth 版を 2026-06 から段階的に提供 | https://apidocs.hibob.com/docs/api-service-users | 2026-11-11 |
| Merge(統合 API) | 海外 | 従業員、雇用、グループ、休暇、給与の実行、勤務表など | API キーと Linked Account ごとのトークン | Common Model(データの種類)単位 | Agent Handler は呼び出しの監査記録あり | Agent Handler(MCP 対応) | https://docs.merge.dev/merge-agent-handler | 2026-11-11 |
| Finch(統合 API) | 海外 | 会社、従業員名簿、個人、雇用、支払い、給与明細 | 雇用主の管理者が Finch Connect で許可 | 製品(データの種類)単位。SSN は別のスコープ | 見つからなかった | 公式 MCP は公式文書で確かめられなかった | https://developer.tryfinch.com/implementation-guide/Connect/Set-Up-Finch-Connect | 2026-11-11 |

## 国内のサービス

### SmartHR

- 対象: 企業向け(人事労務、従業員データベース)。
- AI とエージェントでしていること: 2026 年度に「従業員向け」と「バックオフィス向け」の 2 つの AI エージェントを提供する計画を示した（出典: https://cloud.watch.impress.co.jp/docs/news/2123332.html、見た日 2026-11-11）(報道)。人事部門向けの「AI HRBP」も予定と報じられた。時期は書かれていない（出典: https://cloud.watch.impress.co.jp/docs/news/2123332.html、見た日 2026-11-11）(報道)。
- 提供の段階: AI エージェントは「発表のみ」。公式の MCP サーバーは見つからなかった。
- 権限とデータの扱い:
  - API はアクセストークンで認証する。発行は管理者だけができる（出典: https://developer.smarthr.jp/api/about_api、見た日 2026-11-11）。
  - 上限はトークンごとに 1 時間 5,000 回、毎秒 10 回。サブドメインごとに 1 分 50,000 回（出典: https://developer.smarthr.jp/api/about_api、見た日 2026-11-11）。
  - トークンにはエンドポイントごとに参照(Read)や更新(Write)を割り当てる。Okta の例では `/api/v1/crews` だけが読み書き、ほかは読み取りだ（出典: https://help.okta.com/wf/en-us/content/topics/workflows/connector-reference/smarthr/overviews/authorization.htm、見た日 2026-11-11）。
  - 公式ヘルプの見出しには「リソースのアクセス許可」「従業員項目のアクセス許可」「参照と更新の違い」がある。本文はログインが要るので読んでいない（出典: https://support.smarthr.jp/ja/help/articles/360026266033/、見た日 2026-11-11）。
  - OAuth の連携もある。マネーフォワード Admina は SmartHR Plus 経由の OAuth を勧めている。OAuth では、連携したアカウントの権限グループが見せる範囲だけが同期される（出典: https://support.i.moneyforward.com/en/integrations/zyl6g8sbgx-smart-hr.md、見た日 2026-11-11）。
  - 同じ文書は、SmartHR が 2026 年 8 月ごろに権限を「本人」と「他人」に分ける予定だと書く。見えない項目はエラーを出さずに同期が止まる（出典: https://support.i.moneyforward.com/en/integrations/zyl6g8sbgx-smart-hr.md、見た日 2026-11-11）。
  - API の操作が監査ログに残るかは、公開ページでは確かめられなかった。

### freee人事労務

- 対象: 企業向け(人事労務、勤怠、給与)。
- AI とエージェントでしていること: 公式の MCP サーバー「freee-mcp」がある。人事労務も対象で、従業員、勤怠、給与明細、年末調整の手順書(skill)を含む（出典: https://github.com/freee/freee-mcp、見た日 2026-11-11）。勧める使い方は、freee が運営するリモート版 `https://mcp.freee.co.jp/mcp` だ（出典: https://github.com/freee/freee-mcp、見た日 2026-11-11）。人事評価などはリモート版だけで使える（出典: https://github.com/freee/freee-mcp、見た日 2026-11-11）。
- 提供の段階: OSS 版は 2026-03-02、リモート版は 2026-03-27 に発表された（出典: https://digitalpr.jp/r/132795、見た日 2026-11-11）(会社の発表)。推測: ベータの表記は見当たらず、一般提供に近い。
- 権限とデータの扱い:
  - API は OAuth 2.0 の Bearer トークンで認証する（出典: https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json、見た日 2026-11-11）。
  - 読めるデータの種類: 従業員(住所、健康保険、厚生年金、家族、銀行口座、基本給、手当)、勤怠と打刻、給与明細、賞与明細、年末調整、所属、部門、役職、各種の申請（出典: https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json、見た日 2026-11-11）。
  - 多くのエンドポイントは「管理者権限を持ったユーザーのみ実行可能」だ。上限は 1 時間 10,000 回（出典: https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json、見た日 2026-11-11）。
  - freee-mcp は OAuth 2.0(PKCE)を使う。ローカル版はアプリ登録の時に「必要な権限にチェック」する（出典: https://github.com/freee/freee-mcp、見た日 2026-11-11）。
  - 画面側では、2025-02-28 から機能ごとに権限を決める「カスタム権限機能」がある。例は「全従業員の情報を閲覧のみ」だ（出典: https://digitalpr.jp/r/104908、見た日 2026-11-11）(会社の発表)。部署ごとや項目ごとに絞れるかは書かれていない。
  - OAuth のスコープの一覧と、API の監査ログは見つからなかった。

### KING OF TIME(勤怠)

- 対象: 企業向け(勤怠)。
- AI とエージェントでしていること: 見つからなかった。
- 提供の段階: API は提供中。MCP と AI エージェントは見つからなかった。
- 権限とデータの扱い:
  - 読めるデータ: 従業員、所属、雇用区分、日別勤怠、打刻、日別/月別の人件費、休暇の残り、スケジュール、管理者、申請（出典: https://developer.kingoftime.jp/、見た日 2026-11-11）。
  - 書けるデータ: 従業員(登録、更新、削除)、打刻、日別スケジュール、申請の承認と却下（出典: https://developer.kingoftime.jp/、見た日 2026-11-11）。
  - 認証は Bearer のアクセストークン。発行は「各サポートセンターへお問い合わせください」とある（出典: https://developer.kingoftime.jp/、見た日 2026-11-11）。
  - 文書に「連携希望項目とエンドポイントの対応」の表がある。推測: トークンごとに使える項目を選ぶ形。
  - 8:30-10:00 と 17:30-18:30 は、トークンと打刻以外の API が使えない（出典: https://developer.kingoftime.jp/、見た日 2026-11-11）。
  - マネーフォワード クラウド給与との連携は、2026-01-27 に OAuth 方式に対応した（出典: https://biz.moneyforward.com/support/payroll/news/new-feature/20260127.html、見た日 2026-11-11）。
  - API の監査ログは見つからなかった。

### カオナビ(タレントマネジメント)

- 対象: 企業向け(人材データ、評価)。
- AI とエージェントでしていること: 公式の MCP サーバーと AI エージェントは見つからなかった。
- 提供の段階: 公開 API v2 は提供中。2025 年 4 月の時点で無償だ（出典: https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933、見た日 2026-11-11）(資料の日付 2025-04-01)。
- 権限とデータの扱い:
  - 画面で Consumer Key と Consumer Secret を確かめ、アクセストークンを取ってから API を呼ぶ（出典: https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933、見た日 2026-11-11）。
  - 操作できる機能: 基本情報(メンバー)、顔写真(登録と更新のみ)、シート、所属ツリー、ユーザー、ロール(取得のみ)、マスター、Webhook、拡張アクセス設定（出典: https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933、見た日 2026-11-11）。
  - 「スマートレビューやボイスノートなど、他の機能については API で操作できません」とある（出典: https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933、見た日 2026-11-11）。評価の流れそのものは API の外にある。推測: 評価の結果をシートに入れていれば、シートとして読める。
  - 上限は 1 時間 3,000 回。API の実行結果は管理者メニューで確かめられる。Dry-Run で検証もできる（出典: https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933、見た日 2026-11-11）。
  - API キーをシートや項目、所属で絞れるかは見つからなかった。

## 海外のサービス

### Workday HCM

- 対象: 企業向け(人事、給与、勤怠、タレント、採用)。
- AI とエージェントでしていること: Agent-Ready Tools は MCP の上に作った接続の仕組みだ。MCP に対応したエージェントが Workday のデータを読み、操作できる（出典: https://www.workday.com/en-us/ai-platform/agent-tools-mcp.html、見た日 2026-11-11）。対象の領域は、コア HR、財務、労務管理、タレントと学習、給与、採用などだ（出典: https://www.workday.com/en-us/ai-platform/agent-tools-mcp.html、見た日 2026-11-11）。Data Cloud の Live Data Query では、エージェントが SQL で生のデータを引ける（出典: https://en-sg.newsroom.workday.com/2026-10-13-Workdays-Trusted-Agent-Platform-Now-Delivers-Headless-Access-to-HR-and-Finance,-Letting-Customers-Build-and-Run-Lawful-AI-Agents、見た日 2026-11-11）。
- 提供の段階: 2026-10-13 に Agent-Ready Tools、Data Cloud、Developer Agent、Custom Agents、Agent Harness が一般提供になった。Agent Context Service は 2026 年末から早期提供だ（出典: https://en-sg.newsroom.workday.com/2026-10-13-Workdays-Trusted-Agent-Platform-Now-Delivers-Headless-Access-to-HR-and-Finance,-Letting-Customers-Build-and-Run-Lawful-AI-Agents、見た日 2026-11-11）(会社の発表)。
- 権限とデータの扱い:
  - どのエージェントも「同じ Workday の権限、承認、監査の記録」の下で動くとしている（出典: https://en-sg.newsroom.workday.com/2026-10-13-Workdays-Trusted-Agent-Platform-Now-Delivers-Headless-Access-to-HR-and-Finance,-Letting-Customers-Build-and-Run-Lawful-AI-Agents、見た日 2026-11-11）(会社の発表)。
  - 操作は利用者の ID の範囲に絞るとしている（出典: https://www.workday.com/en-us/ai-platform/agent-tools-mcp.html、見た日 2026-11-11）。
  - API の認証方式、統合用の利用者、監査ログの形式は、ログインが要る文書にあり、確かめられなかった。

### SAP SuccessFactors

- 対象: 企業向け(人事、給与、タレント、採用)。
- AI とエージェントでしていること: 2026 年後半のリリースで、Joule の Assistant を並べた。Payroll Assistant(給与の異常を見つける)、HR Operations Assistant(データの問題を直し、変更を自動化)、HR System Assistant(監査の準備)などだ（出典: https://news.sap.com/2026/10/sap-successfactors-2h-2026-release/、見た日 2026-11-11）(会社の発表)。
- 提供の段階: そのページには提供の段階が書かれていない。「2026 年後半を通して届ける」とだけある（出典: https://news.sap.com/2026/10/sap-successfactors-2h-2026-release/、見た日 2026-11-11）。公式の MCP サーバーは見つからなかった。
- 権限とデータの扱い:
  - OData API はロールごとの権限(RBP)に従う。ただし API の利用者に「Employee Central HRIS OData API (read-only)」の権限があると、RBP の確認を飛ばして全データを返す（出典: https://userapps.support.sap.com/sap/support/knowledge/en/2639949、見た日 2026-11-11）。
  - OData API Audit Log がある。どの連携が変更したかを、システム名、IP アドレス、プロセス名で追える（出典: https://userapps.support.sap.com/sap/support/knowledge/en/3632123、見た日 2026-11-11）。

### BambooHR

- 対象: 企業向け(中小の人事、休暇、採用)。
- AI とエージェントでしていること: 公式の MCP サーバーと、その上の Claude コネクタがある。人事の管理者は保存したレポートや人数、採用を見られる。社員は休暇の残りや申請、同僚の検索ができる（出典: https://www.bamboohr.com/about-bamboohr/press-release/bamboohr-announces-claude-connector-built-on-bamboohr-mcp、見た日 2026-11-11）(会社の発表)。
- 提供の段階: ベータ。2026-10-08 の発表では公開ベータ(open beta)としている（出典: https://www.bamboohr.com/about-bamboohr/press-release/bamboohr-announces-claude-connector-built-on-bamboohr-mcp、見た日 2026-11-11）。文書は「beta」で、参加者に接続用の資格情報を渡す形だ（出典: https://documentation.bamboohr.com/docs/mcp-server、見た日 2026-11-11）。
- 権限とデータの扱い:
  - API キーは利用者ごとに発行する。API の操作は、その利用者自身の操作と同じ権限になる（出典: https://documentation.bamboohr.com/docs/getting-started、見た日 2026-11-11）。
  - 連携アプリは OAuth を使う。トークンは 3600 秒で切れる。スコープを指定するが、一覧はそのページにない（出典: https://documentation.bamboohr.com/docs/getting-started、見た日 2026-11-11）。
  - MCP は OAuth 2.0 で守られる。利用者は要求の内容を見て承認する。アシスタントは利用者が見られる範囲を超えない（出典: https://documentation.bamboohr.com/docs/mcp-server、見た日 2026-11-11）。
  - MCP のツールは 11 の領域にわたる。多くは読み取りだが、従業員の更新や休暇の申請もできる。目標とコメントの削除もある（出典: https://documentation.bamboohr.com/docs/mcp-server、見た日 2026-11-11）。
  - API や MCP の操作の監査ログは見つからなかった。

### Rippling

- 対象: 企業向け(人事、給与、IT、経費をまとめたもの)。
- AI とエージェントでしていること: Rippling AI は、実際の Rippling のデータで質問に答え、作業をする。レポートを作り、社員ごとの給与や福利厚生を説明する（出典: https://www.rippling.com/ai、見た日 2026-11-11）。同じページで「Rippling MCP」を、外の AI ツールに Rippling の文脈を渡す手段として紹介している（出典: https://www.rippling.com/ai、見た日 2026-11-11）。
- 提供の段階: Rippling AI は「Try it now」がある。AI の自動化は順番待ち(waitlist)だ（出典: https://www.rippling.com/ai、見た日 2026-11-11）。MCP の段階は不明。
- 権限とデータの扱い:
  - API で読めるのは、従業員、報酬、勤怠、休暇、採用、人員計画、評価、部署、拠点、独自項目、レポートなど。給与(payroll)は分類に出てこない（出典: https://developer.rippling.com/documentation/rest-api、見た日 2026-11-11）。
  - トークンが読めるのは「作った人の権限」と「トークンのスコープ」の両方で許されたデータだけだ（出典: https://developer.rippling.com/documentation/rest-api/essentials/api-tokens、見た日 2026-11-11）。
  - スコープはオブジェクトごとに分かれる。`workers.read`、`compensations.read`、`time-entries.read-write` などだ。従業員(workers)と報酬には書き込みのスコープがない（出典: https://developer.rippling.com/documentation/rest-api/essentials/permissions、見た日 2026-11-11）。
  - 権限がない値は null で返る（出典: https://developer.rippling.com/documentation/rest-api/essentials/api-tokens、見た日 2026-11-11）。
  - トークンは、持ち主が退職するか 30 日使われないと自動で無効になる。発行時には持ち主と管理者に通知が飛ぶ。「最終利用日時」も見える（出典: https://developer.rippling.com/documentation/rest-api/essentials/api-tokens、見た日 2026-11-11）。
  - Rippling AI は既存の権限を引き継ぐ。操作の前に人の確認を求める（出典: https://www.rippling.com/ai、見た日 2026-11-11）。
  - API 呼び出しの監査ログは見つからなかった。

### HiBob

- 対象: 企業向け(中堅の人事)。
- AI とエージェントでしていること: 公式の MCP サーバーがある。人事データ、組織、休暇、タスク、承認、勤怠、評価、目標、学習、採用、報酬を扱える(機能が有効で、社員に権限がある場合)。読み書きの両方ができる（出典: https://www.hibob.com/mcp-beta、見た日 2026-11-11）。
- 提供の段階: 2026-04-28 にサービス用の利用者で使うホスト版を出した。2026-06 に OAuth 版の段階的な提供を始めた（出典: https://apidocs.hibob.com/docs/hibob-mcp-server、見た日 2026-11-11）。2026-11-09 から、サービス用の利用者での新しい接続を止めている（出典: https://apidocs.hibob.com/docs/hibob-mcp-server、見た日 2026-11-11）。
- 権限とデータの扱い:
  - API はサービス用の利用者(ID とトークン)で使う。最初は権限が何もない（出典: https://apidocs.hibob.com/docs/api-service-users、見た日 2026-11-11）。
  - 権限グループで 3 つを決める。使える機能、項目ごとの閲覧と編集、対象者の範囲(全員、条件、名前の指定)だ（出典: https://apidocs.hibob.com/docs/api-service-users、見た日 2026-11-11）。
  - 既定では在籍中の社員だけが対象。マイナンバーにあたる番号など機微な項目は、閲覧と編集の両方がないと返らない（出典: https://apidocs.hibob.com/docs/api-service-users、見た日 2026-11-11）。
  - MCP は「Bob でできないことは MCP でもできない」。管理者はツールを止めたり、書き込みの前に確認を求めたりできる（出典: https://www.hibob.com/mcp-beta、見た日 2026-11-11）。
  - API の監査ログは見つからなかった。

## 統合 API

### Merge(HRIS の統合 API、Agent Handler)

- 対象: 開発者向け(多くの人事システムを 1 つの API で読む)。
- AI とエージェントでしていること: Agent Handler は、エージェントと外のシステムの間に入る層だ。190 を超えるコネクタ、利用者ごとの認証、ツール呼び出しを調べる Security Gateway を持つ（出典: https://docs.merge.dev/merge-agent-handler、見た日 2026-11-11）。MCP でつなげる（出典: https://docs.merge.dev/merge-agent-handler、見た日 2026-11-11）。
- 提供の段階: 不明(ページに段階の記載がない)。
- 権限とデータの扱い:
  - HRIS の共通モデル: BankInfo、Benefit、Company、Dependent、Employee、EmployeePayrollRun、Employment、Group、Location、PayGroup、PayrollRun、TimeOff、TimeOffBalance、TimesheetEntry など（出典: https://docs.merge.dev/merge-unified/llms.txt、見た日 2026-11-11）。評価のモデルは一覧になかった。
  - 認証は Bearer の API キーと、連携先ごとの `X-Account-Token` だ（出典: https://docs.merge.dev/merge-unified/hris/overview.md、見た日 2026-11-11）。
  - スコープは共通モデル単位。モデルを止めると、その項目もすべて止まる。既定のスコープと、連携先ごとのスコープがある（出典: https://docs.merge.dev/merge-unified/hris/data-management/scopes.md、見た日 2026-11-11）。
  - Agent Handler は、誰が、どのツールを、どのコネクタに、どの利用者の代わりに呼んだかを監査の記録に残す（出典: https://docs.merge.dev/merge-agent-handler、見た日 2026-11-11）。

### Finch(給与と人事の統合 API)

- 対象: 開発者向け(給与と人事のシステムを 1 つの API で読む)。
- AI とエージェントでしていること: 公式文書では確かめられなかった。
- 提供の段階: MCP は不明。
- 権限とデータの扱い:
  - 連携のときに `products` で求める権限を並べる(company、directory、individual、employment、payment、pay_statement など)。雇用主は画面ですべての要求を見る（出典: https://developer.tryfinch.com/implementation-guide/Connect/Set-Up-Finch-Connect、見た日 2026-11-11）。
  - SSN は別のスコープだ。スコープを足すには、雇用主の再認証が要る（出典: https://developer.tryfinch.com/implementation-guide/Connect/Set-Up-Finch-Connect、見た日 2026-11-11）。
  - 連携できるのは、全社員の名簿と全社の給与を見られる管理者だけだ（出典: https://developer.tryfinch.com/how-finch-works/finch-connect、見た日 2026-11-11）。
  - 監査ログは見つからなかった。

## その他(短く)

- HRBrain: 外部の生成 AI と人材データをつなぐ「Brain MCP」を 2027 年以降に順次提供すると報じられた。生のデータを外に送らず、集計結果だけを返す設計だという（出典: https://voix.jp/?p=146490、見た日 2026-11-11）(報道)。段階は「発表のみ」。
- マネーフォワード クラウド: 2026-03-26 に API と MCP サーバーを出したのは会計と確定申告だけだ（出典: https://biz.moneyforward.com/support/account/news/new-feature/20260326.html、見た日 2026-11-11）。人事管理と勤怠の公開 API は見つからなかった。
- ジョブカン勤怠管理: 他社連携は管理画面の「接続文字列」で行う。給与ソフトへは従業員情報と勤怠データを取り込める（出典: https://biz.moneyforward.com/support/payroll/guide/integrations/in04.html、見た日 2026-11-11）。公開の API 仕様書は見つからなかった。

## このプロダクトへの示唆

前提: bot に「普段は簡単に見られないデータ」を読ませ、採用の管理を代わりにやらせる。

### できること

- 従業員、組織、勤怠は、国内外の主なサービスで API から読める。欠員や残業の偏りから採用の必要を見つける材料はそろう。
- 項目と対象者で絞る仕組みがあるサービスもある。HiBob(項目ごとの閲覧/編集、対象者の条件)、SmartHR(エンドポイントと従業員項目ごとの参照/更新)、Rippling(オブジェクトのスコープ × 作った人の権限)だ。
- MCP が 2026 年に一気に広がった。Workday は一般提供、freee は公開済み、BambooHR と HiBob はベータや段階的な提供だ。bot を作る側が個別の API を包む手間は減る。

### 足りないこと

- 権限の形がずれている。MCP の多くは「サインインした人の権限を引き継ぐ」形だ(BambooHR、HiBob の OAuth 版、Workday、Rippling AI)。これは「普段見られないデータを bot が見る」と逆の向きになる。
- 推測: HiBob がサービス用の利用者での MCP の新規接続を 2026-11-09 に止めたのは、この流れの表れだ。bot 専用の ID に広い権限を渡す形は、ベンダーが避け始めている。
- 推測: そのため bot には、管理者が発行するトークン(サービス用の利用者)を使うことになりやすい。そのトークンは、一人の社員より広い範囲を見る「特権の利用者」になる。
- スコープが粗い。統合 API は Merge が共通モデル単位、Finch が製品単位で、Finch は全社の給与を見られる管理者の許可が要る。部署や目的で絞れない。
- 抜け道がある。SAP SuccessFactors では「OData API (read-only)」の権限が、ロールの権限を飛ばして全データを返す。読み取り専用だから安全、とは言えない。
- 監査ログが弱い。API の操作が残ると公開文書で確かめられたのは SAP SuccessFactors(OData API Audit Log)と Merge Agent Handler だけだった。ほかは見つからなかった。bot は自分で「誰の依頼で、何を、なぜ読んだか」を残す必要がある。
- 書き込みが混ざる。SmartHR の crews、KING OF TIME の従業員の削除、BambooHR の MCP の削除など、書けるものが多い。bot は既定を読み取りにし、書き込みは人の承認を通すべきだ。
- 評価のデータは取りにくい。カオナビは評価の流れ(スマートレビュー)を API で操作できない。HRBrain の構想は集計結果だけを返す。推測: 評価は「個人の値を読む」より「集計を返す」形が業界の落としどころになりそうだ。
- 国内の多くは、トークンの発行がサポート窓口経由(KING OF TIME)や申請制(ジョブカン)だ。セルフサービスで bot をつなぐ体験は作りにくい。

### 設計の方向(推測)

- 推測: bot の権限は「目的ごとの小さな資格」に分けて持つとよい。例は「欠員の検知には部署と人数と勤怠の集計だけ」「面接官の割り当てには氏名と所属と予定だけ」だ。
- 推測: 元のサービスのスコープが粗い分は、hiring-os の側で項目を落とし、集計で返す層を作ると差になる。
- 推測: 監査ログを hiring-os の側で必ず残し、人事の担当者が見返せるようにする。これは元のサービスにない価値になる。

## 見つからなかったこと

- SmartHR、freee人事労務、KING OF TIME、カオナビ、BambooHR、Rippling、HiBob、Finch で、API や MCP の操作が監査ログに残るかの公開文書。
- freee人事労務の OAuth スコープの一覧(アプリの権限画面の中身)。
- カオナビの API キーを、シート、項目、所属で絞れるか。
- Workday の API の認証と統合用の利用者の仕組み(文書はログインが要る)。
- SAP SuccessFactors の公式 MCP サーバーと、Joule の各 Assistant の提供の段階。
- Rippling MCP と Finch MCP の公式な提供の段階。
- マネーフォワード クラウド人事管理と勤怠の公開 API。ジョブカン勤怠管理の公開 API 仕様書。
- Merge や Finch が国内のサービス(SmartHR、freee など)につながるか。今回は確かめていない。
- タレントパレット、Deel、Gusto は今回は調べていない。
- freee のヘルプ(support.freee.co.jp)は 403 で開けなかった。KING OF TIME の管理画面でのトークン発行と IP 制限はそこに書かれているが、読めていない。
