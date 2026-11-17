# 主な ATS の AI、エージェント、外部 API、権限の形

## 結論

- 海外の主な ATS は、2026 年に MCP サーバーを出し始めた。Workable、Greenhouse(公開ベータ)、Ashby(公開ベータ)で確かめた。Workday は人事全体の MCP を一般提供にした。
- ATS 自身が採用のエージェントを作っている。Workday の Talent Acquisition Agent は早期導入の段階で、Workable Agent と HERP AI Recruiter は提供中。
- 外部 API の権限は 2 つの形に分かれる。管理者が発行するキー(リソース単位のスコープ)と、人に紐づく OAuth(その人の権限を引き継ぐ)だ。
- 求人ごとや項目ごとに API の範囲を絞れる例は少ない。Ashby と Lever の「機密の求人」の切り替え、Ashby の非公開項目の切り替え程度だった。
- 国内で公開 API とスコープの文書を確かめられたのは HERP Hire だけだった。HRMOS採用、sonar ATS、ジョブカン採用管理では、公開 API の文書が見つからなかった。

## 比べる表

| 名前 | 国 | AI とエージェント | 提供の段階 | 外部 API と認証 | スコープの細かさ | MCP | 出典 | 見た日 |
|---|---|---|---|---|---|---|---|---|
| Greenhouse | 海外 | Voice AI、Notetaker、Job Kickoff Agent など | Notetaker は提供中。エージェントは 2026 年第 3 四半期の予定と書かれていた | Harvest v3(OAuth 2.0)、Ingestion API(OAuth/Basic) | v1/v2 のキーはエンドポイント単位。v3 は認可した人の権限 | 公開ベータ(Core、Plus、Pro) | https://www.greenhouse.com/greenhouse-latest-features | 2026-11-11 |
| Lever | 海外 | Fit Score、候補者の順位づけ、自動化 | 不明 | API キー(Basic)、OAuth 2.0(パートナー) | `opportunities:read:admin` などリソース × 読み書き。機密データは別の許可 | 見つからなかった | https://hire.lever.co/developer/documentation | 2026-11-11 |
| Ashby | 海外 | AI による応募の確認、Ashby Assistant、自然言語で作る Custom Agents | 不明 | API キー(Basic)。OAuth の記載なし | 13 のモジュールごとに読み書き。機密の求人と非公開項目は既定で見えない | あり(公開ベータ、2026-06-29、全プラン) | https://developers.ashbyhq.com/docs/authentication 、https://www.ashbyhq.com/product-updates/mcp | 2026-11-11 |
| Workday Recruiting | 海外 | Talent Acquisition Agent(HiredScore、Paradox と連動) | 早期導入。一般提供は 2027 年初めの予定 | 公開文書は開けなかった | 会社の権限、承認の規則を引き継ぐ(会社の発表) | Agent-Ready Tools(MCP)は一般提供 | https://newsroom.workday.com/2026-10-13-Workday-Launches-Autopilot-Agents-That-Get-Real-Work-Done-Across-HR,-Finance,-and-IT | 2026-11-11 |
| SmartRecruiters(SAP) | 海外 | Winston、AI-Powered Hiring Agent、対話の AI | 不明 | API キー、パートナー API キー、OAuth 2.0(client credentials、パートナー) | 約 60 のスコープ。オファーや監査イベントも別 | 見つからなかった | https://developers.smartrecruiters.com/docs/access-scopes | 2026-11-11 |
| SAP SuccessFactors Recruiting | 海外 | Joule の recruiting assistant | 2026-10 に「多くが今月提供」(会社の発表) | 開けなかった | 開けなかった | 見つからなかった | https://news.sap.com/2026/10/sap-accelerates-autonomous-hcm/ | 2026-11-11 |
| iCIMS | 海外 | iCIMS AI、エージェント型 AI(ソーシング、マッチング、調整) | 不明 | API 文書は利用申請が要る | 開けなかった | 見つからなかった | https://www.icims.com/ | 2026-11-11 |
| Workable | 海外 | Workable Agent(ソーシング、選考、連絡) | 「Just released」 | API トークン(管理者のみ発行) | `r_candidates`、`w_candidates`、`r_employees` などリソース × 読み書き | あり(OAuth 2.0、段階の記載なし) | https://workable.readme.io/reference/workable-mcp-server | 2026-11-11 |
| Teamtailor | 海外 | Teamtailor AI(候補者の提案、評価、要約) | 不明 | API 文書は本文を読めなかった | 開けなかった | 見つからなかった | https://www.teamtailor.com/en/ai-recruiting-software/ | 2026-11-11 |
| HERP Hire | 国内 | HERP AI Recruiter、HERP AI面接 | AI Recruiter は正式提供。AI面接はベータ | HERP Hire API(Bearer の API キー、管理者のみ発行) | `candidacy:read` などリソース × 読み書き。求人ごとの制限は記載なし | ATS は見つからなかった。求職者向けの HERP Career は MCP あり | https://public-api.herp.cloud/hire/public/doc | 2026-11-11 |
| HRMOS採用 | 国内 | 書類判定アシスト、自動求人生成 | 提供中の範囲は不明(「続々搭載予定」) | 公開 API は見つからなかった | 画面は部門、グループで権限。4 つの役割 | 見つからなかった | https://hrmos.co/ats/about/ | 2026-11-11 |
| sonar ATS | 国内 | AI求人作成アシスタント、「採用AI」オプション | 不明 | 「API連携」の見出しはあるが、仕様は見つからなかった | 見つからなかった | 見つからなかった | https://sonar-ats.jp/function | 2026-11-11 |
| ジョブカン採用管理 | 国内 | AI面接 | 近日リリース予定 | 見つからなかった | 見つからなかった | 見つからなかった | https://ats.jobcan.ne.jp/ | 2026-11-11 |

## 海外の ATS

### Greenhouse

- 対象: 企業向け。求職者向けに「Dream Job」の入口もある（出典: https://www.greenhouse.com/、見た日 2026-11-11）。
- AI とエージェントでしていること:
  - Voice AI は、候補者と 1 回目の音声の面接をする。Notetaker は面接のメモを評価表の質問にひもづける（出典: https://www.greenhouse.com/ai-recruiting、見た日 2026-11-11）。
  - ほかに、過去の応募者の掘り起こし、レポートの自然言語での作成、オファーの受諾の予測がある（出典: https://www.greenhouse.com/ai-recruiting、見た日 2026-11-11）。
  - 同じページは「the decision is always yours」と書く。判断は人に残す方針だ（出典: https://www.greenhouse.com/ai-recruiting、見た日 2026-11-11）。
- 提供の段階:
  - Job Kickoff Agent と Candidate Insights Assistant は「2026 年第 3 四半期に提供の予定」と書かれていた（出典: https://www.greenhouse.com/greenhouse-latest-features、見た日 2026-11-11）。
  - その予定の時期は過ぎている。今の段階は確かめられなかった。
  - Chart Agent(Analytics Chart Builder)は公開ベータ。Notetaker は Core、Plus、Pro で提供中（出典: https://www.greenhouse.com/greenhouse-latest-features、見た日 2026-11-11）。
- 外部 API と権限:
  - Harvest v1/v2 のページには「2026-08-31 に削除する」とある。移行先は Harvest v3（出典: https://docs.greenhouse.io/harvest.html、見た日 2026-11-11）。
  - v1/v2 は API キーの Basic 認証。キーごとに使えるエンドポイントを選べる（出典: https://docs.greenhouse.io/harvest.html、見た日 2026-11-11）。
  - ただし v1/v2 のキーは「エンドポイントの全データ」を読める。求人ごとの絞り込みはない（出典: https://docs.greenhouse.io/harvest.html、見た日 2026-11-11）。
  - v1/v2 の書き込みでは On-Behalf-Of ヘッダーで実行者の利用者 ID を送る。文書は「監査のため」と書く（出典: https://docs.greenhouse.io/harvest.html、見た日 2026-11-11）。
  - v3 は OAuth 2.0。自社の連携は client credentials、パートナーは authorization code を使う（出典: https://harvestdocs.greenhouse.io/docs/authentication、見た日 2026-11-11）。
  - v3 では、MCP と動的登録のクライアントは PKCE つきの authorization code を使う（出典: https://harvestdocs.greenhouse.io/docs/authentication、見た日 2026-11-11）。
  - v3 のトークンは `sub` に利用者 ID を入れられる。権限はその利用者のものになる。一覧のエンドポイントは Site Admin の認可が要る（出典: https://harvestdocs.greenhouse.io/docs/authentication、見た日 2026-11-11）。
  - スコープの一覧は公開ページで見つからなかった。
  - v3 には、求人ごとの権限(Job Admin)を読み書きする API がある。部署や拠点で将来の求人の権限も付けられる（出典: https://harvestdocs.greenhouse.io/llms.txt、見た日 2026-11-11）。
  - Ingestion API は、ソーシングのパートナーが候補者を送るための API。OAuth のスコープは `candidates.create`、`candidates.view`、`jobs.view` の 3 つ（出典: https://docs.greenhouse.io/candidate-ingestion.html、見た日 2026-11-11）。
- MCP: Greenhouse MCP は公開ベータで、Core、Plus、Pro で使える。ページは 2026-07 の日付（出典: https://www.greenhouse.com/product-features/greenhouse-mcp、見た日 2026-11-11）。
  - 別のページは「Site Admin が使える」と書く（出典: https://www.greenhouse.com/greenhouse-latest-features、見た日 2026-11-11）。
  - ツールの一覧、読み書きの範囲、認証は製品ページに書かれていなかった。
- 外部のエージェントを入れる仕組み: 連携の一覧(integrations.greenhouse.com)とパートナーの窓口がある（出典: https://www.greenhouse.com/、見た日 2026-11-11）。

### Lever

- 対象: 企業向け。運営は Employ Inc.（出典: https://www.lever.co/、見た日 2026-11-11）。
- AI とエージェントでしていること: Fit Score つきの推薦、候補者の順位づけ、連絡や日程調整の自動化（出典: https://www.lever.co/、見た日 2026-11-11）。
- 提供の段階: 不明。エージェントや MCP の記載は見つからなかった。
- 外部 API と権限:
  - API キーは Basic 認証。文書は「キーには多くの権限がある」と注意している（出典: https://hire.lever.co/developer/documentation、見た日 2026-11-11）。
  - OAuth 2.0 はパートナー向け。スコープは `opportunities:read:admin` のようにリソースと読み書きの組み合わせ（出典: https://hire.lever.co/developer/documentation、見た日 2026-11-11）。
  - 機密の求人や候補者を読む権限は、キーを作るときにしか付けられない（出典: https://hire.lever.co/developer/documentation、見た日 2026-11-11）。
  - 書き込みの多くは `perform_as` で実行者を指定できる（出典: https://hire.lever.co/developer/documentation、見た日 2026-11-11）。
  - 上限はキーごとに毎秒 10 回、瞬間で 20 回（出典: https://hire.lever.co/developer/documentation、見た日 2026-11-11）。

### Ashby

- 対象: 企業向け。
- AI とエージェントでしていること:
  - 求人の基準を決めて応募を AI が確認する。面接の評価の要約もする（出典: https://www.ashbyhq.com/ai、見た日 2026-11-11）。
  - Ashby Assistant は「採用データの全体を知り、代わりに動く AI エージェント」と書かれている（出典: https://www.ashbyhq.com/ai、見た日 2026-11-11）。
  - Custom Agents は、決まった流れのエージェントを自然言語で作る機能（出典: https://www.ashbyhq.com/ai、見た日 2026-11-11）。
- 提供の段階: 各機能の段階はページに書かれていなかった。日程の自動調整だけは追加オプション(Add-on)と書かれていた（出典: https://www.ashbyhq.com/ai、見た日 2026-11-11）。
- 外部 API と権限:
  - API キーの Basic 認証。OAuth の記載はない（出典: https://developers.ashbyhq.com/docs/authentication、見た日 2026-11-11）。
  - キーごとに、13 のモジュール(求人、候補者、オファー、面接、監査ログなど)の読み書きを選べる（出典: https://developers.ashbyhq.com/docs/authentication、見た日 2026-11-11）。
  - 機密の求人は既定で見えない。管理者が別に許可する（出典: https://developers.ashbyhq.com/docs/authentication、見た日 2026-11-11）。
  - 候補者の非公開項目も既定で見えない(オファーは除く)（出典: https://developers.ashbyhq.com/docs/authentication、見た日 2026-11-11）。
  - `X-On-Behalf-Of` で、操作を特定の利用者のものにできる。これにもキーの許可が要る（出典: https://developers.ashbyhq.com/docs/authentication、見た日 2026-11-11）。
  - 監査ログの API(`auditLog.list`)はクローズドベータ（出典: https://developers.ashbyhq.com/llms.txt、見た日 2026-11-11）。
- MCP: Ashby MCP サーバーで Claude や ChatGPT から Ashby のデータを扱える（出典: https://www.ashbyhq.com/ai、見た日 2026-11-11）。
- Ashby MCP サーバーは 2026-06-29 に、全プランで公開ベータ(Open Beta)になった（出典: https://www.ashbyhq.com/product-updates/mcp、見た日 2026-11-11）。
- 利用者ごとに OAuth でつなぐ。返すのは、その利用者が Ashby で見られるデータだけ。入出力は予告なく変わりうる（出典: https://docs.ashbyhq.com/ashby-mcp-server-beta、見た日 2026-11-11）。
- 外部のエージェントを入れる仕組み: パートナーは紹介の面談、法務の確認、サンドボックス、デモを経て Marketplace に載る（出典: https://www.ashbyhq.com/integrations、見た日 2026-11-11）。

### Workday Recruiting(Paradox を含む)

- 対象: 企業向け(大企業が中心)。求職者向けに Candidate Profile も出す。
- AI とエージェントでしていること:
  - Talent Acquisition Agent は、期日に遅れそうな求人を知らせ、候補者を探して要約し、連絡の下書きと面接の調整をする（出典: https://newsroom.workday.com/2026-10-13-Workday-Launches-Autopilot-Agents-That-Get-Real-Work-Done-Across-HR,-Finance,-and-IT、見た日 2026-11-11）。
  - このエージェントは Workday Recruiting、HiredScore、Paradox と連動する（出典: https://newsroom.workday.com/2026-10-13-Workday-Launches-Autopilot-Agents-That-Get-Real-Work-Done-Across-HR,-Finance,-and-IT、見た日 2026-11-11）。
  - Paradox(Olivia)は、チャットや SMS での選考、日程調整、オファーの作成をする。「採用の 90% を自動化」としている(会社の発表)（出典: https://www.paradox.ai/、見た日 2026-11-11）。
  - Candidate Profile では、求職者が情報を一度保存して使い回す。「各企業に何を見せるかは求職者が決める」と書く（出典: https://newsroom.workday.com/2026-10-13-New-Workday-Candidate-Profile-Lets-Job-Seekers-Save-Their-Information-Once-and-Use-It-Every-Time-They-Apply-Through-Workday、見た日 2026-11-11）。
- 提供の段階:
  - Talent Acquisition Agent の autopilot は早期導入の企業に提供中。一般提供は 2027 年初めの予定（出典: https://newsroom.workday.com/2026-10-13-Workday-Launches-Autopilot-Agents-That-Get-Real-Work-Done-Across-HR,-Finance,-and-IT、見た日 2026-11-11）。
  - Candidate Profile は 2027 年初めに一般提供の予定（出典: https://newsroom.workday.com/2026-10-13-New-Workday-Candidate-Profile-Lets-Job-Seekers-Save-Their-Information-Once-and-Use-It-Every-Time-They-Apply-Through-Workday、見た日 2026-11-11）。
  - Paradox の買収の完了は、一次情報を開けず確かめられなかった。paradox.ai のトップには「Paradox for Workday」という連携の記載だけがあった（出典: https://www.paradox.ai/、見た日 2026-11-11）。
- 権限とデータの扱い:
  - エージェントは各社の方針、権限、承認の規則を引き継ぐ。候補者への連絡は採用担当の承認が要る。すべての操作を記録する(会社の発表)（出典: https://newsroom.workday.com/2026-10-13-Workday-Launches-Autopilot-Agents-That-Get-Real-Work-Done-Across-HR,-Finance,-and-IT、見た日 2026-11-11）。
  - Agent-Ready Tools は Workday の MCP ツール。Workday Extend AI で一般提供（出典: https://en-sg.newsroom.workday.com/2026-10-13-Workdays-Trusted-Agent-Platform-Now-Delivers-Headless-Access-to-HR-and-Finance,-Letting-Customers-Build-and-Run-Lawful-AI-Agents、見た日 2026-11-11）。
  - Recruiting の API の文書は開けなかった。

### SmartRecruiters と SAP SuccessFactors Recruiting

- 対象: 企業向け。
- 買収: SAP は 2025-08-01 に SmartRecruiters の買収を発表した。完了は 2025 年第 4 四半期の見込みで、単独の製品としても残すとした（出典: https://news.sap.com/2025/08/sap-to-acquire-smartrecruiters/、見た日 2026-11-11）。
  - 今の SmartRecruiters のサイトは「SmartRecruiters, part of SAP SuccessFactors」と書く（出典: https://www.smartrecruiters.com/、見た日 2026-11-11）。完了の日付の発表は見つからなかった。
- AI とエージェントでしていること:
  - SmartRecruiters は Winston という AI の層、AI-Powered Hiring Agent、対話の AI チャット、AI のマッチングを掲げる（出典: https://www.smartrecruiters.com/、見た日 2026-11-11）。Hiring Agent のページは 403 で開けなかった。
  - SAP は 2026-10 に、Joule の recruiting assistant を含む複数の assistant が「今月提供」と書いた(会社の発表)（出典: https://news.sap.com/2026/10/sap-accelerates-autonomous-hcm/、見た日 2026-11-11）。中身は書かれていなかった。
- 外部 API と権限:
  - 認証は API キー、パートナー API キー、OAuth 2.0 の client credentials、パートナー向けの OAuth の 4 つ（出典: https://developers.smartrecruiters.com/、見た日 2026-11-11）。
  - スコープは細かい。候補者の読み取りとオファーの読み取りが別で、`audit_events_read` もある（出典: https://developers.smartrecruiters.com/docs/access-scopes、見た日 2026-11-11）。
  - API キーが利用者の権限を引き継ぐかは書かれていなかった。
- MCP: 見つからなかった。
- 外部のエージェントを入れる仕組み: Marketplace とパートナーのネットワークがある（出典: https://www.smartrecruiters.com/、見た日 2026-11-11）。

### iCIMS

- 対象: 企業向け(大企業が中心)。
- AI とエージェントでしていること: iCIMS AI を掲げる。FAQ は「エージェント型 AI がソーシング、マッチング、連絡、調整を支える」と書く（出典: https://www.icims.com/、見た日 2026-11-11）。
- 提供の段階: 書かれていなかった。
- 外部 API と権限:
  - API の文書は開発者コミュニティにあり、利用申請が要る（出典: https://developer-community.icims.com/、見た日 2026-11-11）。
  - パートナーでなくても、顧客は連携を作れる。Marketplace に載せるには検証が要る（出典: https://developer-community.icims.com/getting-started/integrating-icims、見た日 2026-11-11）。
  - 800 以上のパートナーの技術とつながるとしている(会社の発表)（出典: https://www.icims.com/、見た日 2026-11-11）。
  - 認証の方式とスコープは、ログインの外では読めなかった。
- MCP: 見つからなかった。

### Workable

- 対象: 企業向け(中小が中心)。ATS に加え、従業員と休暇の機能も持つ。
- AI とエージェントでしていること:
  - Workable Agent は、ソーシング、選考、候補者への連絡を ATS の中で行う。トップでは「Just released」と書く（出典: https://www.workable.com/、見た日 2026-11-11）。
  - 候補者を最大 14 の基準で採点し、理由を示す。人が候補者とやり取りを始めると止まる（出典: https://www.workable.com/workable-ai、見た日 2026-11-11）。
  - 設定は会社、求人、候補者ごとに変えられる。管理者は全体を止められる。すべての操作を記録する(会社の発表)（出典: https://www.workable.com/workable-ai、見た日 2026-11-11）。
- 外部 API と権限:
  - API トークンは管理者だけが発行できる。期限は 30 日から 2 年（出典: https://help.workable.com/hc/en-us/articles/115015785428-Generating-an-API-access-token、見た日 2026-11-11）。
  - スコープは `r_candidates`、`w_candidates`、`r_employees` などリソースと読み書きの組み合わせ。`r_employees` は「機微な従業員の情報」と注意書きがある（出典: https://help.workable.com/hc/en-us/articles/115015785428-Generating-an-API-access-token、見た日 2026-11-11）。
- MCP:
  - エンドポイントは `https://mcp.workable.com/mcp`。認証は OAuth 2.0 で、動的なクライアント登録に対応する（出典: https://workable.readme.io/reference/workable-mcp-server、見た日 2026-11-11）。
  - ツールは「認証した利用者に許された範囲」で動く（出典: https://workable.readme.io/reference/workable-mcp-server、見た日 2026-11-11）。
  - 書き込みのツールもある。候補者の移動、不採用、オファーの承認、評価の署名などだ（出典: https://workable.readme.io/reference/workable-mcp-server、見た日 2026-11-11）。
  - 署名などは「最終で戻せない。先に利用者に確かめる」とツールの説明にある（出典: https://workable.readme.io/reference/workable-mcp-server、見た日 2026-11-11）。
  - 段階の記載はなかった。ページの更新日は 2026-07-16。

### Teamtailor

- 対象: 企業向け。
- AI とエージェントでしていること: 人材プールからの候補者の提案、基準に沿った評価、面接の要約、求人の原稿（出典: https://www.teamtailor.com/en/ai-recruiting-software/、見た日 2026-11-11）。
- 提供の段階: 書かれていなかった。
- 権限とデータの扱い: ISO 42001(AI の管理)を取ったと書く（出典: https://www.teamtailor.com/en/、見た日 2026-11-11）。API の文書(docs.teamtailor.com)は本文を読めなかった。
- MCP: 見つからなかった。

## 国内の ATS

### HERP Hire(HERP)

- 対象: 企業向け(HERP Hire、HERP AI Recruiter)。求職者向けに HERP Career もある。
- AI とエージェントでしていること:
  - HERP AI Recruiter は、応募書類の一次確認、面接の書き起こしと要約、評価やメールの案の作成をする（出典: https://prtimes.jp/main/html/rd/p/000000126.000030340.html、見た日 2026-11-11）。
  - 過去の選考データから、採用要件の見直しや候補者の推薦もする（出典: https://prtimes.jp/main/html/rd/p/000000126.000030340.html、見た日 2026-11-11）。
  - HERP AI面接は、1 回目の面接を AI が行う。なりすましを検知すると面接を止める（出典: https://prtimes.jp/main/html/rd/p/000000136.000030340.html、見た日 2026-11-11）。
- 提供の段階:
  - HERP AI Recruiter は 2026-06-23 に正式提供。ベータは 2025-10 から。導入は 200 社超(会社の発表)（出典: https://prtimes.jp/main/html/rd/p/000000126.000030340.html、見た日 2026-11-11）。
  - HERP AI面接は 2026-10-27 にベータの提供を始めた（出典: https://prtimes.jp/main/html/rd/p/000000136.000030340.html、見た日 2026-11-11）。
  - 一覧では、2026-04-22 に「HERP Agent Network」(人材紹介会社へ求人を出す仕組み)の発表もあった（出典: https://prtimes.jp/main/action.php?run=html&page=searchkey&search_word=HERP%20Hire、見た日 2026-11-11）。本文は読んでいない。
- 外部 API と権限:
  - HERP Hire API は 2026-02-03 に正式提供。ベータは 2025-10-22 から。有料の契約者が使える（出典: https://prtimes.jp/main/html/rd/p/000000113.000030340.html、見た日 2026-11-11）。
  - 読めるのは応募、応募のファイル、職種。書けるのは応募の作成、選考の登録、評価の記入（出典: https://prtimes.jp/main/html/rd/p/000000113.000030340.html、見た日 2026-11-11）。
  - API キーは管理者だけが発行できる。発行時に名前、期限、スコープを決める（出典: https://help.herp.cloud/ja/articles/HERP-Hire-API-86ba917e、見た日 2026-11-11）。
  - 認証は Bearer の API キー。スコープは `candidacy:read`、`requisition:write` のようにリソースと読み書きの組み合わせ（出典: https://public-api.herp.cloud/hire/public/doc、見た日 2026-11-11）。
  - 職種ごとに範囲を絞る仕組みと、監査ログの記載は見つからなかった。上限はテナントごとに毎分 100 回（出典: https://public-api.herp.cloud/hire/public/doc、見た日 2026-11-11）。
  - 入力したデータは AI 提供会社の学習に使わないとしている（出典: https://prtimes.jp/main/html/rd/p/000000126.000030340.html、見た日 2026-11-11）。
- MCP:
  - ATS(HERP Hire)の MCP は見つからなかった。
  - 求職者向けの HERP Career は、2026-08-20 に MCP で Claude とつないだ。会話で求人を探し、希望をプロフィールに保存する（出典: https://prtimes.jp/main/html/rd/p/000000131.000030340.html、見た日 2026-11-11）。
  - 接続は Claude デスクトップ用のファイル(.mcpb)と API キーで行う。OAuth の記載はない（出典: https://herp.careers/careers/mcp-guide、見た日 2026-11-11）。

### HRMOS採用(ビズリーチ)

- 対象: 企業向け。
- AI とエージェントでしていること: 書類判定アシスト(応募書類と求人の要件の適合を判定)と、自動求人生成（出典: https://hrmos.co/ats/about/、見た日 2026-11-11）。
- 提供の段階: 製品ページは「AI機能を続々搭載予定」と書く。どこまで提供済みかは分からなかった（出典: https://hrmos.co/ats/、見た日 2026-11-11）。
- 権限とデータの扱い:
  - 役割は「管理者」「採用担当者」「採用コーディネーター」「面接官」の 4 つ。IP の制限もある（出典: https://hrmos.co/ats/faq/、見た日 2026-11-11）。
  - 部門や新卒、中途などのグループで権限を分けられる（出典: https://hrmos.co/ats/about/、見た日 2026-11-11）。
  - 連携は、媒体からの応募の取り込み、カレンダー、Slack、SmartHR など（出典: https://hrmos.co/ats/about/、見た日 2026-11-11）。
  - 公開 API の文書は見つからなかった。パートナーのページは販売の紹介の制度だった（出典: https://hrmos.co/partner/ats/、見た日 2026-11-11）。
- MCP: 見つからなかった。

### sonar ATS(Thinkings)

- 対象: 企業向け(新卒と中途)。
- AI とエージェントでしていること: AI求人作成アシスタントが、チャットで要件を整理して求人の原稿を作る（出典: https://sonar-ats.jp/function、見た日 2026-11-11）。料金のページには「採用AI」というオプションもある（出典: https://sonar-ats.jp/、見た日 2026-11-11）。
- 提供の段階: 書かれていなかった。
- 権限とデータの扱い:
  - 面接官などに見せる応募者の項目を選べる。人材紹介会社には専用の管理画面を出せる（出典: https://sonar-ats.jp/function、見た日 2026-11-11）。
  - 「多彩なHRサービスとAPI連携」という見出しはある。公開 API の仕様は見つからなかった（出典: https://sonar-ats.jp/、見た日 2026-11-11）。
- MCP: 見つからなかった。

### ジョブカン採用管理(Donuts)

- 対象: 企業向け。
- AI とエージェントでしていること: AI面接は「近日リリース予定」で、1 回 3,000 円と書く。リファレンスチェックは 1 回 1,500 円から（出典: https://ats.jobcan.ne.jp/、見た日 2026-11-11）。
- 提供の段階: AI面接は発表のみ。
- 権限とデータの扱い: 公開 API と権限の文書は見つからなかった。
- MCP: 見つからなかった。

## このプロダクトへの示唆

### できること

- 海外の主な ATS は、外部のエージェントの入口(MCP、OAuth)を自分で用意し始めた。Workable の MCP は書き込みまでできる。bot を ATS につなぐ道は、少なくとも海外では開いている。
- 人に紐づく OAuth(Greenhouse v3 の `sub`、Workable MCP)なら、bot はその人と同じ範囲だけを見る。既存の権限をそのまま使える。
- 実行者の記録の仕組みはある。Greenhouse の On-Behalf-Of、Lever の `perform_as`、Ashby の `X-On-Behalf-Of` だ。bot の操作を「誰の代わりか」で残せる。
- HERP Hire API は国内で唯一、スコープつきの公開 API を確かめられた。国内で最初につなぐ先の候補になる。

### 足りないこと

- **スコープが粗い。** 管理者が発行するキーのスコープは、リソースと読み書きの単位だ。求人ごと、部署ごと、項目ごとには、ほぼ絞れない。Greenhouse v1/v2 は「エンドポイントの全データ」と明記している。
  - 推測: 「普段は見られないデータ」を bot に読ませるには、サービス用のキーを使うことになる。そのキーは広すぎるので、bot の側に求人や項目の単位の方針の層が要る。
- **機密の扱いが ATS ごとに違う。** Ashby と Lever は機密の求人をキーごとに切り替えられる。ほかは確かめられなかった。
- **監査ログを外から読めない。** 監査ログの API は Ashby(クローズドベータ)と SmartRecruiters(`audit_events_read`)だけで確かめた。国内では見つからなかった。Workday と Workable の「すべて記録する」は会社の発表だ。
  - 推測: bot が何を読み、何を書いたかの記録は、ATS に頼らず bot の側で持つ必要がある。
- **書き込みの危険。** Workable MCP には、評価の署名のように戻せない操作がある。Workday も連絡の前に人の承認を求める。bot の書き込みには、操作ごとの承認の段階が要る。
- **国内の API の空白。** HRMOS採用、sonar ATS、ジョブカン採用管理では公開 API が見つからなかった。
  - 推測: 国内の中小企業の多くは、bot から API で触れない ATS を使っている。CSV や画面の操作を代わりにする仕組みか、ATS 自体を置き換える選択が要る。

### 競合の見え方

- ATS 自身がエージェントを作っている(Workday、Workable、Ashby、HERP)。「ATS の中の AI」は差別化にならない。
  - 推測: 差別化の候補は、複数の ATS と人事のデータをまたぐ bot、Ashby の Custom Agents に近い「自然言語での流程の設計」、求職者の bot との A2A だ。
- 求職者の側でも、データを求職者が持つ動きが出ている。Workday Candidate Profile は「何を見せるかは求職者が決める」と書く。HERP Career は MCP で Claude とつないだ。
  - 推測: 求職者向けの bot は、こうした求職者のプロフィールに許可つきでつなぐ形がとりやすい。

## 見つからなかったこと

- **検索の上限:** この調べの途中で WebSearch の上限に達した。以降は、知っている URL を WebFetch で直接開いて調べた。そのため候補の一部は調べていない。
- **調べていない、または開けなかった ATS:**
  - talentio: www.talentio.co.jp は 403、talentio.com はログイン画面だった。
  - 採用一括かんりくん、Airワーク 採用管理、Oracle Recruiting: 調べていない。
  - Teamtailor の API 文書: 本文を読めなかった。
  - iCIMS の API 文書: 利用申請が要るため読んでいない。
  - Workday Recruiting の API 文書: 開けなかった。
- **確かめられなかった事実:**
  - Workday による Paradox の買収の完了日(一次情報を開けなかった)。
  - SAP による SmartRecruiters の買収の完了日。
  - Greenhouse の Job Kickoff Agent と Candidate Insights Assistant の今の段階(予定の 2026 年第 3 四半期は過ぎている)。
  - Greenhouse Harvest v1/v2 が 2026-08-31 に実際に止まったか。
  - Greenhouse v3 と Greenhouse MCP のスコープの一覧、MCP のツールの一覧。
  - Workable MCP の提供の段階。
  - Lever、SmartRecruiters、iCIMS、Teamtailor の MCP。
  - HRMOS採用、sonar ATS、ジョブカン採用管理の公開 API。
  - 国内の ATS で、API の操作を監査ログで追えるか。
