# 企業の側でつなぐ相手と、つなぎ方(2026-11 時点)

hiring-os は企業側のシステム(人事労務、勤怠、給与、評価、ATS、求人媒体など)を作らず、つなぐ相手にする。この文書は、つなぐ相手ごとに、外から何をどう読めるかを調べたものだ。見た日はすべて 2026-11-18。[hr-data.md](hr-data.md) と [ats.md](ats.md) と重なるサービスも、ここで開き直した。件数はこのファイルの中で数える。

出典の種類の書き方:

- 無印: 公式の開発者文書、料金ページ、ヘルプ、製品ページ、規約。
- (会社の発表): そのサービスの会社のプレスリリースやブログ。
- (報道)、(解説): 報道機関や解説の記事。
- (連携先の資料): そのサービスとつなぐ他社が出す公式ヘルプや手順書。
- (抜粋で確認): ページが開けず、検索結果の抜粋でだけ確かめたもの。

## 結論

- 国内の人事労務、勤怠、給与は、統合 API では届かない。Apideck は SmartHR、KING OF TIME、freee人事労務、ジョブカンを「まだ対応していない」と明記していた。Merge、Finch、Kombo、Unified.to の国内の対応は確かめられなかった。国内は自前でつなぐ前提になる(「統合 API の範囲、粗さ、料金の形」)。
- 国内で外部の開発者がすぐ始められるのは、SmartHR、freee人事労務、HERP Hire、カオナビの 4 件だった。KING OF TIME とジョブカンは申請か問い合わせが要る。Airシフトとマネーフォワード クラウド給与は公開 API が見つからなかった。HRMOS採用は 2026-08-31 に API の提供を決めた段階だ。
- 求人媒体は、応募を外に出す API を ATS の提携先にしか開いていない。Indeed は開発者契約と Indeed の裁量、Airワーク は提携 ATS 7 社だった。国内の媒体で企業が使える公開 API は見つからず、確かめられた口は管理画面の CSV の書き出しだけだった。
- 画面を操作する bot は、規約とぶつかる可能性が高い。Indeed の規約は「AI or Agentic AI」を含む自動のアクセスを禁じ、SmartHR の規約はスクレイピングを禁じている。画面の操作は担当者の権限の全体で動き、監査で本人と区別しにくい。
- MCP は「担当者本人のログインと権限」の形にそろってきた。HiBob は 2026-11-09 から、サービス用の利用者での MCP の新しい接続を止めた。ADP も組織全体の権限は「coming soon」だった。推測: 担当者の PC で、その人の権限で読む hiring-os の形は、この流れに合う。
- メール、予定、文書には狭い口がある。予定の空き(Google の freeBusy、Microsoft の getSchedule)、Google Drive の `drive.file`、SharePoint の Selected scope、Exchange の RBAC for Applications だ。逆に Gmail の本文を広く読む scope(`gmail.readonly` など)は restricted で、サーバーに置くなら 12 か月ごとの第三者の評価が要る。Slack は Marketplace 外の商用アプリの履歴の取得を 1 分 1 回に絞り、LLM の学習を禁じた。
- 担当者の PC に bot を入れると、企業の IT の承認が最大 4 段重なる。1〜3 段は製品の仕組みの承認で、端末(Intune の App Control、macOS の MDM)、OAuth アプリの管理者の同意(Microsoft Entra、Google Workspace)、チャットのアプリの承認(Slack)だ。macOS では、画面の収録の許可を MDM で配れず、担当者本人がオンにする。4 段目は事業者の審査だ。国内の大企業では、セキュリティチェックシートへの回答が導入の条件になる例が増えている(報道)。

## 比べる表

1 行 1 サービス。区分の件数: 人事労務 5、勤怠 5、給与 4、評価 4、ATS 5、統合 API 5、求人媒体 4(Indeed は API と CSV の 2 行)、メール 2、予定 2、チャット 4、文書の置き場 4。合わせて 44 行(国内 15、海外 29)。セルは短くまとめた。詳しい中身と、表にない出典は本文にある。

| サービス | 区分 | 国 | API | 読める項目 | 認証 | 絞れる単位 | MCP の段階 | 書き込みの可否 | 外部の開発者の条件 | 出典 | 見た日 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| SmartHR | 人事労務 | 国内 | あり | 従業員(crews)ほか。一覧は API 仕様書 | 管理者が発行するトークン。SmartHR Plus 経由の OAuth もある(連携先の資料) | OAuth はつないだ人の権限グループの範囲。トークンの細かさは今回の公開ページで確かめられず | 公式は見つからなかった | 可(追加、削除のエラー定義あり) | SmartHR の利用者は無料、手続き不要。Sandbox は無料。パートナー審査の文書は見つからなかった | https://developer.smarthr.jp/ | 2026-11-18 |
| freee人事労務 | 人事労務 | 国内 | あり | 従業員(住所、保険、家族、口座、基本給、手当)、所属、役職、勤怠、打刻、申請、年末調整 | OAuth 2.0(本人がログイン) | アプリごとに API 権限を選ぶ。多くは「管理者のみ実行可」 | 不明(freee-mcp を公開中。段階の表記なし) | 可(従業員、勤怠、申請、年末調整など) | 開発者アカウントは無料。使える API は契約プランの機能と同じ | https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json | 2026-11-18 |
| BambooHR | 人事労務 | 海外 | あり | 従業員、休暇、目標、採用、レポート、データセット | 利用者ごとの API キー。パートナーは OAuth | API キーは作った人の権限。OAuth はスコープ | ベータ | 可(MCP で従業員の更新、休暇申請、目標の削除など) | 開発者ポータルは無料。Marketplace チームと調整。プラン条件は見つからなかった | https://documentation.bamboohr.com/docs/mcp-server | 2026-11-18 |
| HiBob | 人事労務 | 海外 | あり | 人事データ、休暇、勤怠、評価、目標、学習、採用、報酬 | API はサービス用の利用者(ID とトークン)。MCP は本人の OAuth | 機能、項目ごとの閲覧/編集、対象者(全員、条件、指名) | 不明(OAuth 版を 2026-06 から段階的に提供) | 可(Bob で許される範囲) | 管理者がサービス用の利用者を作る。パートナー条件は見つからなかった | https://apidocs.hibob.com/docs/api-service-users | 2026-11-18 |
| Rippling | 人事労務 | 海外 | あり | 従業員(workers)、報酬、部署、休暇、勤怠、シフト、候補者、求人など約 150 スコープ | API トークン(Bearer) | オブジェクトごとのスコープ × 作った人の権限 | 不明(製品ページに「Rippling MCP」の札のみ) | 一部可(休暇申請、勤怠、部署など)。workers と報酬は読み取りのみ | トークン作成は専用の権限が要る。App Shop の条件は確かめられなかった | https://developer.rippling.com/documentation/rest-api/essentials/permissions | 2026-11-18 |
| KING OF TIME | 勤怠 | 国内 | あり | 従業員、所属、日別/月別勤怠、打刻、休暇、スケジュール、人件費、申請 | Bearer のアクセストークン | 連携目的とエンドポイントの対応表あり。対象者で絞る記載は見つからなかった | 見つからなかった | 可(従業員の登録/削除、打刻、スケジュール、申請の承認) | トークンはサポートセンターに問い合わせて発行。動作の問い合わせは受けない | https://developer.kingoftime.jp/ | 2026-11-18 |
| ジョブカン勤怠管理 | 勤怠 | 国内 | あり(仕様書は非公開) | 従業員、グループ、管理者、シフト、打刻、集計など(画面の例) | API クライアント(client_credentials) | 資源ごとに create/read/update/delete を選ぶ | 見つからなかった | 可(資源による) | 事前の利用申請が要る(連携先の資料、2023 年作成) | https://help.crowdlog.jp/hc/article_attachments/4982421642782 | 2026-11-18 |
| Airシフト | 勤怠(店舗のシフト) | 国内 | 見つからなかった | 連携は 4 つだけ(シフトボード、freee人事労務、Airワーク 給与支払、Airメイト) | 該当なし | 該当なし | 見つからなかった | 該当なし | 外部の開発者向けの記載は見つからなかった | https://faq.airshift.jp/hc/ja/articles/360003861632 | 2026-11-18 |
| Deputy | 勤怠(シフト) | 海外 | あり | 従業員、勤務表(timesheet)、シフト(roster)、休暇 | OAuth 2.0(利用者が承認)、永続トークン | 見つからなかった | 公式は見つからなかった | 可(従業員の追加、休暇の追加など) | 7 日の試用アカウントで開発。審査の記載は見つからなかった | https://developer.deputy.com/docs/using-oauth-20.md | 2026-11-18 |
| 7shifts | 勤怠(飲食店のシフト) | 海外 | あり | 利用者、シフト、打刻、時給、店舗、部門、休暇 | 自社用はアクセストークン(管理者レベル)。他社製品は OAuth | OAuth はプランでエンドポイントが変わる | 不明(公式 MCP あり。「新しい」とだけ記載。読み取りのみ) | 可(API)。MCP は GET のみ | OAuth は審査済みのパートナーだけ。提携の審査と技術の認定が要る | https://developers.7shifts.com/docs/authentication.md | 2026-11-18 |
| freee人事労務(給与) | 給与 | 国内 | あり | 給与明細、賞与明細、基本給、手当、控除 | OAuth 2.0 | 給与明細は「管理者権限を持ったユーザーのみ」 | 不明(freee-mcp に給与明細の手順あり) | 一部可(明細の備考、手当、控除の更新) | 人事労務と同じ | https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json | 2026-11-18 |
| マネーフォワード クラウド給与 | 給与 | 国内 | 見つからなかった | 公開 API の一覧に給与はない | 該当なし | 該当なし | 見つからなかった(MCP は会計だけ) | 該当なし | API/MCP の技術支援は有償の公認メンバーの士業事務所に限る(会計の告知) | https://developers.biz.moneyforward.com/ | 2026-11-18 |
| ADP | 給与 | 海外 | あり | 従業員、勤怠、休暇、給与の入力、入社、採用(API Central の用途) | OAuth 2.0 + 相互 TLS の証明書 | MCP は管理者がデータとできる操作を決める(会社の発表) | 一般提供(会社の発表で「Available Today」。Enterprise HR と Vantage HCM のみ) | 可(給与の入力など) | パートナーは参加契約(DPA)、Marketplace への 2 つの掲載、SSO、セキュリティ審査が要る | https://marketplace-cdn.adp.com/dev-portal/pdf/ADP_Marketplace_Partner_Development_Learning_Guide | 2026-11-18 |
| Gusto | 給与 | 海外 | あり(パートナー限定) | 会社、従業員、給与、勤怠、報酬(MCP のツール) | OAuth 2.0 | パートナーは審査でスコープを割り当て | 不明(MCP は v0.1.0。2025-08 から提供) | 可(MCP で給与の実行も可) | パートナーは事前承認とセキュリティ審査。実績の少ない新しい製品は対象外 | https://docs.gusto.com/app-integrations/docs/introduction | 2026-11-18 |
| カオナビ | 評価 | 国内 | あり | メンバー基本情報、シート(評価履歴、異動履歴など)、所属ツリー、ユーザー、ロール | Consumer Key/Secret からアクセストークン | 見つからなかった | 公式は見つからなかった | 可(メンバー、シート、所属など) | 公開 API v2 は無償(2025-04 時点) | https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933 | 2026-11-18 |
| HRBrain | 評価 | 国内 | 公式の仕様書は見つからなかった | メンバー情報(連携先の資料) | 見つからなかった | 見つからなかった | 発表のみ(Brain MCP は 2027 年以降、報道) | メンバーの登録、更新(連携先の資料) | 見つからなかった | https://voix.jp/?p=146490 | 2026-11-18 |
| Lattice | 評価 | 海外 | あり | 利用者、部署、評価サイクル、評価、フィードバック、目標、近況の更新(updates) | API キー(作った人の権限を引き継ぐ) | スコープなし。作った人の見える範囲 | 不明(2026-07-07 に「available now」。ベータの表記なし) | API は目標だけ。MCP は評価の提出、フィードバックも可 | プラン条件は見つからなかった | https://developers.lattice.com/docs/authentication-1.md | 2026-11-18 |
| Culture Amp | 評価 | 海外 | あり | 従業員(今の状態のみ)、評価サイクル、上司の評価、サーベイ | OAuth 2.0 client credentials(Account Owner が作る) | 「対象:ID:権限」の形のスコープ(例に `performance-evaluations-read`) | 見つからなかった | 不可(読み出しのみ) | 全プランで追加料金なし | https://support.cultureamp.com/en/articles/8675294-faqs-culture-amp-api | 2026-11-18 |
| HERP Hire | ATS | 国内 | あり | 応募、応募ファイル、評価、担当、職種、ユーザー、エージェント | Bearer の API キー(管理者のみ発行) | `candidacy:read` など資源 × 読み書き | ATS は見つからなかった | 可(応募の追加、選考ステップ、評価の記入など) | 有料プランの契約者だけ | https://public-api.herp.cloud/hire/public/doc | 2026-11-18 |
| HRMOS採用 | ATS | 国内 | 発表のみ(2026-08-31 に提供を決定。時期未定) | 選考情報、応募者情報(予定) | 未発表 | 「選考フロー管理機能」の適用環境だけ | 見つからなかった | 選考評価の登録(予定) | 未発表 | https://hrmos.co/info/news/20260831-2/ | 2026-11-18 |
| Greenhouse | ATS | 海外 | あり | 候補者、応募、求人、面接、評価表、オファーなど | Harvest v3 は OAuth 2.0。自社は client credentials、パートナーは authorization code | v3 は利用者(sub)の権限。一覧は Site Admin の認可 | ベータ(Open Beta) | 可 | パートナーは共通の顧客 1 社以上、契約の署名が要る | https://harvestdocs.greenhouse.io/docs/authentication | 2026-11-18 |
| Ashby | ATS | 海外 | あり | 求人、候補者、面接、オファー、レポート、監査ログなど 13 モジュール | API キー(Basic)。MCP は本人の OAuth | モジュールごとの読み書き。機密の求人と非公開項目は既定で見えない | ベータ | 可 | パートナーは紹介の面談、法務の確認、デモの承認 | https://developers.ashbyhq.com/docs/authentication | 2026-11-18 |
| Workable | ATS(人事も一部) | 海外 | あり | 求人、候補者、オファー、従業員、休暇、勤怠、評価 | API トークン。MCP は OAuth 2.0 | トークンはスコープを選ぶ。MCP は本人の権限 | 不明(提供中。段階の表記なし) | 可(MCP で約 39 の書き込みツール) | プランとパートナーの条件は見つからなかった | https://workable.readme.io/reference/workable-mcp-server | 2026-11-18 |
| Merge | 統合 API | 海外 | あり | HRIS 15 モデル、ATS 17 モデル。評価のモデルなし | API キー + 連携先ごとのトークン | 共通モデル単位。連携先ごとのスコープ | 不明(Agent Handler の段階の記載なし) | 一部 | 3 接続まで無料。月 650 ドルで 10 接続まで | https://www.merge.dev/pricing | 2026-11-18 |
| Finch | 統合 API | 海外 | あり | 会社、名簿、個人、雇用、支払い、給与明細、控除、福利厚生 | 雇用主の管理者が Finch Connect で許可 | 製品(データの種類)単位。SSN は別 | ベータ | 一部(控除など) | Starter は 1 接続月 65 ドル、15 接続まで | https://www.tryfinch.com/pricing | 2026-11-18 |
| Kombo | 統合 API | 海外 | あり | 従業員、雇用、グループ、休暇、勤務表、評価、給与明細、ATS | 見つからなかった | スコープあり(詳細は未確認) | 見つからなかった | 一部(Scale 以上) | 料金は非公開(年額の基本料 + 接続ごと) | https://www.kombo.dev/pricing | 2026-11-18 |
| Apideck | 統合 API | 海外 | あり | 従業員、会社、部署、休暇申請、給与、勤務予定 | Vault で認証を預かる | Data Scopes は Scale 以上 | 不明(MCP サーバーを全プランに含む) | 一部(従業員、部署、休暇) | Launch は月 599 ドルで 25 社、1 区分 | https://www.apideck.com/pricing | 2026-11-18 |
| Unified.to | 統合 API | 海外 | あり | 従業員、グループ、会社、拠点、給与明細、休暇、勤務など | 接続ごとの資格情報 | MCP のツールを権限やツール名で絞れる | 不明(「launched」とだけ記載) | 一部 | 試用は無料(月 1 万回)。Grow は月 750 ドルから | https://unified.to/pricing | 2026-11-18 |
| Indeed(Indeed Apply、Disposition Sync、Retrieve Candidates) | 求人媒体 | 海外(日本も対象) | あり(ATS 提携先だけ) | 応募の JSON と履歴書。Smart Sourcing の候補者、Smart Screening の点 | 提携先のアプリの OAuth。企業の登録は Indeed の管理者か所有者の 3-legged トークン | 企業ごと(登録した企業) | 求職者向けのみベータ(Claude 限定)。企業向けは見つからなかった | 採否の状態を返せる(Disposition Sync) | 開発者契約。Indeed の裁量で許可。統合は約 6 週間 | https://docs.indeed.com/indeed-apply/ats | 2026-11-18 |
| Indeed 管理画面の CSV | 求人媒体 | 海外(日本語ヘルプ) | なし(画面の書き出し) | 応募者の一覧(項目の記載なし) | 担当者のログイン(2 段階認証が必須) | 求人と応募者の選択 | なし | なし | 認証済みか「スポンサー求人のみ」の企業。1 回 1,000 件、1 日 1 万件、3 か月以内 | https://jp.indeed.com/help/employers/articles/how-to-export-candidates | 2026-11-18 |
| Airワーク 採用管理 | 求人媒体 | 国内 | 公開 API は見つからなかった。提携 ATS への連携あり | 応募者の一覧(CSV) | 企業が「外部連携認証キー」を発行(抜粋で確認) | 不明 | 見つからなかった | 不明 | 連携先は 7 社の ATS に限る(2026-07-27 時点、抜粋で確認) | https://airregi.jp/work/recruitment/function | 2026-11-18 |
| engage | 求人媒体 | 国内 | 公開 API は見つからなかった | 応募者の情報(Excel か CSV) | 担当者のログイン | 応募から 1 年以内(抜粋で確認) | 見つからなかった | 不明 | 見つからなかった | https://en-gage.net/function/ | 2026-11-18 |
| Gmail(Google Workspace) | メール | 海外 | あり | メール本文、ヘッダー、ラベル | 本人の OAuth か、ドメイン全体の委任(管理者) | scope(種類と読み書き)。送信元では絞れない | 公式あり。Developer Preview | 下書き、送信、ラベル | restricted scope の審査と 12 か月ごとのセキュリティ評価(CASA) | https://developers.google.com/workspace/gmail/api/auth/scopes | 2026-11-18 |
| Exchange Online(Microsoft Graph のメール) | メール | 海外 | あり | メール本文、ヘッダー、フォルダー | 本人の OAuth(delegated)か、アプリの権限(管理者の同意) | アプリの権限は RBAC for Applications でメールボックスの集まりに絞れる | Work IQ MCP は一般提供(delegated のみ)。旧 Mail MCP はプレビュー | 送信、移動、削除 | アプリの権限は Global Administrator の同意。Work IQ は Copilot Credits の従量課金 | https://learn.microsoft.com/en-us/exchange/permissions-exo/application-rbac | 2026-11-18 |
| Google Calendar | 予定 | 海外 | あり | 空き(busy の時間帯)、予定の詳細 | 本人の OAuth か、ドメイン全体の委任 | scope(`calendar.freebusy` など) | 公式あり。Developer Preview | 予定の作成と変更 | 公開アプリは審査(分類はページに記載なし) | https://developers.google.com/workspace/calendar/api/v3/reference/freebusy/query | 2026-11-18 |
| Microsoft Graph の予定(getSchedule、findMeetingTimes) | 予定 | 海外 | あり | 空き、件名と場所(相手の共有の設定による) | getSchedule は delegated とアプリの両方。findMeetingTimes は delegated のみ | RBAC for Applications で予定を読むメールボックスを絞れる | Work IQ MCP は一般提供。旧 Calendar MCP はプレビュー | 予定の作成と変更 | アプリの権限は管理者の同意 | https://learn.microsoft.com/en-us/graph/api/calendar-getschedule | 2026-11-18 |
| Slack | チャット | 海外 | あり | メッセージ、スレッド、ファイル、検索 | 本人のトークン(user token)と bot のトークン | チャンネル(bot を招いた所)、scope | 公式あり。一般提供(2026-02-17、会社の発表) | 投稿、予約投稿、canvas | Marketplace 外の商用アプリは履歴の取得が 1 分 1 回。MCP は Marketplace か社内アプリだけ。LLM の学習と一括の書き出しは禁止 | https://slack.com/terms-of-service/api | 2026-11-18 |
| Microsoft Teams | チャット | 海外 | あり(Graph) | チャットとチャンネルのメッセージ、会議の記録 | delegated、アプリの権限、RSC(入れたチームやチャットだけ) | チーム、チャット、会議ごと(RSC) | Work IQ MCP は一般提供。旧 Teams MCP はプレビュー | 投稿 | テナント全体のメッセージをアプリの権限で読むには申請(protected API) | https://learn.microsoft.com/en-us/microsoftteams/platform/graph-api/rsc/resource-specific-consent | 2026-11-18 |
| LINE WORKS | チャット | 国内 | あり(API 2.0) | メッセージ(bot)、予定、メール、ファイルなど | 本人の OAuth か、Service Account(JWT、アプリ専用の仮想の管理者) | scope(`mail.read`、`calendar.read` など) | 公式は見つからなかった(非公式のみ) | bot の投稿など | 使える scope はプランで変わる | https://developers.worksmobile.com/jp/docs/auth | 2026-11-18 |
| Chatwork | チャット | 国内 | あり(API v2) | ルームのメッセージ、タスク、ファイル | 本人の OAuth 2.0 か API トークン | scope(`rooms.messages:read` など) | Chatwork の GitHub に MCP サーバーあり。段階の表示なし | 投稿、タスク | 管理者の承認の要否は不明(ヘルプは 403) | https://developer.chatwork.com/docs/oauth | 2026-11-18 |
| Google Drive | 文書 | 海外 | あり | ファイルの中身とメタデータ | 本人の OAuth か、ドメイン全体の委任 | `drive.file` なら本人が選んだファイルだけ | 公式あり。Developer Preview | 作成、更新 | `drive.file` は non-sensitive。`drive.readonly` は restricted で審査 | https://developers.google.com/workspace/drive/api/guides/api-specific-auth | 2026-11-18 |
| SharePoint と OneDrive | 文書 | 海外 | あり(Graph) | ファイル、リスト、項目 | delegated かアプリの権限 | サイト、リスト、項目、ファイル(Selected scope) | Work IQ MCP は一般提供。旧 SharePoint、OneDrive MCP はプレビュー | read、write、owner、fullcontrol を選んで与える | Entra での同意と、資源ごとの付与の両方が要る | https://learn.microsoft.com/en-us/graph/permissions-selected-overview | 2026-11-18 |
| Box | 文書 | 海外 | あり | ファイル、フォルダー、Box AI | 本人の OAuth 2.0。JWT と CCG は管理者の承認 | サービスアカウントは招かれたフォルダーだけ | 公式のリモート MCP あり。段階の表示なし | 作成、更新 | サーバーのアプリは管理者の承認。MCP は管理者が管理画面で有効にする | https://developer.box.com/guides/authentication/ | 2026-11-18 |
| Dropbox | 文書 | 海外 | あり | ファイル、共有リンク、検索 | 本人の OAuth。チームの scope は管理者 | App Folder か Full Dropbox | 公式のリモート MCP あり。オープンベータ | 作成、移動、削除 | 管理者がアプリの作成を止められる | https://help.dropbox.com/integrations/connect-dropbox-mcp-server | 2026-11-18 |

## 人事労務

### SmartHR

- 公開 API がある。SmartHR を使っていれば無料で、管理画面の設定だけで使える(出典: https://developer.smarthr.jp/、見た日 2026-11-18)。
- SmartHR を使っていない人も、開発者向けの Sandbox で無料で試せる(出典: https://developer.smarthr.jp/、見た日 2026-11-18)。
- 認証はアクセストークン。発行は「管理者のみ可能」だ(出典: https://developer.smarthr.jp/api/about_api、見た日 2026-11-18)。
- 上限はトークンごとに 1 時間 5,000 回、毎秒 10 回。サブドメインごとに 1 分 50,000 回(出典: https://developer.smarthr.jp/api/about_api、見た日 2026-11-18)。
- 例に出る資源は従業員(`/api/v1/crews`)。エラー表に従業員の追加の上限と「削除できない資源」があり、書き込みもできると読める(出典: https://developer.smarthr.jp/api/about_api、見た日 2026-11-18)。
- OAuth の連携もある。マネーフォワード Admina は SmartHR Plus 経由の OAuth を勧めている。管理者のアカウントでログインして承認する(出典: https://support.i.moneyforward.com/en/integrations/zyl6g8sbgx-smart-hr.md、見た日 2026-11-18)(連携先の資料)。
- OAuth で同期されるのは、つないだアカウントの権限グループが見られる項目だけ。見えない項目はエラーを出さずに抜ける(出典: https://support.i.moneyforward.com/en/integrations/zyl6g8sbgx-smart-hr.md、見た日 2026-11-18)(連携先の資料)。
- 権限は「本人」と「他人」で分けて管理する。両方で閲覧か編集が要る(出典: https://support.i.moneyforward.com/en/integrations/zyl6g8sbgx-smart-hr.md、見た日 2026-11-18)(連携先の資料)。
- トークンをエンドポイントや項目で絞る仕組みは、今回開いた公開ページでは確かめられなかった。説明のヘルプ(support.smarthr.jp)は今回開いていない。
- 公式の MCP は見つからなかった。検索で出たのは個人の OSS と他社のホスト版だけだった。
- 他社の製品として SmartHR Plus に載せる条件(審査、費用)は見つからなかった。

### freee人事労務

- 公開 API がある。認証は OAuth 2.0(出典: https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json、見た日 2026-11-18)。
- 読めるもの: 従業員(住所、健康保険、厚生年金、家族、銀行口座、基本給、手当、控除)、所属、部門、役職、勤怠、打刻、勤怠の集計、各種の申請、承認経路、年末調整(出典: https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json、見た日 2026-11-18)。
- 書けるもの: 従業員の作成、更新、削除。勤怠の更新と削除。打刻の登録。申請の作成と承認の操作。年末調整の更新(出典: https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json、見た日 2026-11-18)。
- 従業員の作成、更新、削除や、基本給、手当、控除の操作は「管理者権限を持ったユーザーのみ実行可能」(出典: https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json、見た日 2026-11-18)。
- 使える API は契約プランの機能と同じ。例は「スタンダードプランなら打刻 API も使える」(出典: https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json、見た日 2026-11-18)。
- 上限は 1 時間 10,000 回(出典: https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json、見た日 2026-11-18)。
- 開発者アカウントは無料で作れる。アプリの詳細画面で API の権限を選ぶ。権限を変えたらトークンを出し直す(出典: https://developer.freee.co.jp/getting-started、見た日 2026-11-18)。
- 公式の MCP「freee-mcp」がある。リモート版は `https://mcp.freee.co.jp/mcp`。認証は OAuth 2.0(PKCE)(出典: https://github.com/freee/freee-mcp、見た日 2026-11-18)。
- freee-mcp の道具は汎用の GET、POST、PUT、PATCH、DELETE。人事労務の手順書は 11 本(出典: https://github.com/freee/freee-mcp、見た日 2026-11-18)。
- MCP の段階: ページにベータや一般提供の表記はない。段階は不明。
- 公開アプリの審査やアプリストア掲載の条件は、今回のページでは見つからなかった。

### BambooHR

- API キーは利用者ごとに発行する。操作はそのキーの利用者と同じ権限になる(出典: https://documentation.bamboohr.com/docs/getting-started、見た日 2026-11-18)。
- 他社のアプリは OAuth を使う。開発者ポータルは無料。トークンは 3600 秒で切れる(出典: https://documentation.bamboohr.com/docs/getting-started、見た日 2026-11-18)。
- Marketplace に載せる条件は書かれていない。「Marketplace チームと一緒に進められる」とだけある(出典: https://documentation.bamboohr.com/docs/getting-started、見た日 2026-11-18)。
- MCP はベータ。最終更新は 2026-09-18(出典: https://documentation.bamboohr.com/docs/mcp-server、見た日 2026-11-18)。
- MCP は OAuth 2.0。管理者が「AI Connectors」アプリを有効にし、対象の権限レベルを選ぶ(出典: https://documentation.bamboohr.com/docs/mcp-server、見た日 2026-11-18)。
- MCP の道具は 56。読み取り 41、書き込み 12、削除 2(出典: https://documentation.bamboohr.com/docs/mcp-server、見た日 2026-11-18)。
- 書き込みの例: 従業員の更新、休暇の申請と承認、目標の作成と削除、応募へのコメント(出典: https://documentation.bamboohr.com/docs/mcp-server、見た日 2026-11-18)。
- 権限は利用者の権限レベルに従う。休暇の残りには休暇の閲覧権限、採用には ATS の設定権限が要る(出典: https://documentation.bamboohr.com/docs/mcp-server、見た日 2026-11-18)。
- プラン条件は書かれていない。

### HiBob

- API はサービス用の利用者(ID とトークン)で使う。作れるのは Bob の管理者など(出典: https://apidocs.hibob.com/docs/api-service-users、見た日 2026-11-18)。
- サービス用の利用者は最初は何も見えない。権限グループで機能、項目ごとの閲覧と編集、対象者を決める(出典: https://apidocs.hibob.com/docs/api-service-users、見た日 2026-11-18)。
- 対象者は「全員」「条件に合う人」「名前を指定」から選ぶ。既定は在籍中の社員だけ(出典: https://apidocs.hibob.com/docs/api-service-users、見た日 2026-11-18)。
- SSN や生年月日など機微な項目は、閲覧と編集の両方がないと返らない(出典: https://apidocs.hibob.com/docs/api-service-users、見た日 2026-11-18)。
- MCP: 2026-04-28 にサービス用の利用者で使うホスト版を出した。2026-06 に OAuth 版の段階的な提供を始めた(出典: https://apidocs.hibob.com/docs/hibob-mcp-server、見た日 2026-11-18)。
- 2026-11-09 から、サービス用の利用者での MCP の新しい接続を止めた。今の接続も今後止まりうる(出典: https://apidocs.hibob.com/docs/hibob-mcp-server、見た日 2026-11-18)。
- MCP は本人がログインし、本人の権限を毎回あてる。対象は人事データ、休暇、勤怠、評価、目標、学習、採用、報酬(出典: https://www.hibob.com/mcp-beta、見た日 2026-11-18)。
- 管理者が Bob で MCP を有効にする。読み書きは Bob で許される範囲(出典: https://www.hibob.com/mcp-beta、見た日 2026-11-18)。
- MCP の段階: 一般提供の表記は見つからなかった。推測: ページの URL が `mcp-beta` で、段階的な提供の途中。
- パートナーの条件とプラン条件は見つからなかった。

### Rippling

- API トークンを作れるのは、トークン用の権限を持つ人。管理者は会社の全トークンを見て止められる(出典: https://developer.rippling.com/documentation/rest-api/essentials/api-tokens、見た日 2026-11-18)。
- トークンが読めるのは「作った人の権限」と「トークンのスコープ」の両方で許される範囲だけ(出典: https://developer.rippling.com/documentation/rest-api/essentials/api-tokens、見た日 2026-11-18)。
- 見えない値は null で返る(出典: https://developer.rippling.com/documentation/rest-api/essentials/api-tokens、見た日 2026-11-18)。
- 持ち主が退職するか、30 日使われないとトークンは自動で止まる(出典: https://developer.rippling.com/documentation/rest-api/essentials/api-tokens、見た日 2026-11-18)。
- スコープは約 150。workers、compensations、candidates、job-requisitions、leave-requests、time-entries、departments など(出典: https://developer.rippling.com/documentation/rest-api/essentials/permissions、見た日 2026-11-18)。
- workers と compensations には読み取りのスコープしかない。給与(payroll)の名のスコープはない(出典: https://developer.rippling.com/documentation/rest-api/essentials/permissions、見た日 2026-11-18)。
- 書き込みのスコープがあるのは、休暇申請、勤怠、シフト、部署、採用の下書きなど(出典: https://developer.rippling.com/documentation/rest-api/essentials/permissions、見た日 2026-11-18)。
- MCP: 製品ページに「Rippling MCP」の札がある。段階、認証は書かれていない(出典: https://www.rippling.com/ai、見た日 2026-11-18)。段階は不明。
- App Shop に載せる条件は、開発者サイトの入口がログインを求めたため確かめられなかった(出典: https://developer.rippling.com/documentation、見た日 2026-11-18)。

## 勤怠

### KING OF TIME

- 認証は Bearer のアクセストークン。発行は「各サポートセンターへお問い合わせください」(出典: https://developer.kingoftime.jp/、見た日 2026-11-18)。
- 読めるもの: 企業、管理者、従業員、所属、雇用区分、日別勤怠、打刻、日別/月別の費用、月別勤怠、休暇の残り、スケジュール、申請(出典: https://developer.kingoftime.jp/、見た日 2026-11-18)。
- 書けるもの: 従業員の登録、更新、削除。打刻の登録。スケジュールの登録と削除。申請の承認と棄却(出典: https://developer.kingoftime.jp/、見た日 2026-11-18)。
- 月別勤怠と月別スケジュールは書けない(出典: https://developer.kingoftime.jp/、見た日 2026-11-18)。
- 「連携希望項目」とエンドポイントの対応表がある。目的ごとに使うエンドポイントを確かめる表だ(出典: https://developer.kingoftime.jp/、見た日 2026-11-18)。
- 8:30〜10:00 と 17:30〜18:30 は、トークンと打刻以外の API が使えない(出典: https://developer.kingoftime.jp/、見た日 2026-11-18)。
- 上限は企業ごとに直近 5 分で 500 回。連携サービスごとに 1500 回(出典: https://developer.kingoftime.jp/、見た日 2026-11-18)。
- API の動作の問い合わせは受け付けない(出典: https://developer.kingoftime.jp/、見た日 2026-11-18)。
- マネーフォワード クラウド給与との連携は 2026-01-27 に OAuth 方式に対応した。接続文字列の方式は今後なくなる(出典: https://biz.moneyforward.com/support/payroll/news/new-feature/20260127.html、見た日 2026-11-18)(連携先の資料)。
- MCP、プラン条件、費用は見つからなかった。

### ジョブカン勤怠管理

- API を使うには、ジョブカンへの利用申請が要る。窓口は「Jobcan CX・API連携事務局」(出典: https://help.crowdlog.jp/hc/article_attachments/4982421642782、見た日 2026-11-18)(連携先の資料、2023 年 10 月作成)。
- 申請の後、管理者ページの「基本情報設定」から「他社システム連携」で API クライアントを発行する(出典: https://help.crowdlog.jp/hc/article_attachments/4982421642782、見た日 2026-11-18)(連携先の資料)。
- 画面では、資源ごとに create/read/update/delete を選ぶ。資源は employees、groups、managers、shifts、shiftRequests、adits(打刻)、summaries など(出典: https://help.crowdlog.jp/hc/article_attachments/4982421642782、見た日 2026-11-18)(連携先の資料)。
- 付与の方式は client_credentials と refresh_token から選ぶ(出典: https://help.crowdlog.jp/hc/article_attachments/4982421642782、見た日 2026-11-18)(連携先の資料)。
- 公式の API 仕様書は公開の場所で見つからなかった。api.jobcan.ne.jp のトップは 404 だった。
- 資料が 2023 年のもので、今の画面と違う可能性がある。MCP は見つからなかった。

### Airシフト(店舗のアルバイト向け)

- 連携しているのは、シフトボード、freee人事労務、Airワーク 給与支払、Airメイトの 4 つ。「上記以外のサービスとは現時点で連携していない」(出典: https://faq.airshift.jp/hc/ja/articles/360003861632、見た日 2026-11-18)。
- freee人事労務へは概算人件費のデータを送れる。freee のアカウントが要る(出典: https://airregi.jp/shift/function/integration/、見た日 2026-11-18)。
- Airメイトへは、シフト、勤怠、概算人件費のデータを送れる(出典: https://airregi.jp/shift/function/integration/、見た日 2026-11-18)。
- 外部の開発者向けの公開 API、MCP は見つからなかった。
- 推測: Airシフトの勤怠を取るには、CSV(画面の書き出し)の道しかない。画面を bot が読む道は、D15 で使わない。freee人事労務に送られるのは概算人件費で、勤怠は送られない(勤怠の送り先は Airメイト)。

### Deputy

- API の資源に、従業員、勤務表(timesheet)、シフト(roster)、休暇がある。追加、更新、削除の API も多い(出典: https://developer.deputy.com/、見た日 2026-11-18)。
- 認証は「永続トークン」か OAuth 2.0(出典: https://developer.deputy.com/docs/getting-started-with-the-deputy-api.md、見た日 2026-11-18)。
- OAuth は利用者が自分のインストールに対して承認する。スコープは `longlife_refresh_token` だけが書かれている。アクセストークンは 24 時間(出典: https://developer.deputy.com/docs/using-oauth-20.md、見た日 2026-11-18)。
- トークンが承認した人の権限に絞られるかは書かれていない(出典: https://developer.deputy.com/docs/using-oauth-20.md、見た日 2026-11-18)。
- 開発は 7 日の試用アカウントで行う。延長は API サポートに頼む。パートナーの審査の記載はない(出典: https://developer.deputy.com/docs/using-oauth-20.md、見た日 2026-11-18)。
- Embedded Partner には実装の手厚い支援がある(出典: https://developer.deputy.com/docs/getting-started-with-the-deputy-api.md、見た日 2026-11-18)。
- 公式の MCP は見つからなかった。検索で出たのは他社のホスト版だけだった。

### 7shifts(飲食店のシフト)

- 自社用の連携はアクセストークン。管理画面の「Developer Tools」で作る。1 社分の全 API を使える(出典: https://developers.7shifts.com/docs/authentication.md、見た日 2026-11-18)。
- 他社の製品として多くの顧客につなぐには OAuth。審査済みのパートナーだけが使える。提携の審査と技術の認定がある(出典: https://developers.7shifts.com/docs/authentication.md、見た日 2026-11-18)。
- OAuth はプランで使える資源が変わる。利用者、時給、打刻は Entrée 以上。シフト、休暇、勤務時間と賃金は The Works 以上(出典: https://developers.7shifts.com/docs/plan-requirements、見た日 2026-11-18)。
- プランが足りないと 403 が返る(出典: https://developers.7shifts.com/docs/plan-requirements、見た日 2026-11-18)。
- 公式の MCP がある。文書と仕様の検索は認証なしで使える。自社データを読むにはアクセストークンを渡す(出典: https://developers.7shifts.com/docs/mcp-server.md、見た日 2026-11-18)。
- MCP の実行は GET だけ。書き込みはできない(出典: https://developers.7shifts.com/docs/mcp-server.md、見た日 2026-11-18)。
- MCP の段階: 「MCP support here is new」とだけある。段階は不明。

## 給与

### freee人事労務(給与)

- 給与明細と賞与明細の一覧、個人ごとの明細を読める(出典: https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json、見た日 2026-11-18)。
- 給与明細の API は「管理者権限を持ったユーザーのみ実行可能」。給与計算中は値が null になる(出典: https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json、見た日 2026-11-18)。
- 書けるのは明細の備考、基本給、手当、控除の設定など。給与計算の確定は API の一覧に見当たらなかった(出典: https://raw.githubusercontent.com/freee/freee-api-schema/master/hr/open-api-3/api-schema.json、見た日 2026-11-18)。
- freee-mcp の手順書に給与明細が入っている(出典: https://github.com/freee/freee-mcp、見た日 2026-11-18)。

### マネーフォワード クラウド給与

- 開発者サイトに載る公開 API は、会計、経費、請求書、債務支払、連結会計だけ。給与、人事管理、勤怠はない(出典: https://developers.biz.moneyforward.com/、見た日 2026-11-18)。
- MCP サーバーの記載も会計だけ(出典: https://developers.biz.moneyforward.com/、見た日 2026-11-18)。
- 会計の API と MCP は 2026-09-24 に API キーの認証に対応した。技術の問い合わせ窓口は原則ない。支援は有償の公認メンバーの士業事務所に限る(出典: https://biz.moneyforward.com/support/account/news/new-feature/202609242.html、見た日 2026-11-18)。
- MCP の利用規約(特約)は 2026-07-23 制定。対象の製品は個別に書かれていない(出典: https://biz.moneyforward.com/agreement/mcp、見た日 2026-11-18)。
- 給与への取り込みは、勤怠側(KING OF TIME など)から OAuth で引く形がある(出典: https://biz.moneyforward.com/support/payroll/news/new-feature/20260127.html、見た日 2026-11-18)。外から給与のデータを読む公開 API は見つからなかった。

### ADP

- 他社がつなぐ道(Marketplace): まず 30 日のサンドボックス期間。連携の仕様、価格、日程を 30 日以内に出す(出典: https://marketplace-cdn.adp.com/dev-portal/pdf/ADP_Marketplace_Partner_Development_Learning_Guide、見た日 2026-11-18)。
- その後、開発者参加契約(DPA)を結ぶ。契約なしでは連携を完成できない(出典: https://marketplace-cdn.adp.com/dev-portal/pdf/ADP_Marketplace_Partner_Development_Learning_Guide、見た日 2026-11-18)。
- 必須は 3 つ。API の開発、Marketplace の 2 つの掲載(新規顧客向けと既存顧客向け)、SSO(出典: https://marketplace-cdn.adp.com/dev-portal/pdf/ADP_Marketplace_Partner_Development_Learning_Guide、見た日 2026-11-18)。
- すべての API 呼び出しに相互 TLS の証明書が要る(出典: https://marketplace-cdn.adp.com/dev-portal/pdf/ADP_Marketplace_Partner_Development_Learning_Guide、見た日 2026-11-18)。
- ADP のセキュリティ組織(GSO)がアプリを審査する(出典: https://marketplace-cdn.adp.com/dev-portal/pdf/ADP_Marketplace_Partner_Development_Learning_Guide、見た日 2026-11-18)。
- 顧客が自分で使う道(API Central): 顧客が契約する。用途は従業員の同期、勤怠、休暇、給与の入力、入社、採用(出典: https://apps.adp.com/en-US/apps/419897/adp-api-central/features、見た日 2026-11-18)。
- API Central の MCP は、今は ADP Enterprise HR と Vantage HCM だけ。本人がログインし、本人が見られる範囲だけ。組織全体の権限での接続は「coming soon」(出典: https://apps.adp.com/en-US/apps/419897/adp-api-central/features、見た日 2026-11-18)。
- 2026-10-22 の発表は、MCP サーバーへの接続を「Available Today」とした。管理者がエージェントの見られるデータと操作を決める(出典: https://mediacenter.adp.com/adp-launches-new-ai-powered-tools-to-accelerate-intelligent-workforce-automation、見た日 2026-11-18)(会社の発表)。
- API Central は使った量に応じた課金と報じられた(出典: https://nationalcioreview.com/?p=81497、見た日 2026-11-18)(報道)。

### Gusto

- 他社向けの API(App Integrations)はパートナーに限る(出典: https://docs.gusto.com/app-integrations/docs/introduction、見た日 2026-11-18)。
- 本番には事前承認とセキュリティ審査が要る。承認は保証されない。先に申し込むよう勧めている(出典: https://docs.gusto.com/app-integrations/docs/introduction、見た日 2026-11-18)。
- 「小さな会社に使われた実績のない初期の製品」は今は対象外(出典: https://docs.gusto.com/app-integrations/docs/introduction、見た日 2026-11-18)。
- スコープは審査で用途に合わせて割り当てる。外の呼び出しは拒否される(出典: https://docs.gusto.com/app-integrations/docs/introduction、見た日 2026-11-18)。
- 顧客が自分の Gusto につなぐ道として、MCP サーバーと CLI がある。これはパートナー API とは別だ(出典: https://docs.gusto.com/app-integrations/docs/introduction、見た日 2026-11-18)。
- MCP は OAuth 2.0(PKCE)。使えるのは全体管理者か完全な管理者。つなぐときにデータの種類を選ぶ(出典: https://docs.gusto.com/app-integrations/docs/mcp、見た日 2026-11-18)。
- 道具は 72。`run_payroll` で給与の計算と送信までできる。文書はすべての呼び出しで人の確認を勧める(出典: https://docs.gusto.com/app-integrations/docs/mcp、見た日 2026-11-18)。
- MCP の版は 0.1.0。2025-08 に出て、2026-09 まで更新がある。ベータか一般提供かは書かれていない(出典: https://docs.gusto.com/app-integrations/docs/mcp、見た日 2026-11-18)。
- 製品ページ(gusto.com/product/agents)は 403 で開けなかった。

## 評価

### カオナビ

- 公開 API v2 は 2025-04 時点で無償(出典: https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933、見た日 2026-11-18)(資料の日付 2025-04-01)。
- 画面で Consumer Key と Consumer Secret を確かめ、アクセストークンを取って呼ぶ(出典: https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933、見た日 2026-11-18)。
- 操作できる機能: 基本情報、顔写真(登録と更新のみ)、シート、所属ツリー、ユーザー、ロール(取得のみ)、マスター、Webhook、拡張アクセス設定(出典: https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933、見た日 2026-11-18)。
- シートには、異動履歴、評価履歴、資格などを入れる(出典: https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933、見た日 2026-11-18)。
- 「スマートレビューやボイスノートなど、他の機能については API で操作できません」(出典: https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933、見た日 2026-11-18)。
- 上限は 1 時間 3,000 回。実行結果は管理者メニューで見られる。Dry-Run で検証もできる(出典: https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933、見た日 2026-11-18)。
- API キーをシート、項目、所属で絞れるかは見つからなかった。公式の MCP は見つからなかった。

### HRBrain

- 「Brain MCP」は外部の生成 AI と人材データをつなぐ基盤。2027 年以降に順次提供と報じられた(出典: https://voix.jp/?p=146490、見た日 2026-11-18)(報道、記事の日付 2026-10-27)。
- 生のデータを外に送らず、HRBrain の側で検索と集計をして「集計結果のみ」を返す設計(出典: https://voix.jp/?p=146490、見た日 2026-11-18)(報道)。
- 2026-04 から、社内向けの生成 AI「Brain」は提供中(出典: https://voix.jp/?p=146490、見た日 2026-11-18)(報道)。
- Yoom には HRBrain のメンバーの取得、検索、登録、更新のアクションがある(出典: https://lp.yoom.fun/apps/hrbrain、見た日 2026-11-18)(連携先の資料)。
- 公式の公開 API の仕様書、認証、利用条件は見つからなかった。

### Lattice

- API で読めるもの: 利用者、部署、評価サイクル、評価、評価対象者、質問、フィードバック、目標、目標の更新、近況の更新(updates)、タスク、コンピテンシー、独自属性(出典: https://developers.lattice.com/、見た日 2026-11-18)。
- API の書き込みは目標の作成、更新、進み具合の更新だけ(出典: https://developers.lattice.com/、見た日 2026-11-18)。
- 認証は Bearer の API キー。キーは作った人のアクセスをそのまま引き継ぐ。スコープの記載はない(出典: https://developers.lattice.com/docs/authentication-1.md、見た日 2026-11-18)。
- Lattice MCP は 2026-07-07 に「available now」。米国と EMEA のデータ保管の全顧客が対象(出典: https://lattice.com/blog/introducing-lattice-mcp、見た日 2026-11-18)(会社の発表)。
- MCP は本人のログインと権限を使う。目標、フィードバック、1on1、過去の評価を読める。上司は評価の下書きと提出もできる(出典: https://lattice.com/blog/introducing-lattice-mcp、見た日 2026-11-18)(会社の発表)。
- 2026-08 に、更新の提出、フィードバックの依頼と提出が加わった。EU のデータ保管の顧客にも広げた(出典: https://lattice.com/blog/august-2026-product-updates、見た日 2026-11-18)(会社の発表)。
- MCP の段階: ベータの表記はない。プラン条件は書かれていない。

### Culture Amp

- API は全プランで使える。追加料金はない(出典: https://support.cultureamp.com/en/articles/8675294-faqs-culture-amp-api、見た日 2026-11-18)。
- API は外へ出すだけ。データの取り込み(書き込み)は今はできない(出典: https://support.cultureamp.com/en/articles/8675294-faqs-culture-amp-api、見た日 2026-11-18)。
- 従業員のデータは今の状態だけ。ほかの領域は数年分さかのぼれるものもある(出典: https://support.cultureamp.com/en/articles/8675294-faqs-culture-amp-api、見た日 2026-11-18)。
- 資格情報は Account Owner の権限を持つ管理者だけが作れる。会社単位で、権限の範囲の全データに届く(出典: https://docs.api.cultureamp.com/docs/customer-guide-getting-credentials、見た日 2026-11-18)。
- 認証は OAuth 2.0 の client credentials。スコープは「対象:ID:権限の列」の形。トークンは約 1 時間の JWT(出典: https://docs.api.cultureamp.com/reference/authentication、見た日 2026-11-18)。
- 同じページの応答の例に `employees-read` と `performance-evaluations-read` が並ぶ。推測: 評価を読むにはこの権限が要る。
- 開発者サイト(developer.cultureamp.com)はサインインの画面だった。MCP は見つからなかった。

## ATS

### HERP Hire

- 認証は Bearer の API キー。発行できるのは管理者権限を持つ利用者だけ(出典: https://public-api.herp.cloud/hire/public/doc、見た日 2026-11-18)。
- 使えるのは有料プランの契約者だけ(出典: https://public-api.herp.cloud/hire/public/doc、見た日 2026-11-18)。
- スコープは資源 × 読み書き。`candidacy:read`、`requisition:write`、`user:read` など(出典: https://public-api.herp.cloud/hire/public/doc、見た日 2026-11-18)。
- 読めるもの: 応募、応募ファイル、コンタクト、タイムラインのコメント、評価、担当、職種、ユーザー、エージェント(出典: https://public-api.herp.cloud/hire/public/doc、見た日 2026-11-18)。
- 書けるもの: 応募の追加、選考ステップの更新、選考の終了、評価の記入、担当の割り当て、職種の追加(出典: https://public-api.herp.cloud/hire/public/doc、見た日 2026-11-18)。
- 上限はテナントごとに 1 分 100 回(出典: https://public-api.herp.cloud/hire/public/doc、見た日 2026-11-18)。
- 求人ごとの絞り込みと MCP の記載はなかった。

### HRMOS採用

- 2026-08-31 に API の提供を「決定」したと発表した。提供時期は未定(出典: https://hrmos.co/info/news/20260831-2/、見た日 2026-11-18)(会社の発表)。
- 予定の機能: 選考情報と応募者情報の取得、選考評価の登録(出典: https://hrmos.co/info/news/20260831-2/、見た日 2026-11-18)。
- 対象は「選考フロー管理機能」を使う環境の、「選考フロー設定あり」の求人の応募者(出典: https://hrmos.co/info/news/20260831-2/、見た日 2026-11-18)。
- 費用、認証、他社の開発者の条件は書かれていない。段階は「発表のみ」。

### Greenhouse

- Harvest v1/v2 は 2026-08-31 に削除の予定と書かれている(出典: https://docs.greenhouse.io/harvest.html、見た日 2026-11-18)。今日はその日を過ぎている。今も動くかは確かめていない。
- v1/v2 のキーはエンドポイントごとに許可する。書き込みには「監査のため」実行者の ID を送る(出典: https://docs.greenhouse.io/harvest.html、見た日 2026-11-18)。
- v3 は OAuth 2.0。自社の連携は client credentials。パートナーは authorization code(出典: https://harvestdocs.greenhouse.io/docs/authentication、見た日 2026-11-18)。
- v3 は `sub` で利用者を指定し、その人の権限で動く。一覧の API は Site Admin の認可が要る(出典: https://harvestdocs.greenhouse.io/docs/authentication、見た日 2026-11-18)。
- MCP と動的登録のクライアントは PKCE つきの authorization code を使う(出典: https://harvestdocs.greenhouse.io/docs/authentication、見た日 2026-11-18)。
- パートナーは契約の署名が先。資格情報は Partner Support に頼む。スコープの例は `harvest:job_posts:list`(出典: https://harvestdocs.greenhouse.io/docs/harvest-partner-oauth、見た日 2026-11-18)。
- パートナーの申し込みには、共通の顧客が 1 社以上と、プライバシーポリシーのあるサイトが要る(出典: https://www.greenhouse.com/integration-partner、見た日 2026-11-18)。
- MCP は Open Beta。Core、Plus、Pro の全利用者が対象。ページの日付は 2026-07(出典: https://www.greenhouse.com/product-features/greenhouse-mcp、見た日 2026-11-18)。

### Ashby

- API キーの Basic 認証。キーごとに 13 のモジュールの読み書きを選ぶ(出典: https://developers.ashbyhq.com/docs/authentication、見た日 2026-11-18)。
- 機密の求人と非公開の項目は既定で見えない。管理者が別に許す(出典: https://developers.ashbyhq.com/docs/authentication、見た日 2026-11-18)。
- `X-On-Behalf-Of` で操作を特定の利用者のものにできる(出典: https://developers.ashbyhq.com/docs/authentication、見た日 2026-11-18)。
- MCP はベータ。2026-06-22 作成の文書。入出力は予告なく変わりうる(出典: https://docs.ashbyhq.com/ashby-mcp-server-beta、見た日 2026-11-18)。
- MCP は本人の OAuth。本人が見られるデータだけ返す。組織の管理者がオンにする(出典: https://docs.ashbyhq.com/ashby-mcp-server-beta、見た日 2026-11-18)。
- MCP の書き込み: 候補者の作成、メモの下書き、ステージの移動、求人への追加(出典: https://docs.ashbyhq.com/ashby-mcp-server-beta、見た日 2026-11-18)。
- 全プランで使える。分析だけの契約は対象外(出典: https://docs.ashbyhq.com/ashby-mcp-server-beta、見た日 2026-11-18)。
- パートナーは紹介の面談、法務の確認、サンドボックス、デモの承認を経て Marketplace に載る。費用は書かれていない(出典: https://www.ashbyhq.com/integrations、見た日 2026-11-18)。

### Workable

- API トークンは管理画面の「Integrations」で作る。スコープはフォームで選ぶ。`r_employees` は機密の従業員データに届く(出典: https://workable.readme.io/reference/generate-an-access-token、見た日 2026-11-18)。
- MCP は `https://mcp.workable.com/mcp`。OAuth 2.0 と動的なクライアント登録に対応(出典: https://workable.readme.io/reference/workable-mcp-server、見た日 2026-11-18)。
- MCP の道具は約 94。読み取り約 55、書き込み約 39。求人、候補者、オファー、従業員、休暇、勤怠、評価にわたる(出典: https://workable.readme.io/reference/workable-mcp-server、見た日 2026-11-18)。
- 道具は本人が見られる範囲、できる範囲に絞られる(出典: https://workable.readme.io/reference/workable-mcp-server、見た日 2026-11-18)。
- 評価の提出や署名は取り消せない。文書は先に本人に確かめるよう書く(出典: https://workable.readme.io/reference/workable-mcp-server、見た日 2026-11-18)。
- 段階とプラン条件は書かれていない。文書の最終更新は 2026-07-16。

## 統合 API

### Merge

- 料金: Launch は 3 接続(Linked Account)まで無料。月 650 ドルで 10 接続まで。それを超えると 1 接続 65 ドル。Professional と Enterprise は契約で決める(出典: https://www.merge.dev/pricing、見た日 2026-11-18)。
- Launch は同期が 1 日 1 回、ログの保存は 3 日(出典: https://www.merge.dev/pricing、見た日 2026-11-18)。
- HRIS の共通モデルは 15: BankInfo、Benefit、Company、Dependent、EmployeePayrollRun、Employee、EmployerBenefit、Employment、Group、Location、PayGroup、PayrollRun、TimeOff、TimeOffBalance、TimesheetEntry(出典: https://docs.merge.dev/merge-unified/llms.txt、見た日 2026-11-18)。
- ATS の共通モデルは 17。Candidate、Application、Job、Scorecard、Offer、ScheduledInterview など(出典: https://docs.merge.dev/merge-unified/llms.txt、見た日 2026-11-18)。
- HRIS に評価のモデルはない(出典: https://docs.merge.dev/merge-unified/llms.txt、見た日 2026-11-18)。
- スコープは共通モデル単位。モデルを止めると、その項目もすべて止まる。連携先ごとのスコープもある(出典: https://docs.merge.dev/merge-unified/hris/data-management/scopes.md、見た日 2026-11-18)。
- 共通モデルにない項目は Remote Data で元の形のまま取れる。ただし Professional か Enterprise だけ(出典: https://docs.merge.dev/merge-unified/supplemental-data/remote-data.md、見た日 2026-11-18)。
- Agent Handler は 190 を超える MCP 対応のコネクタを持つ。誰が、どの道具を、誰の代わりに呼んだかを監査の記録に残す(出典: https://docs.merge.dev/merge-agent-handler、見た日 2026-11-18)。段階は書かれていない。
- Agent Handler の料金: Free は月 2,000 クレジット。Pro は月 1,000 ドルで 25,000 クレジット(出典: https://www.merge.dev/pricing/agent-handler、見た日 2026-11-18)。
- 国内のサービスへの対応は確かめられなかった。連携の一覧は最初のページ(J まで)しか読めず、freee、HERP、HRMOS はそこになかった(出典: https://www.merge.dev/integrations、見た日 2026-11-18)。

### Finch

- 料金: Starter は 1 接続月 65 ドル、15 接続まで、24 社の連携先。Pro と Premier は営業に問い合わせ、250 社超(出典: https://www.tryfinch.com/pricing、見た日 2026-11-18)。
- 無料のプランはない。模擬データのサンドボックスは無料(出典: https://www.tryfinch.com/pricing、見た日 2026-11-18)。
- 連携の型は 2 つ。自動型は 30 社超(書き込み 5 社)、24 時間ごとに同期。補助型は 175 社超、7 日ごとに更新、Pro 以上だけ(出典: https://developer.tryfinch.com/integrations/integration-types.md、見た日 2026-11-18)。
- 補助型は、雇用主が Finch 用の管理者の利用者を作る。初めの設定に 1〜2 週間かかる(出典: https://developer.tryfinch.com/integrations/integration-types.md、見た日 2026-11-18)。
- 許可するのは、全社の名簿と全社の給与を見られる雇用主の管理者だけ(出典: https://developer.tryfinch.com/how-finch-works/finch-connect、見た日 2026-11-18)。
- Finch MCP サーバーはベータ。トークンは接続 1 つにつき 1 つ。読み取り専用のトークンを勧める(出典: https://developer.tryfinch.com/developer-resources/Finch-MCP-Server.md、見た日 2026-11-18)。
- 国内のサービスへの対応は確かめていない。

### Kombo

- 料金は公開していない。年額の基本料と、接続した顧客ごとの料金。使っていない接続は課金しない(出典: https://www.kombo.dev/pricing、見た日 2026-11-18)。
- Start は読み取りだけ。読み書きは Scale から(出典: https://www.kombo.dev/pricing、見た日 2026-11-18)。
- 区分は ATS、HRIS と給与、適性検査と経歴確認、LMS(出典: https://www.kombo.dev/pricing、見た日 2026-11-18)。
- 連携は 250 超。一覧に SmartHR、freee、KING OF TIME、HERP、HRMOS、ジョブカン、カオナビ、HRBrain、マネーフォワードはなかった(出典: https://www.kombo.dev/integrations、見た日 2026-11-18)。
- HRIS で読めるもの: 従業員、雇用、グループ、法人、勤務地、休暇、勤務表、評価サイクルと評価、スキル。給与明細と給与の実行も別の API にある(出典: https://docs.kombo.dev/_llms/developer-documentation/hris.txt、見た日 2026-11-18)。
- 書き込み: 従業員の作成、報酬の更新、休暇の作成と削除など(出典: https://docs.kombo.dev/_llms/developer-documentation/hris.txt、見た日 2026-11-18)。
- MCP は見つからなかった。

### Apideck

- 料金: Launch は月 599 ドルで 25 社、1 区分。Scale は月 1,299 ドルで 100 社、3 区分(出典: https://www.apideck.com/pricing、見た日 2026-11-18)。
- 項目の対応づけ(Custom Field Mapping)とデータの絞り込み(Data Scopes)は Scale から(出典: https://www.apideck.com/pricing、見た日 2026-11-18)。
- MCP サーバーは全プランに含む。Vault が認証を受け持つ(出典: https://www.apideck.com/pricing、見た日 2026-11-18)。
- HRIS で読めるもの: 従業員、会社、部署、休暇申請、給与、従業員の給与、勤務予定。給与と勤務予定は読み取りだけ(出典: https://developers.apideck.com/apis/hris/reference、見た日 2026-11-18)。
- 日本の HRIS で対応するのは Workday、SAP SuccessFactors、BambooHR、Deel、HiBob(旧版)、Remote、Sage HR の 7 つ(出典: https://www.apideck.com/integrations/country/japan/hris.md、見た日 2026-11-18)。
- 同じページは「まだ対応していない地元のシステム」として、SmartHR、KING OF TIME、freee人事労務、マネーフォワード クラウド給与、ジョブカン、ジンジャー、COMPANY を挙げる(出典: https://www.apideck.com/integrations/country/japan/hris.md、見た日 2026-11-18)。

### Unified.to

- 料金: Test は無料(30 日、月 1 万回)。Grow は月 750 ドルから(月 75 万回)。Pro は月 1,500 ドルから。Scale は月 3,000 ドルから(出典: https://unified.to/pricing、見た日 2026-11-18)。
- 課金は API の呼び出しの回数。接続の数は全プランで無制限(出典: https://unified.to/pricing、見た日 2026-11-18)。
- 連携は 2,303 超。「HR & Directory」が 949、ATS が 185(出典: https://unified.to/pricing、見た日 2026-11-18)。
- 顧客の従業員データを保存しない。毎回、元のサービスに問い合わせる(出典: https://docs.unified.to/hris/overview、見た日 2026-11-18)。
- HRIS のモデル: 福利厚生、会社、控除、端末、従業員、グループ、拠点、給与明細、休暇、勤務(出典: https://docs.unified.to/hris/overview、見た日 2026-11-18)。
- MCP サーバーは接続ごと。道具は権限や道具の名前(`list_*` など)で絞れる(出典: https://docs.unified.to/mcp、見た日 2026-11-18)。段階は「launched」とだけある。
- SmartHR の連携ページ(unified.to/integrations/smarthr)は 404 だった。国内のサービスへの対応は確かめられなかった。

## 統合 API の範囲、粗さ、料金の形

| 統合 API | 区分 | 連携先の数 | 粗さ(共通モデルで落ちるもの) | 絞れる単位 | 料金の形(公開ページ) | 国内のサービス |
|---|---|---|---|---|---|---|
| Merge | HR と給与、ATS、会計、CRM など 9 | 「数百」 | 評価のモデルなし。独自項目は Remote Data(上位プランだけ) | 共通モデル単位、連携先ごと | 接続(Linked Account)の数(3 接続無料、10 接続まで月 650 ドル、超過 1 接続 65 ドル) | 確かめられなかった |
| Finch | 人事と給与に特化 | 250 超(自動型 30 超) | 給与、控除、福利厚生に強い。評価、ATS はない | 製品(データの種類)単位。SSN は別 | 接続の数(1 接続月 65 ドル) | 確かめていない |
| Kombo | ATS、HRIS と給与、適性検査、LMS | 250 超 | 評価のモデルがある。書き込みは上位プラン | スコープあり(詳細未確認) | 非公開(年額 + 接続ごと) | 一覧になかった |
| Apideck | 12 区分 | 不明 | 給与と勤務予定は読み取りだけ。絞り込みは上位プラン | Data Scopes(Scale 以上) | 顧客の数と区分の数(25 社 1 区分で月 599 ドル) | 7 つ。SmartHR などは未対応と明記 |
| Unified.to | 39 区分 | 2,303 超 | 保存しない。毎回元に問い合わせる | MCP は道具の単位 | API の呼び出し回数(月 750 ドルから) | 確かめられなかった |

- 範囲: 評価まで共通モデルに持つのは Kombo だけだった。Merge は評価のモデルを持たない(出典: https://docs.merge.dev/merge-unified/llms.txt、見た日 2026-11-18)。Finch は給与と福利厚生に寄る(出典: https://developer.tryfinch.com/llms.txt、見た日 2026-11-18)。
- 粗さ: Merge のスコープはモデル単位で、止めると項目ごと止まる(出典: https://docs.merge.dev/merge-unified/hris/data-management/scopes.md、見た日 2026-11-18)。Finch は全社の給与を見られる管理者の許可が前提(出典: https://developer.tryfinch.com/how-finch-works/finch-connect、見た日 2026-11-18)。部署や目的で絞る仕組みは、どこにも見つからなかった。
- 鮮度: Merge の Launch は 1 日 1 回。Finch の補助型は 7 日ごと。Unified.to は保存せず毎回元に問い合わせる(出典は各節)。
- 料金の形は 3 つに分かれる。接続か顧客の数で払う(Merge と Finch は接続、Apideck と Kombo は顧客)、呼び出しの回数で払う(Unified.to)、道具の呼び出しのクレジットで払う(Merge Agent Handler)。
- 国内: 国内の主なサービスに対応すると確かめられた統合 API はなかった。Apideck は SmartHR、KING OF TIME、freee人事労務、ジョブカンなどを「まだ対応していない」と明記している(出典: https://www.apideck.com/integrations/country/japan/hris.md、見た日 2026-11-18)。

## 求人媒体の管理画面

### Indeed

- Indeed Apply は ATS の提携先向けの仕組み。Indeed と開発者契約を結び、統合ごとに申請する(出典: https://docs.indeed.com/indeed-apply/ats、見た日 2026-11-18)。
- 応募は JSON で ATS の `postUrl` に POST される。HMAC-SHA1 の署名が付く。履歴書は Base64 で入る(出典: 同上、見た日 2026-11-18)。
- 統合には通常 6 週間ほどかかる、と書いている。費用の記載はない(出典: 同上、見た日 2026-11-18)。
- Disposition Sync は、ATS での選考の状態を Indeed に返す GraphQL の API。提携先のアプリの OAuth で動く。企業の同意の記載はない(出典: https://docs.indeed.com/disposition-sync-api/disposition-sync-api-guide、見た日 2026-11-18)。
- 2026-10-31 の更新で、Disposition Sync に日本の提携先向けの検証が足された(出典: https://docs.indeed.com/release-notes、見た日 2026-11-18)。
- Retrieve Candidates API は、Indeed から企業向けに候補者の情報を取り出す API。対象は Smart Sourcing で関心を示した候補者と、Smart Screening の結果(出典: https://docs.indeed.com/candidate-sync-apis/retrieve-candidates-api/retrieve-candidates-api-guide、見た日 2026-11-18)。
  - 読める項目: 候補者は名前、メール、所在地、履歴書の URL。Smart Screening は応募の ID、Smart Fit Score、履歴書。
  - 企業の登録には、企業を表す 3-legged OAuth のトークンが要る。scope は `employer.ats_candidate.sync`。作るのは Indeed の管理者か所有者。
  - 取り出しは 2-legged のトークンで、本人の操作は要らない。
  - 日本での提供の記載はなかった。
- 追加の API 規約は、API の許可を「Indeed の裁量」とし、いつでも止められると書く(出典: https://docs.indeed.com/legal-terms/additional-api-terms-and-guidelines、見た日 2026-11-18)。
- 同じ規約は、代理店が「Indeed API を第三者のシステムに埋め込む」ことを禁じる。トークンをエンドユーザーの間で共有することも禁じる(出典: 同上、見た日 2026-11-18)。
- MCP: Indeed の MCP サーバーは求職者向けのベータ。Claude のコネクタでしか使えない。道具は求人の検索、求人の詳細、本人の履歴書、企業のデータの 4 つ(出典: https://docs.indeed.com/mcp、見た日 2026-11-18)。企業向けの MCP は見つからなかった。
- CSV: 管理画面の「応募者リストをエクスポート」で CSV を出せる。1 回 1,000 件、1 日 1 万件まで。3 か月より前の応募は出せない(出典: https://jp.indeed.com/help/employers/articles/how-to-export-candidates、見た日 2026-11-18)。
  - 条件: 企業のアカウントが「認証済み」か「スポンサー求人のみ」。2 段階認証が有効。11 日以上前に出した求人が 1 件以上ある。
  - 出せる項目の一覧は書かれていなかった。
- 応募の通知メールの仕様の一次情報は見つからなかった。

### Airワーク 採用管理(Indeed Japan)

- 提供する事業者は Indeed Japan株式会社だ。公式の「Airワーク 採用管理に関する特約事項」(2025-12-16 制定、2026-04-01 改定)は、当サービスを提供する「当社」を Indeed Japan株式会社と書く(出典: https://cdn.p.recruit.co.jp/terms/aws-t-1027/index.html、見た日 2026-11-18)。
- 2025-04 から運営会社が Indeed Japan株式会社に変わったことは、販売代理店のお知らせ(2025-03-30)で確かめた。前の運営会社は、このお知らせに書かれていない(出典: https://co-do.jp/news/oshirase/air%E3%83%AF%E3%83%BC%E3%82%AF-%E6%8E%A1%E7%94%A8%E7%AE%A1%E7%90%86%E3%81%AE%E9%81%8B%E5%96%B6%E4%BC%9A%E7%A4%BE%E5%A4%89%E6%9B%B4%E3%81%AE%E3%81%8A%E7%9F%A5%E3%82%89%E3%81%9B/、見た日 2026-11-18)。(会社の発表)
- Indeed の公式の移管の告知は見つからなかった。
- 公式の機能一覧に、無料の「応募者一覧のダウンロード」がある。「応募者情報をCSVでダウンロードできます」と書く(出典: https://airregi.jp/work/recruitment/function、見た日 2026-11-18)。
- 同じページで、他の媒体からの応募は手で登録する形だった。自動の取り込みの記載はない(出典: 同上、見た日 2026-11-18)。
- Indeed への求人の自動連携は書いている(出典: 同上、見た日 2026-11-18)。
- 外部の ATS への連携は「外部連携認証キー」で行う。キーは発行から 90 日以内に設定しないと無効になる。連携できる ATS は i-web、採用一括かんりくん、JobSuite、sonar ATS、Talentio、MOCHICA、riksak の 7 つ(2026-07-27 時点)(出典: https://faq.rct.airwork.net/hc/ja/articles/42558116110617、見た日 2026-11-18)。この本文は 403 で開けず、検索結果の抜粋で確かめた。
- ヘルプによると、新卒の応募者は一覧の書き出しに含まれない。別の画面から出す(出典: https://faq.rct.airwork.net/hc/ja/articles/35513808519833、見た日 2026-11-18)。本文は 403 で開けず、抜粋で確かめた。
- 公開の API の文書、MCP、応募の通知メールの仕様は見つからなかった。
- 推測: 連携先が提携 ATS に限られる。hiring-os が直接つなぐには、提携 ATS を経由するか、CSV の書き出しを使う形になる。

### engage(株式会社エンゲージ)

- engage の事業は、2026-04-01 にカカクコムへ株式の 85.1% が移った(出典: https://s3-ap-northeast-1.amazonaws.com/enjapanhp/wp-content/uploads/20260806153235/27.3_1Q_tanshin.pdf、見た日 2026-11-11)。既存の market.md の出典で、今回は開き直していない。
- 公式の機能のページは「応募者情報をエクセルで出力できます」と書く(出典: https://en-gage.net/function/、見た日 2026-11-18)。
- 求人の連携先は「エンゲージ」「LINEキャリア」「Google しごと検索」「スタンバイ」「求人ボックス」(出典: 同上、見た日 2026-11-18)。
- ヘルプでは CSV で書き出せる。対象は応募から 1 年以内の人(出典: https://support.en-gage.net/hc/ja/articles/900007350383、見た日 2026-11-18)。本文は 403 で開けず、抜粋で確かめた。
- 連携サービスとして採用管理の「Hirehub」を紹介している、との抜粋が出た。公式の本文は確かめていない。
- 公開の API、MCP は見つからなかった。

### その他の国内の媒体(短く)

- バイトル: 利用規約の目次は開けた。求職者向けの規約で、掲載企業向けの規約は見つからなかった(出典: https://www.baitoru.com/about/kiyaku.html、見た日 2026-11-18)。2026-03-02 の改定は dipID の導入と外部アカウントの連携の条項の追加だった(出典: https://www.baitoru.com/notifications/detail/674io6q7e、見た日 2026-11-18)。掲載企業向けの API と CSV の一次情報は見つからなかった。
- タウンワーク、マイナビバイト: 掲載企業向けの API、CSV、通知メールの一次情報は見つからなかった。
- 求人ボックス: 求人の検索の API(パブリッシャー向け)はあるとの抜粋が出た。応募のデータを企業の外に出す API は見つからなかった。「かんたん応募」は提携 ATS か「採用ボード」で使う、との報道があった(出典: https://webtan.impress.co.jp/r/prtimes/items/000000317.000071307、見た日 2026-11-18)。(会社の発表)

## メール

### Gmail(Google Workspace)

- ドメイン全体の委任は、特権管理者だけが設定できる。設定すると、アプリは「すべてのユーザー」のデータに届く(出典: https://knowledge.workspace.google.com/admin/apps/control-api-access-with-domain-wide-delegation、見た日 2026-11-18)。
- 管理者はクライアントごとに scope を並べる。Google は scope を狭くするよう勧める。2 人目の特権管理者の承認(Multi-party approval)を求める設定もある(出典: 同上、見た日 2026-11-18)。
- Gmail の scope のうち restricted は `gmail.readonly`、`gmail.metadata`、`gmail.compose`、`gmail.modify` など。`gmail.send` は sensitive(出典: https://developers.google.com/workspace/gmail/api/auth/scopes、見た日 2026-11-18)。
- アドオンの `gmail.addons.current.message.readonly` は sensitive。アドオンが動いている間だけメッセージを読める(出典: 同上、見た日 2026-11-18)。
- restricted scope の審査: データをサーバーに保存するか送るなら、Google が認めた第三者のセキュリティ評価(CASA)が要る。少なくとも 12 か月ごとに再評価する。審査は数週間かかりうる(出典: https://developers.google.com/identity/protocols/oauth2/production-readiness/restricted-scope-verification、見た日 2026-11-18)。
- 例外: 自分の Workspace の組織の中だけで使う Internal のアプリは審査が要らない(出典: 同上、見た日 2026-11-18)。
- ドメイン全体のインストールでも、restricted か sensitive の scope を使うなら審査が要る、と書いている(出典: 同上、見た日 2026-11-18)。
- 費用は、このページに記載がなかった。
- MCP: Google の公式の Gmail MCP サーバーは `https://gmailmcp.googleapis.com/mcp/v1`。Google Workspace Developer Preview Program の参加が前提(出典: https://developers.google.com/workspace/guides/configure-mcp-servers、見た日 2026-11-18)。
  - 本人の委任の OAuth で動く。OAuth のクライアントに「Use this client for an AI-powered agent」の設定が要る。
  - ドメイン全体の委任のサービスアカウントは、この設定の対象外。
  - 「ユーザーと同じ権限とデータの統制を引き継ぐ」と書いている。
- 2026-05 の発表は、Workspace の MCP サーバーを「public developer preview」にしたと書いた。2026-05-01 から順に出す(出典: https://workspaceupdates.googleblog.com/2026/05/agent-tools-and-security-updates-for-workspace-developers.html、見た日 2026-11-18)。(会社の発表)
- 同じ発表は、エージェントの道具と API に段階の仕組み(tiering)を入れると書いた。大量のデータの持ち出しを防ぐためで、上の段階が要る開発者は 1% 未満の見込み(出典: 同上、見た日 2026-11-18)。(会社の発表)

### Microsoft 365(Exchange Online、Outlook)

- RBAC for Applications は、アプリの権限をメールボックスの集まりに絞る仕組み。Application Access Policies の後継(出典: https://learn.microsoft.com/en-us/exchange/permissions-exo/application-rbac、見た日 2026-11-18)。
- 絞る単位は 2 つ。Exchange の management scope(メールボックスの属性の条件)と、Entra の管理単位(出典: 同上、見た日 2026-11-18)。
- 対象の役割は `Application Mail.Read`、`Application Mail.ReadBasic`(本文と添付を除く)、`Application Calendars.Read` など。Graph と EWS で使える(出典: 同上、見た日 2026-11-18)。
- 注意: Entra で組織全体の権限を同意したままだと、絞りは効かない。2 つの権限は足し算になる(出典: 同上、見た日 2026-11-18)。
- 設定には Exchange の Organization Management の役割が要る。変更が効くまで 30 分〜2 時間かかる(出典: 同上、見た日 2026-11-18)。
- 1 つの組織で 1 万個のアプリまで使える(出典: 同上、見た日 2026-11-18)。
- MCP: Work IQ MCP は Work IQ API の一部として一般提供(出典: https://learn.microsoft.com/microsoft-agent-365/tooling-servers-overview、見た日 2026-11-18)。
  - Work IQ は Entra の delegated の認証だけ。アプリ単独(app-only)の認証は使えない(出典: https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq/api-overview、見た日 2026-11-18)。
  - 料金は Copilot Credits の従量課金(出典: 同上、見た日 2026-11-18)。
  - メール、予定、OneDrive と SharePoint の文書、Teams のメッセージを扱う(出典: 同上、見た日 2026-11-18)。
  - 旧来の Mail、Calendar、SharePoint、OneDrive、Teams の MCP サーバーはプレビュー。本番と新しい開発には使わないよう書いている(出典: https://learn.microsoft.com/microsoft-agent-365/tooling-servers-overview、見た日 2026-11-18)。
- 管理者の同意: admin consent workflow を有効にすると、同意できない利用者が管理者に申請できる。申請はメールで審査役に届く(出典: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-admin-consent-workflow、見た日 2026-11-18)。
- Graph のアプリの権限(application permissions)を求めるアプリを承認できるのは Global Administrator だけ(出典: 同上、見た日 2026-11-18)。

## 予定

### Google Calendar

- freeBusy.query は、busy の時間帯だけを返す。空きは返さず、間から求める(出典: https://developers.google.com/workspace/calendar/api/v3/reference/freebusy/query、見た日 2026-11-18)。
- 使える scope は `calendar.freebusy`、`calendar.events.freebusy`、`calendar.readonly`、`calendar` のどれか(出典: 同上、見た日 2026-11-18)。
- 1 回で見られるカレンダーは 50 まで。グループの展開は 100 人まで(出典: 同上、見た日 2026-11-18)。
- scope の説明: `calendar.freebusy` は「カレンダーの空きを見る」。`calendar.events.owned` は自分が持つカレンダーの予定を読み書きする(出典: https://developers.google.com/workspace/calendar/api/auth、見た日 2026-11-18)。
- このページに sensitive と restricted の分類はなかった。
- MCP: Calendar MCP は `https://calendarmcp.googleapis.com/mcp/v1`。Developer Preview(出典: https://developers.google.com/workspace/guides/configure-mcp-servers、見た日 2026-11-18)。

### Microsoft Graph の予定

- getSchedule は、利用者、配布リスト、会議室の空きを返す。最小の権限は `Calendars.ReadBasic`。delegated とアプリの権限の両方で使える(出典: https://learn.microsoft.com/en-us/graph/api/calendar-getschedule、見た日 2026-11-18)。
- 返す項目は空きの状態と時間帯。例では件名と場所も返っている(出典: 同上、見た日 2026-11-18)。
- findMeetingTimes は、出席者の空きから会議の候補を出す。delegated の `Calendars.Read.Shared` だけで、アプリの権限は使えない(出典: https://learn.microsoft.com/en-us/graph/api/user-findmeetingtimes、見た日 2026-11-18)。
- アプリの権限で予定を読むなら、RBAC for Applications の `Application Calendars.Read` で対象のメールボックスを絞れる(出典: https://learn.microsoft.com/en-us/exchange/permissions-exo/application-rbac、見た日 2026-11-18)。
- 推測: 面接の日程の調整は、担当者本人の delegated で getSchedule か findMeetingTimes を呼ぶ形が一番狭い。組織全体の鍵は要らない。

## チャット

### Slack

- 2025-05-29 の変更: Marketplace に載っていない商用配布のアプリは、`conversations.history` と `conversations.replies` が 1 分に 1 回、1 回 15 件までになった(出典: https://docs.slack.dev/changelog/2025/05/29/rate-limit-changes-for-non-marketplace-apps、見た日 2026-11-18)。
  - 2025-05-29 以降に作ったアプリと、新しいインストールに効く。
  - Marketplace のアプリは変わらない。
  - 企業が自分で作った社内のアプリは、1 分 50 回以上、1 回 1,000 件のまま。
- API の規約(発効日 2025-10-10、日本語版)(出典: https://slack.com/terms-of-service/api、見た日 2026-11-18):
  - 組織の外の利用者に出すアプリは「API データを使用して大規模言語モデルをトレーニングすること」を禁じる。
  - メッセージやファイルの一括の書き出しを禁じる(別の契約で許す場合を除く)。
  - データアクセス API と Real-time Search API では、永続的なコピー、アーカイブ、インデックス、長期のデータストアを作ってはならない。
  - 利用者の問い合わせに関係のないデータを裏で集めることを禁じる。そのデータで製品を改善することも禁じる。
  - 商用の配布を認める契約は、Marketplace への参加と Marketplace 契約への同意を意味する。
  - Slack はアプリを監査する権利を持つ。
- MCP: 公式の Slack MCP サーバーは `https://mcp.slack.com/mcp`(出典: https://docs.slack.dev/ai/slack-mcp-server/、見た日 2026-11-18)。
  - 本人のトークン(user token)で動く。
  - 「unlisted apps are prohibited from using MCP」。Marketplace に載ったアプリか社内のアプリだけ使える。
  - ワークスペースの管理者が、通常のアプリの承認の流れで MCP のクライアントを承認する。監査ログに残る。
  - チャンネルの履歴、スレッド、検索、投稿、canvas の道具がある。
- Slack は 2026-02-17 に MCP サーバーと Real-time Search API の一般提供を発表した。RTS API では「ユーザーデータが外部サーバーに保管されることはありません」と書く(出典: https://slack.com/blog/news/mcp-real-time-search-api-now-available、見た日 2026-11-18)。(会社の発表)
- アプリの承認の管理のヘルプは 429 で開けなかった(https://slack.com/help/articles/222386767-Manage-app-approval-for-your-workspace)。

### Microsoft Teams

- RSC(resource-specific consent)は、アプリの権限を入れたチーム、チャット、会議だけに絞る仕組み(出典: https://learn.microsoft.com/en-us/microsoftteams/platform/graph-api/rsc/resource-specific-consent、見た日 2026-11-18)。
  - `ChatMessage.Read.Chat` はそのチャットの全メッセージを読む。`ChannelMessage.Read.Group` はそのチームのチャンネルのメッセージを読む。どちらもアプリ単独の権限。
  - delegated の RSC は、チームかチャットのメンバーなら誰でも与えられる。app-only の RSC は管理者か資源の持ち主だけ、と本文は書く。
  - RSC の権限は Entra の管理画面に出ない。Teams の画面で見る。
- テナント全体のメッセージをアプリの権限で読む API は「protected API」で、申請が要る、と Microsoft の Q&A に書かれていた(出典: https://learn.microsoft.com/en-us/answers/questions/524535/issue-with-running-get-command-within-graph-explor、見た日 2026-11-18)。(解説)公式の説明のページ(https://learn.microsoft.com/en-us/graph/teams-protected-apis)は 404 で開けなかった。
- 従量課金の API(metered API)のページは開けず、2026 年の料金は確かめていない。
- MCP: Work IQ MCP で Teams のメッセージも扱える。一般提供(出典: https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq/api-overview、見た日 2026-11-18)。

### LINE WORKS

- 認証は 2 つ。本人のログインによる OAuth 2.0(Authorization Code)と、Service Account の JWT(出典: https://developers.worksmobile.com/jp/docs/auth、見た日 2026-11-18)。
- Service Account は「アプリ専用の仮想管理者アカウントです」。bot や一括処理向け(出典: 同上、見た日 2026-11-18)。
- 本人の OAuth では、使える範囲は本人の権限と scope の重なりになる(出典: 同上、見た日 2026-11-18)。
- scope には `mail.read`、`calendar.read`、`file.read`、`bot` などがある。使える scope はドメインのプランで変わる(出典: https://developers.worksmobile.com/jp/docs/auth-scope、見た日 2026-11-18)。
- 公式の MCP サーバーは見つからなかった。非公式の「nworks」はある(出典: https://glama.ai/mcp/servers/yjcho9317/nworks/inspect、見た日 2026-11-18)。(解説)

### Chatwork

- OAuth 2.0 は Authorization Code だけ。アクセストークンは 30 分、リフレッシュトークンは 14 日(`offline_access` なら無期限)(出典: https://developer.chatwork.com/docs/oauth、見た日 2026-11-18)。
- scope は `rooms.messages:read`、`rooms.tasks:read`、`rooms.files:read` など。ルームの単位の scope はない(出典: 同上、見た日 2026-11-18)。
- 従来の API トークンの方式もある(出典: 同上、見た日 2026-11-18)。
- MCP: Chatwork の GitHub の組織に MCP サーバーがある。31 の道具。API トークンで動き、OAuth には対応しないと書く。段階の表示はない(出典: https://github.com/chatwork/chatwork-mcp-server、見た日 2026-11-18)。
- API トークンの発行に組織の管理者の承認が要るかは、ヘルプが 403 で開けず不明。

## 文書の置き場

### Google Drive

- `drive.file` は non-sensitive。本人がアプリで開いたファイルか、アプリに渡したファイルだけに届く。Google Picker と組み合わせる(出典: https://developers.google.com/workspace/drive/api/guides/api-specific-auth、見た日 2026-11-18)。
- `drive.readonly`、`drive`、`drive.metadata.readonly` は restricted。restricted の用途は、バックアップと同期、生産性と教育、報告とセキュリティに限る(出典: 同上、見た日 2026-11-18)。
- Google は既存のアプリにも、restricted から `drive.file` への移行を勧める(出典: 同上、見た日 2026-11-18)。
- MCP: Drive MCP は `https://drivemcp.googleapis.com/mcp/v1`。Developer Preview(出典: https://developers.google.com/workspace/guides/configure-mcp-servers、見た日 2026-11-18)。

### SharePoint と OneDrive

- Selected scope は 4 つ。`Sites.Selected`、`Lists.SelectedOperations.Selected`、`ListItems.SelectedOperations.Selected`、`Files.SelectedOperations.Selected`(出典: https://learn.microsoft.com/en-us/graph/permissions-selected-overview、見た日 2026-11-18)。
- 同意しただけでは何も読めない。資源ごとに権限を付ける操作が要る(出典: 同上、見た日 2026-11-18)。
- 与える役割は read、write、owner、fullcontrol(出典: 同上、見た日 2026-11-18)。
- delegated では、アプリの権限と本人の権限の重なりになる。アプリが本人を超えることはない(出典: 同上、見た日 2026-11-18)。
- サイトの単位で権限を付けるには `Sites.FullControl.All` が要る(出典: 同上、見た日 2026-11-18)。
- MCP: Work IQ MCP で OneDrive と SharePoint の文書を扱う。一般提供(出典: https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq/api-overview、見た日 2026-11-18)。

### Box

- OAuth 2.0 の利用者のアプリは、企業の設定によって管理者の有効化が要る。JWT と CCG のサーバーのアプリは、管理者の承認が要る(出典: https://developer.box.com/guides/authentication/、見た日 2026-11-18)。
- サービスアカウントは空のフォルダーから始まる。共同作業者として招かれたフォルダーだけを見る(出典: 同上、見た日 2026-11-18)。
- MCP: Box のリモート MCP サーバーは `https://mcp.box.com`。管理者が Admin Console で有効にする。「Users can only access content they already have permission to view or edit in Box」(出典: https://developer.box.com/guides/box-mcp/remote/、見た日 2026-11-18)。
- 段階(ベータか一般提供か)は文書に書かれていなかった。

### Dropbox

- アクセスの型は 2 つ。App Folder はアプリのフォルダーだけ。Full Dropbox は利用者の全データ(出典: https://docs.dropboxapi.com/dropbox-api/docs/oauth、見た日 2026-11-18)。
- チームの scope のトークンは、承認した管理者ではなくチームに結びつく(出典: 同上、見た日 2026-11-18)。
- MCP: 公式のリモート MCP サーバーは `https://mcp.dropbox.com/mcp`。オープンベータ(出典: https://help.dropbox.com/integrations/connect-dropbox-mcp-server、見た日 2026-11-18)。
- チームの管理者は、利用者がアプリを作るのを止められる(出典: 同上、見た日 2026-11-18)。

## API のないシステムへの道

### (a) 担当者の PC の bot が画面を操作する

- Claude の computer use: 今の版 `computer_toolset_20260801` はベータのヘッダーが要らない。SDK のクラスはベータ(出典: https://platform.claude.com/docs/en/agents-and-tools/tool-use/computer-use-tool、見た日 2026-11-18)。
  - 勧める対策: 専用の VM かコンテナで最小の権限。ログイン情報を渡さない。ドメインの許可リスト。結果の大きい操作は人が確認する。
  - 画面の中の指示に従ってしまう場合がある(prompt injection)、と書いている。
  - 製品に入れるときは、利用者にリスクを伝え、同意を取るよう求める。
- OpenAI の computer use: `computer` ツールは今も使える。`computer-use-preview` からの移行の節がある(出典: https://developers.openai.com/api/docs/guides/tools-computer-use、見た日 2026-11-18)。
  - 勧める対策: 隔離したブラウザか VM。結果の大きい操作は確認する。資格情報を画面に出さない。
  - 段階(ベータか一般提供か)の表示はなかった。
- Microsoft Copilot Studio の computer use: Windows の PC の上で、画面を操作して Web とデスクトップのアプリを動かす。PC は Power Automate のマシンとして登録する(出典: https://learn.microsoft.com/en-us/microsoft-copilot-studio/computer-use、見た日 2026-11-18)。
  - 資格情報は「作った人のもの」か「使う人のもの」を選ぶ。作った人のものでエージェントを共有すると、誰でも作った人の権限で動かせる、と警告している。
  - 操作できるサイトとアプリを許可リストで絞れる。ただし開くことは止めない。
  - 1 ステップ 5 Copilot Credits(上位のモデルは 15)。
  - 専用の PC、最小の権限、Intune での Edge の制限、App Control でのアプリの制限を勧める。
- UiPath と Power Automate Desktop 単体の条件は、今回は調べていない。

### (b) ブラウザの拡張

- Chrome の管理者は、`ExtensionSettings` で拡張を許可、禁止、強制インストールできる。`*` を禁止にして、許可する拡張だけを並べられる(出典: https://support.google.com/chrome/a/answer/7532015、見た日 2026-11-18)。
- `runtime_blocked_hosts` で、拡張が特定のサイトに触れるのを止められる(出典: 同上、見た日 2026-11-18)。
- Chrome Enterprise のポリシーの一覧のページは、本文が取れなかった(https://chromeenterprise.google/policies/#ExtensionInstallAllowlist)。

### (c) CSV の書き出し

- Indeed、Airワーク、engage はどれも管理画面から応募者を書き出せる(各節を参照)。
- Indeed は 2 段階認証と、1 回 1,000 件などの上限がある(出典: https://jp.indeed.com/help/employers/articles/how-to-export-candidates、見た日 2026-11-18)。
- 推測: CSV は規約の上で一番安全な道。ただし担当者の手作業が残り、間隔も空く。

### 規約の問題

- Indeed(利用規約、2026-09-29 更新)(出典: https://www.indeed.com/legal、見た日 2026-11-18):
  - D.21: 「Use any automated system (bots, scrapers, spiders, AI or Agentic AI) to access, data-mine」を禁じる。
  - D.21: Indeed が用意した公開の窓口以外での利用を禁じる。
  - D.21: 第三者の機械学習のモデルの開発や学習のために使うことを禁じる。
  - D.22(4): scraping と bot の禁止は残したまま、Indeed は「Permitted AI Connector」で外部の AI につなぐ道を出しうる。ベータで、いつでも止められる。
  - D.7.2: 他人や自動のシステムにアカウントを使わせた場合、その行為の責任は本人が負う。
- LinkedIn(利用規約、2025-11-03 発効)の 8.2 は、ソフト、スクリプト、ロボット、クローラー、ブラウザのプラグインとアドオンで scraping することを禁じる。bot での自動のアクセスも禁じる(出典: https://www.linkedin.com/legal/user-agreement、見た日 2026-11-18)。
- SmartHR(利用規約、最終改定 2026-05-26)(出典: https://smarthr.jp/terms/terms-smarthr/、見た日 2026-11-18):
  - 第 12 条 14 号: 「スクレイピング等、手段を問わず、本サービスの仕様若しくは情報、又は他のユーザーの情報を収集する行為」を禁じる。
  - 第 10 条の 2: スクリプトや bot で AI 機能にアクセスすることを禁じる。
  - 第 17 条: API 連携サービスの利用の結果は、利用ユーザーが自ら責任を負う。
- Slack の API の規約は、上の「Slack」の節を参照。
- 推測: Indeed と SmartHR の文言は、画面の操作の bot も「自動の手段」に入る書き方だ。担当者の PC から動かしても、規約の上の扱いは変わらない可能性が高い。

### 権限の問題

- 画面を操作する bot は、担当者のログインのまま動く。scope のような絞りはない。
- Copilot Studio は、作った人の資格情報で共有すると誰でもその権限で動かせる、と警告している(出典: https://learn.microsoft.com/en-us/microsoft-copilot-studio/computer-use、見た日 2026-11-18)。
- Claude の文書は、モデルにログイン情報を渡さないよう勧めている(出典: https://platform.claude.com/docs/en/agents-and-tools/tool-use/computer-use-tool、見た日 2026-11-18)。
- 推測: API なら「応募者を読む」だけに絞れる。画面の操作では、担当者が人事のシステムで見られるもの全部に届いてしまう。監査の記録も、担当者本人の操作と区別しにくい。

## 担当者の PC に bot を入れるときの IT の承認

### 端末の管理(Windows)

- Intune の App Control for Business は、許可していないアプリの実行を止める。監査のモードもある(出典: https://learn.microsoft.com/en-us/intune/intune-service/protect/endpoint-security-app-control-policy、見た日 2026-11-18)。
- Intune で配ったアプリは「managed installer」の印が付き、信頼される。それ以外のアプリは、追加のポリシーで許可する(出典: 同上、見た日 2026-11-18)。
- 推測: 管理の厳しい企業では、bot は Intune から配ってもらう必要がある。担当者が自分で入れる形は通らない。

### 端末の管理(macOS)

- Apple の構成プロファイルでは、画面の収録(ScreenCapture)とキー入力の監視(ListenEvent)を許可できない。「A profile can't grant access to the contents; it can only deny it」(出典: https://raw.githubusercontent.com/apple/device-management/release/mdm/profiles/com.apple.TCC.configuration-profile-policy.yaml、見た日 2026-11-18)。
- できるのは、管理者でない利用者が自分で許可できるようにする設定(`AllowStandardUserToSetSystemService`)だけ(出典: 同上、見た日 2026-11-18)。
- Accessibility は設定できる。ただし macOS 27.0 では通知が出て、利用者が設定を変えられる(出典: 同上、見た日 2026-11-18)。
- 同じ出典で、Accessibility、Camera、Microphone、SpeechRecognition、BluetoothAlways などの鍵は macOS 27.0 で廃止(deprecated)の扱いだ。代わりに、宣言型の管理の構成 `com.apple.configuration.app.settings` の `Privacy` の鍵を使うよう書く。ScreenCapture と ListenEvent には、廃止の記載がない(出典: 同上、見た日 2026-11-18)。移った先の `Privacy` の鍵で何を許可できるかは調べていない。
- この設定は監視対象(supervised)の端末で、MDM から入れる(出典: https://support.apple.com/guide/deployment/privacy-preferences-policy-control-payload-dep38df53c2a/web、見た日 2026-11-18)。
- Jamf の手順は調べていない。推測: Jamf も同じ Apple の仕組みを使うので、画面の収録は担当者本人の許可が要る。

### OAuth アプリの管理者の同意

- Microsoft Entra: admin consent workflow で、利用者は同意できないアプリを申請できる。アプリの権限の承認は Global Administrator だけ(出典: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-admin-consent-workflow、見た日 2026-11-18)。
- Google Workspace: 管理者はアプリごとに Trusted、Limited、Specific Google data、Blocked を選ぶ(出典: https://knowledge.workspace.google.com/admin/apps/control-which-apps-access-google-workspace-data、見た日 2026-11-18)。
  - Gmail や Drive を「Restricted」にすると、Trusted か Specific のアプリだけが読める。
  - Gmail、Drive、Docs、Chat は、メールの送信やファイルの削除など高リスクの scope だけを止められる。
  - 未設定のアプリを全部止める設定がある。その場合、利用者の申請が「Apps pending review」に並ぶ。

### Slack のアプリの承認

- Slack MCP のクライアントは、ワークスペースの管理者が通常のアプリの承認の流れで承認する(出典: https://docs.slack.dev/ai/slack-mcp-server/、見た日 2026-11-18)。
- アプリの承認のヘルプのページは 429 で開けなかった。

### Chrome 拡張の許可リスト

- 上の「(b) ブラウザの拡張」を参照。

### 国内の情報システム部門の審査の慣行

- 利用企業が SaaS の事業者にセキュリティチェックシートの記入を頼むのは「一般的なプロセス」。大企業を中心に導入の必須条件にする例が増えている(出典: https://www.itmedia.co.jp/news/article/2501/30/1250130007/、見た日 2026-11-18)。(報道)
- 項目は「個社ごとに内容は異なる」ため、回答の標準化が難しい(出典: 同上、見た日 2026-11-18)。(報道)
- アシュアードの 2025 年の 2,609 件の評価では、利用者の多要素認証の実施率が 53.0%。インシデント対応の体制は 35.0%(出典: https://atmarkit.itmedia.co.jp/ait/articles/2601/13/news041.html、見た日 2026-11-18)。(報道)
- 経済産業省の SCS 評価制度は、取引先ごとに違う対策の要求をそろえる制度。★3 と ★4 は 2026 年度末ごろに申請を始める予定、との検索結果の抜粋が出た(出典: https://www.meti.go.jp/policy/netsecurity/scs.html、見た日 2026-11-18)。このページと発表の資料は 403 で開けず、本文は確かめていない。
- ISMAP は、政府のクラウドの調達のセキュリティの水準を確保する制度。ISMAP-LIU は、機密性 2 の情報を扱う SaaS のうち、リスクの小さな業務向け(出典: https://www.digital.go.jp/policies/security/ismap-liu、見た日 2026-11-18)。
- 推測: ISMAP は官公庁に売るときの条件で、民間の採用の現場で求められる場面は限られる。
- 民間企業が ISMS や SOC 2 をどのくらい求めるかの数字は、公開の資料で見つからなかった。

## このプロダクトへの示唆

人事のシステムと ATS(上の「人事労務」から「統合 API」)と、求人媒体、メール、予定、チャット、文書、IT の承認(上の「求人媒体の管理画面」から後)に分けて書く。

### 人事のシステムと ATS(事実)

- 国内の人事労務と勤怠は、自前でつなぐしかない。統合 API の対応を確かめられなかった。Apideck は未対応と明記していた。
- 国内で外部の開発者がすぐ始められるのは SmartHR(利用者は無料、手続き不要)、freee人事労務(開発者アカウント無料、OAuth)、HERP Hire(有料プランの顧客が管理者キーを発行)、カオナビ(無償)だった。
- 申請や問い合わせが要るのは KING OF TIME(サポートセンター)、ジョブカン(利用申請)。HRMOS採用は API がまだない。マネーフォワード クラウド給与と Airシフトは公開 API が見つからなかった。
- 海外の給与は門が固い。Gusto はパートナー限定で、実績の少ない初期の製品は対象外。ADP は参加契約、Marketplace の掲載、SSO、セキュリティ審査が要る。
- MCP は「本人のログインと権限」の形にそろってきた。HiBob、BambooHR、Ashby、Workable、Lattice、Gusto、ADP がそうだ。HiBob はサービス用の利用者での新しい接続を 2026-11-09 に止めた。ADP も組織全体の権限は「coming soon」。
- 管理者キーの形が残るのは API の側だ。SmartHR、KING OF TIME、HERP Hire、7shifts、Culture Amp は管理者が発行するキーやトークンで動く。
- 統合 API は海外の ATS と HRIS を広く押さえる。料金は 1 接続あたり月 65 ドル前後からで、接続の数で増える(Merge、Finch)。

### 人事のシステムと ATS(推測: 最初につなぐ順)

- 推測: 1 番目は freee人事労務。OAuth で、人事、勤怠、給与明細を 1 つの API で読める。公式の MCP もある。Airシフトからは概算人件費が freee に送られるので、店舗の会社の人件費の一部も拾える。勤怠は送られない。
- 推測: 2 番目は SmartHR。従業員のマスターとして広く使われ、API は無料で手続きもない。ただし勤怠と給与は別のサービスにある。
- 推測: 3 番目は ATS の HERP Hire。応募の追加と評価の記入まで API でできる。採用の bot には一番近いデータだ。HRMOS採用は API の提供を待つ。
- 推測: 勤怠は KING OF TIME とジョブカンが大きいが、どちらも申請や問い合わせが要る。先に申請だけ出しておくとよい。
- 推測: 店舗のアルバイト向けは、Airシフトに API がない。道は CSV(画面からの書き出し)だけになる。画面を操作する bot は、PRD の D15 で使わない。freee人事労務へ送られるのは概算人件費で、勤怠は送られない。Airシフトの CSV の書き出しの中身は、この調べでは確かめていない。海外の 7shifts と Deputy は API が開いている。

### 人事のシステムと ATS(推測: 統合 API か自前か)

- 推測: 国内の顧客が先なら自前でつなぐ。統合 API は国内のサービスに届かないためだ。
- 推測: 海外の ATS と HRIS は統合 API が速い。特に ATS は Kombo と Merge が Greenhouse、Ashby、Lever、Workable を押さえている。
- 推測: 統合 API は粗い。モデル単位のスコープでは「目的ごとの小さな資格」を作れない。hiring-os の側で項目を落とす層が要る。
- 推測: 給与は統合 API(Finch)経由が現実的だ。Gusto と ADP に直接パートナーとして入るのは、実績と審査の壁が高い。
- 推測: MCP は「人事の担当者本人の権限」で動く形が主流になった。企業の bot を担当者の PC に入れる hiring-os の形とは合う。担当者がログインし、その人の権限で読む設計にすると、ベンダーの方向とぶつからない。

### 求人媒体、メール、予定、チャット、文書、IT の承認(事実)

- 求人媒体の大手は、応募を企業の外に出す API を ATS の提携先にしか開いていない。Indeed は開発者契約と Indeed の裁量、Airワーク は提携 ATS 7 社だった。
- 国内の媒体(engage、バイトル、タウンワーク、マイナビバイト)で、企業が使える公開 API は見つからなかった。確かめられた外への口は、管理画面の CSV の書き出しだけだった。
- Indeed、LinkedIn、SmartHR の規約は、bot や scraping による自動のアクセスを禁じている。Indeed は「AI or Agentic AI」も明記した。
- メールと予定には、管理者が絞れる仕組みがある。Exchange は RBAC for Applications でメールボックスの集まりに絞れる。Google はドメイン全体の委任を全利用者に効かせ、絞るのは scope だけ。
- Gmail と Drive の広い読み取りは restricted で、外部のサーバーに置くなら 12 か月ごとの第三者の評価が要る。`drive.file` と freeBusy の scope は狭い。
- Slack は 2025 年から、Marketplace 外の商用アプリの履歴の取得を 1 分 1 回に絞り、LLM の学習と一括の書き出しを禁じた。MCP も Marketplace か社内のアプリだけが使える。
- Microsoft の Work IQ MCP は一般提供だが、delegated だけで、Copilot Credits の従量課金。Google の Workspace MCP は Developer Preview。
- macOS では、画面の収録の許可を MDM で配れない。担当者本人がオンにする必要がある。

### 求人媒体、メール、予定、チャット、文書、IT の承認(推測)

- hiring-os が「担当者の PC の bot」を使うと、IT の承認は最大 4 段重なる。端末(Intune か MDM)、OAuth アプリの同意(Entra か Google)、チャット(Slack のアプリの承認)の 3 つに、事業者の審査(セキュリティチェックシート。報道)が加わる。
- 最初につなぐ相手は、規約と承認の軽い順に選ぶのがよい。候補は、担当者本人の OAuth による予定の空き(freeBusy、getSchedule)、`drive.file`、Exchange の RBAC で絞ったメールボックス。
- Gmail の本文を読むには restricted scope の審査が要る。初期は、担当者が応募の通知メールを専用の宛先に転送する形か、Gmail アドオンの狭い scope で避けられる。
- Slack は Marketplace に載るまで、他社のワークスペースの履歴を実用の速さで読めない。初期は通知の投稿(書き込み)に絞るのが現実的だ。
- 求人媒体の応募は、ATS の提携の道(Indeed など)か、CSV の取り込みになる。画面の操作の bot は、Indeed と SmartHR の規約に触れる可能性が高い。
- 画面の操作の bot は、担当者の全権限で動き、監査で本人と区別しにくい。情報システム部門の審査では最も通りにくい形になりそうだ。
- 国内の大企業に売るなら、セキュリティチェックシートへの回答の準備が要る。SCS 評価制度の ★3 か ★4 が、今後の共通の物差しになる可能性がある。

## 見つからなかったこと

### 人事のシステムと ATS

- SmartHR のトークンをエンドポイントや項目で絞る仕組みの公開文書(説明のヘルプは今回開いていない)。SmartHR Plus にアプリを載せる条件。
- freee のアプリストアに公開アプリを載せる審査と費用。
- KING OF TIME とジョブカンの、プラン条件と費用。ジョブカンの公式の API 仕様書(api.jobcan.ne.jp は 404)。
- Airシフト、マネーフォワード クラウド給与、マネーフォワード クラウド人事管理の公開 API。
- ジョブカン労務HR とジンジャー勤怠は今回調べていない。
- HRBrain の公式の API 仕様書と利用条件。
- Lattice、Workable、BambooHR、HiBob、Rippling、Deputy の、API が使えるプランの条件。
- Rippling の App Shop の条件と、Rippling MCP の段階。
- Deputy のトークンが承認した人の権限に絞られるか。
- Culture Amp の MCP。開発者サイト(developer.cultureamp.com)はサインインの画面だった。
- Merge、Finch、Unified.to が国内のサービスに対応するか。
- Kombo の認証方式とスコープの細かさ。
- Merge Agent Handler、Unified.to MCP、Apideck MCP、Workable MCP、Lattice MCP、Gusto MCP、freee-mcp の提供の段階(どれもベータか一般提供かの表記がない)。
- ADP の API Central の料金(報道で「使った量に応じた課金」とだけ)。
- Greenhouse Harvest v1/v2 が予定どおり 2026-08-31 に止まったか。

開けなかったページ:

- https://gusto.com/product/agents (403)
- https://api.jobcan.ne.jp/ (404)
- https://unified.to/integrations/smarthr (404)
- https://www.apideck.com/accounting-software/smarthr (404)
- https://developer.cultureamp.com/ (サインインの画面)
- https://developer.rippling.com/documentation (本文はログインが要る)
- https://developers.adp.com/getting-started (題名しか取れなかった)

### 求人媒体、メール、予定、チャット、文書、IT の承認

- Indeed の応募の通知メールの仕様、CSV の項目の一覧。
- Indeed の Retrieve Candidates API が日本の企業で使えるか。
- Airワーク 採用管理の外部連携の仕様書(連携の API の形)。ヘルプは 403 で開けなかった。
- engage、バイトル、タウンワーク、マイナビバイト、求人ボックスの、企業が使える公開 API と MCP。
- バイトルとタウンワークの掲載企業向けの利用規約の自動化の条項。
- HERP や HRMOS などの ATS が、媒体の応募をどの方式(通知メール、CSV、ログイン)で取り込むか。HRMOS の資料の PDF は画像で読めなかった。
- Google Calendar の scope の sensitive と restricted の分類。
- Microsoft Teams の protected API と metered API の公式の説明(404、別のページに飛んだ)。
- Chatwork の API トークンの発行に管理者の承認が要るか(ヘルプは 403)。
- LINE WORKS の公式の MCP サーバー。
- Box のリモート MCP の段階(ベータか一般提供か)。
- UiPath と Power Automate Desktop 単体の条件。Jamf の手順。
- 民間企業が SaaS の導入で ISMS や SOC 2 をどのくらい求めるかの数字。
- 経済産業省の SCS 評価制度の本文(403)。

### 開けなかったページ

- 403: https://faq.rct.airwork.net/hc/ja/articles/42558116110617 、https://faq.rct.airwork.net/hc/ja/articles/35513808519833 、https://support.en-gage.net/hc/ja/articles/900007350383 、https://help.chatwork.com/hc/ja/articles/115000172402 、https://www.meti.go.jp/policy/netsecurity/scs.html 、https://www.meti.go.jp/press/2025/03/20260327001/20260327001.html 、https://www.meti.go.jp/press/2025/03/20260327001/20260327001-a.pdf
- 404: https://docs.indeed.com/retrieve-candidates-api/retrieve-candidates-api-integration-guide 、https://learn.microsoft.com/en-us/graph/teams-protected-apis 、https://atsguide.hrmos.co/hc/article_attachments/30999222537625
- 429: https://slack.com/help/articles/222386767-Manage-app-approval-for-your-workspace
- 本文が取れなかった(JavaScript の描画): https://chromeenterprise.google/policies/#ExtensionInstallAllowlist 、https://www.ismap.go.jp/csm
- 別のページに飛んだ: https://learn.microsoft.com/en-us/graph/teams-licenses(Graph の目次に飛んだ)
