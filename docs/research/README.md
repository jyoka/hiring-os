# 調べもの: AI ネイティブな採用の仕組み(2026-11 時点)

この節は `docs/prd.md` の根拠になる調べものの入口だ。各主張の出典 URL と見た日は、各ファイルの本文にある。この README の表と結論は、各ファイルの記載をまとめたもので、本文より強く言い切らない。

## 結論(Goal の問いへの答え)

問い: 既存の ATS、採用の SaaS、求人の大手は、本当にまだ AI ネイティブでないのか。どこに機会があるのか。

答え: 「AI がない」は誤りだった。「自社の囲いの中だけで AI ネイティブになろうとしている」が、確かめた事実に近い。囲いの外の 4 つは、確かめた範囲では誰も出していない。ここが機会だ。

この結論は、主に米国の Indeed と LinkedIn の事実による。国内の大手(リクナビ、タウンワーク、Airワーク)の AI 機能は、一次情報に届いていない(job-platforms.md「見つからなかったこと」)。

### 確かめた事実

- 大手は企業向けのエージェントをすでに一般提供している。Indeed の Sourcing Assistant(米国)、LinkedIn の Hiring Assistant、Paradox の会話型 ATS(現場職)がその例だ。Indeed の応募の 70% は、AI の提案や、AI のデータにもとづくメールとポップアップなどから来ている(会社の発表)。[job-platforms.md「Indeed」](job-platforms.md)、[ai-hiring-tools.md「企業向け(海外)」](ai-hiring-tools.md)
- 大手のエージェントは、自社の求人と自社の候補者の中で動く。Indeed の CEO は、内定、条件交渉、入社手続きの自動化を「多くの顧客のシステムと連携すると遅くなる」として後回しにした。[job-platforms.md「経営の方針」](job-platforms.md)
- 求職者の側で「代わりに動く」機能は試験か下書きどまりだ。Indeed の Apply For Me は米国の限定試験で、確認なしの自動応募は 2026-08-04 に止めた。LinkedIn と Indeed の利用規約は、外部の bot による自動化を禁じている。[job-platforms.md「求職者向け」](job-platforms.md)
- 求職者の側の外部の AI への窓口は「求人の検索」だけ開いた。Indeed と ZipRecruiter は ChatGPT アプリを出し、Indeed は MCP をベータで出した。応募は自社のサイトに戻す。[job-platforms.md「横断の論点」](job-platforms.md)
- 企業の側は、自社の求人に限ったエージェントを汎用アシスタントの中に出し始めた。LinkedIn の Hiring Pro(中小企業向け)は、2026-10-21 から Claude の中で求人の原稿を作り、人の承認の後に掲載する。[general-assistants.md「Claude」](general-assistants.md)、[job-platforms.md「LinkedIn」](job-platforms.md)
- ATS と人事のサービスは 2026 年に MCP を出し始めた(Greenhouse、Ashby、Workable、Wantedly Hire、Workday、freee、BambooHR、HiBob)。多くは「サインインした人の権限を引き継ぐ」形で、スコープはリソースと読み書きの単位と粗い。[ats.md「結論」](ats.md)、[hr-data.md「結論」](hr-data.md)
- 汎用アシスタントの権限の単位は、アプリ、ツール、サイトのどれかだった。データの中身の種類で見せる範囲を決める設定は、調べた 9 件のどれにもなかった。[general-assistants.md「求職に関係するデータだけを見せ、ほかは遮断するはできるか」](general-assistants.md)
- エージェントどうしの約束は A2A(v1.0.1)に集まりつつある。ただし採用の語彙(求人、応募、同意、選考の結果)は、A2A にも MCP にも RFC 9396 にもない。[a2a-and-permissions.md「結論」](a2a-and-permissions.md)

### 見つからなかった 4 つ(= 機会の候補)

| 機会 | 確かめた範囲の状態 | 根拠 |
|---|---|---|
| 1. 企業の中の複数のシステム(ATS、人事、勤怠)をまたぎ、目的ごとに絞った権限で管理を代わりにやる bot | ATS ごと、人事のサービスごとのエージェントはある。またぐものは見つからなかった。監査ログを外から読める例も少ない | ats.md「足りないこと」、hr-data.md「足りないこと」 |
| 2. 企業が自社の採用流程そのものを自然言語で設計する仕組み | 見つからなかった。Ashby の Custom Agents(決まった流れのエージェントを自然言語で作る)と、Metaview の管理者の設定が近い | ai-hiring-tools.md「点の自動化か、流程全体か」、ats.md「Ashby」 |
| 3. 求職に関係するデータだけを見て、それ以外を遮断する求職者のアシスタント | 見つからなかった。既存の自動応募の拡張は、認証情報や私的な通信まで扱うと自己申告している。近いものは 2 つある。Workday Candidate Profile は「各企業に何を見せるかは求職者が決める」と書く(発表のみ、Workday 経由の応募に限る)。HERP Career は MCP で Claude とつなぐ。どちらの記載にも、外部のソース(メール、予定)を取り込んで求職の分だけに絞る仕組みはなかった | ai-hiring-tools.md「求職者向けの差別化」、general-assistants.md 同上、ats.md「競合の見え方」 |
| 4. 企業の bot と求職者の bot が直接やり取りする A2A | 製品も、採用向けの標準も見つからなかった。Indeed の利用規約は「応募を企業かその Agentic AI に送る」と書き、企業側のエージェントは想定し始めている | job-platforms.md「Indeed」、a2a-and-permissions.md「見つからなかったこと」 |

### 機会を狭める条件

- 日本の職業安定法: 厚生労働省は「AI による自動処理でも、事業者の判断で選別、加工、連絡の差配をすれば職業紹介(許可が必要)」と書いている。bot の作り方しだいで、許可の要否が変わる。[regulation.md「1.2」](regulation.md)
- 求職者からの課金の制約: 特定募集情報等提供事業者と有料職業紹介事業者は、原則として求職者から報酬を取れない。[regulation.md「1.1」](regulation.md)
- EU の AI 法: 採用の AI は附属書 III の高リスク。義務の適用は 2027-12-02 に延びた。[regulation.md「2.1」「2.2」](regulation.md)
- 米国の訴訟: Mobley v. Workday は、ベンダーが雇用主の代理人として責任を負いうる、という論点で集団訴訟が続いている。[risks.md「2. 訴訟」](risks.md)
- 大手の利用規約: 求職者の bot が大手のサイトで応募を自動化すると、規約とぶつかる。[job-platforms.md「横断の論点」](job-platforms.md)
- 国内の ATS の API の空白: 公開 API とスコープの文書を確かめられた国内の ATS は HERP Hire だけだった。[ats.md「国内の ATS」](ats.md)

### 推測

- 推測: 大手が囲いの外に出にくいのは、外部の bot に開くほど、自社の両側のデータと課金点(応募、スポンサー求人)が弱まるからだ。根拠は Indeed の CEO の発言と規約の書き方だけで、会社はそう述べていない。
- 推測: hiring-os は大手と正面から競わず、大手の API や ATS の「外側」(企業の社内データの上、求職者の手元)に座る方が、大手の方針とぶつかりにくい。

## 比べる表

行は製品とサービスだけ。見た日は各ファイルの本文と表にある(いずれも 2026-11-11)。提供の段階は「発表のみ / ベータ / 一般提供 / 不明」で書く。

### 求人の大手(詳しくは job-platforms.md)

| 名前 | 対象 | AI とエージェントでしていること | 提供の段階 | 権限とデータの扱い | 出典 |
|---|---|---|---|---|---|
| Indeed Sourcing Assistant | 企業向け | 自然言語で候補者像を受け、候補者を探して応募を誘う | 一般提供(米国) | 送る文面は採用担当が承認する | https://www.indeed.com/news/releases/indeeds-ai-powered-sourcing-assistant-helps-employers-hire-over-30-faster?co=US |
| Indeed Smart Screening(Smart Fit Score) | 企業向け | 企業の基準で応募者に 0〜100 の点と要約を付ける | 一般提供(提供範囲は不明) | 求職者が出した情報だけで採点する(会社の発表) | https://www.indeed.com/news/releases/introducing-indeeds-smart-fit-score?co=US |
| Indeed Talent Scout | 企業向け | 会話で候補者の一覧とスカウト文の下書きを出す | 不明(米国のみ) | 有料契約が要る。ATS からはパートナートークンでつなぐ | https://www.indeed.com/employers/talentscout |
| Indeed Career Scout | 求職者向け | 求人の推薦、応募の事前入力、面接練習 | 不明(2025-09 発表) | Indeed のプロフィールと会話を使う | https://www.indeed.com/news/releases/indeed-introduces-new-suite-of-hiring-products-career-scout-talent-scout-premium-sponsored-jobs-and-indeed-connect?co=US |
| Indeed Apply For Me | 求職者向け | プロフィールから応募の文面を下書きする | ベータ(米国の限定試験。自動応募は停止) | 応募数に上限。本人が確かめてから送る | https://www.indeed.com/news/releases/indeed-tests-apply-for-me-job-search?co=US |
| Indeed の ChatGPT アプリと MCP | 求職者向け | 外部の AI から求人を検索し、表示する | アプリは一般提供(日本を含む)、MCP はベータ | Indeed のアカウントでつなぐ。応募は Indeed で行う | https://docs.indeed.com/mcp |
| Indeed PLUS AI アシスタント | 企業向け(国内) | 応募の状況を分析し、求人原稿の改善を提案する | ベータ(2026-09-07 から) | 企業の承認なしに原稿を変えない | https://jp.indeed.com/news/releases/20260907 |
| リクルートエージェント AI 面接練習 | 求職者向け(国内) | 音声と映像で面接を練習する | 一般提供 | 結果は企業に渡さない(会社の説明) | https://www.r-agent.com/guide/?p=38627 |
| LinkedIn Hiring Assistant | 企業向け | ヒアリング、ソーシング、評価、事前選考、日程調整 | 一般提供(版 2 は順次) | Recruiter の追加契約。指示した作業だけをする | https://business.linkedin.com/talent-solutions/hiring-assistant |
| LinkedIn Hiring Pro(Claude から) | 企業向け(中小) | 求人原稿を作り、承認後に掲載し、候補者を絞る | 一般提供(Claude、2026-10-21 発表) | 人が直して承認してから載る | https://news.linkedin.com/2026/making-it-easier-for-small-businesses-to-hire-on-linkedin |
| LinkedIn AI 求人検索、Job Match | 求職者向け | 自然な言葉で求人を探し、合い具合を示す | 一般提供(展開中) | 外部の AI への窓口は見つからなかった。規約は bot を禁止 | https://news.linkedin.com/2026/LinkedIn-Research-Talent-2026? |
| ZipRecruiter | 両方 | ChatGPT アプリでの求人検索、選考の質問の提案、ZipIntro | 一般提供 | ATS 連携 180 以上。応募は自社のサイト | https://d18rn0p25nwr6d.cloudfront.net/CIK-0001617553/3f6efbcd-c86a-4295-a03c-b36dbbf4aa12.pdf |
| ビズリーチ AI | 両方(国内) | 求人票の自動作成、スカウト文の調整、キャリア相談 AI | 一般提供 | 個人データの扱いの記載なし | https://www.bizreach.co.jp/pressroom/pressrelease/2026/0701.html |
| エン PeopleX | 企業向け(国内) | AI 面接などを OEM で売る | 発表のみ(2026-04)。自治体の導入の発表あり | 記載なし | https://prtimes.jp/main/html/rd/p/000001186.000000725.html |
| ディップ 面接コボット、dip AI エージェント | 両方(国内) | 応募者への自動連絡と日程調整。対話で求人を提案 | コボットは一般提供。AI エージェントは 2024 年の開始のみ確認 | AI の使用の明示なし | https://www.baitoru.com/solution/?p=344 |

### ATS(詳しくは ats.md)

| 名前 | 対象 | AI とエージェントでしていること | 提供の段階 | 権限とデータの扱い | 出典 |
|---|---|---|---|---|---|
| Greenhouse | 企業向け | Notetaker、Job Kickoff Agent など。MCP | MCP は公開ベータ。エージェントは段階不明 | v3 は OAuth で認可した人の権限。重い操作は人が確認 | https://support.greenhouse.io/hc/en-us/articles/53944054829083-Greenhouse-MCP-security-FAQ |
| Lever | 企業向け | Fit Score、順位づけ | 不明 | API キー/OAuth。`opportunities:read:admin` 型のスコープ | https://hire.lever.co/developer/documentation |
| Ashby | 企業向け | Ashby Assistant、自然言語の Custom Agents、MCP | MCP は公開ベータ。ほかは不明 | 利用者ごとの OAuth。機密の求人と非公開項目は既定で見えない | https://docs.ashbyhq.com/ashby-mcp-server-beta |
| Workday Recruiting(Paradox を含む) | 企業向け | Talent Acquisition Agent。会話型 ATS で応募から入社書類まで | Agent は早期導入(一般提供は 2027 年初めの予定)。会話型 ATS は一般提供 | 権限と承認の規則を引き継ぎ、操作を記録(会社の発表) | https://newsroom.workday.com/2026-10-13-Workday-Launches-Autopilot-Agents-That-Get-Real-Work-Done-Across-HR,-Finance,-and-IT |
| Workday Candidate Profile | 求職者向け | 情報を一度保存し、Workday 経由の応募で使い回す | 発表のみ(一般提供は 2027 年初めの予定) | 各企業に何を見せるかは求職者が決める(会社の発表) | https://newsroom.workday.com/2026-10-13-New-Workday-Candidate-Profile-Lets-Job-Seekers-Save-Their-Information-Once-and-Use-It-Every-Time-They-Apply-Through-Workday |
| SmartRecruiters / SAP SuccessFactors Recruiting | 企業向け | Winston、Joule の recruiting assistant | 不明 | 約 60 の細かいスコープ(監査イベントの読み取りあり) | https://developers.smartrecruiters.com/docs/access-scopes |
| iCIMS | 企業向け | エージェント型 AI(ソーシング、調整) | 不明 | API 文書は利用申請が要る | https://www.icims.com/ |
| Workable | 企業向け | Workable Agent、MCP | 不明 | MCP は OAuth で利用者の範囲。書き込みもできる | https://workable.readme.io/reference/workable-mcp-server |
| Teamtailor | 企業向け | 候補者の提案、評価、要約 | 不明 | API 文書を読めなかった | https://www.teamtailor.com/en/ai-recruiting-software/ |
| HERP Hire / HERP Career | 企業向け(国内)/ 求職者向け(国内) | AI Recruiter、AI 面接。Career は MCP で Claude とつなぐ | AI Recruiter は一般提供、AI 面接はベータ | API キーは管理者が発行。リソース × 読み書きのスコープ | https://public-api.herp.cloud/hire/public/doc |
| HRMOS採用 | 企業向け(国内) | 書類判定アシスト、求人の自動生成 | 不明 | 役割と部門の権限。公開 API は見つからなかった | https://hrmos.co/ats/about/ |
| sonar ATS | 企業向け(国内) | AI 求人作成アシスタント | 不明 | 公開 API は見つからなかった | https://sonar-ats.jp/function |
| ジョブカン採用管理 | 企業向け(国内) | AI 面接 | 発表のみ | 公開 API は見つからなかった | https://ats.jobcan.ne.jp/ |
| Wantedly Hire MCP | 企業向け(国内) | 閲覧、検索、集計 | 一般提供(読み取りだけ) | 個人のトークン。利用者の権限に従う | https://www.tv-tokyo.co.jp/plus/external-pr/entry/225784.html |

### AI 採用ツール(詳しくは ai-hiring-tools.md)

| 名前 | 対象 | AI とエージェントでしていること | 提供の段階 | 権限とデータの扱い | 出典 |
|---|---|---|---|---|---|
| HireVue | 企業向け | 会話と職種の推薦、音声の AI 面接官 | 不明。面接官は発表のみ | ATS 連携の記載なし | https://www.hirevue.com/press-release/hirevue-acquires-hireguide-technology-to-accelerate-agentic-ai-hiring |
| Eightfold AI Interviewer | 企業向け | 構造化面接、書き起こし、要約 | 一般提供(2025-10) | 内容だけ評価し、生体情報を使わない(会社の発表) | https://eightfold.ai/company/press/press-releases/eightfold-ai-launches-ai-interviewer-to-deliver-faster-and-more-equitable-hiring/ |
| Juicebox | 企業向け | ソーシングとアウトリーチ | 一般提供 | ATS 40 以上。文面は人が承認 | https://juicebox.ai/ |
| Metaview | 企業向け | 面接の記録、ソーシング、選考、レポート | 一般提供 | 管理者がエージェントの可否を決める | https://www.metaview.ai/ |
| Alex | 企業向け | 電話と動画の面接、書類選考、日程調整 | 一般提供 | ATS 33 以上。身分証の照合 | https://www.alex.com/ |
| ConverzAI | 企業向け(人材会社) | 音声、テキスト、メールで成約まで | 不明 | 記載なし | https://www.reworked.co/the-wire/converzai-secures-16m-series-a-to-transform-recruitment-with-ai-powered-virtual-recruiters/ |
| Paraform | 企業向け | 外部リクルーターとエージェントの市場 | 一般提供 | 記載なし | https://www.paraform.com/ |
| Mercor | AI ラボ向け | 専門家をつなぐ(元は AI 採用) | 一般提供 | 記載なし(報道) | https://techcrunch.com/2025/10/27/mercor-quintuples-valuation-to-10b-with-350m-series-c/ |
| PeopleX AI 面接 | 企業向け(国内) | デジタルヒューマンの面接、評価レポート | 一般提供(2025-04) | ATS 連携の記載なし | https://ascii.jp/elem/000/004/265/4265392/ |
| harutaka AI 面接 | 企業向け(国内) | 質問を動的に作り、Web 面接に引き継ぐ | 一般提供(2025-08) | 自社の製品の中で引き継ぐ | https://www.excite.co.jp/news/article/Prtimes_2025-08-02-35867-121/ |
| HireRoo | 企業向け(国内) | コーディング試験と面接 | 一般提供 | 記載なし | https://thebridge.jp/2025/02/engineer-focused-platform-hireroo-raises-313-million-yen-in-series-a-funding |
| リクルタ AI ダイレクト採用 | 企業向け(国内) | 候補者の発掘とスカウトの送信 | ベータ | 匿名化して判定(会社の発表) | https://ascii.jp/elem/000/004/248/4248479/ |
| Wantedly AI エージェントモード | 企業向け(国内) | 要件の理解から候補者リストまで | 一般提供(2025-11) | スカウト付きプランの中 | https://aismiley.co.jp/ai_news/wantedly-ai-agent-mode/ |
| LazyApply | 求職者向け | 自動応募、紹介依頼メールの自動送信 | 一般提供 | Gmail が必須。認証情報や私的な通信も扱うと申告 | https://chromewebstore.google.com/detail/lazyapply-automate-your-j/pgnfaifdbfoiehcndkoeemaifhhbgkmm |
| Simplify Copilot | 求職者向け | フォームの自動入力、回答の下書き | 一般提供 | ページへのアクセス権。送信は本人 | https://help.simplify.jobs/articles/8686025-manage-autofill-settings-in-the-simplify-extension |
| Jobright Agent | 求職者向け | 求人を探し、書類を合わせ、代わりに応募する | 一般提供 | 送信の方法と権限の記載なし | https://jobright.ai/blog/jobright-launches-first-ai-agent-to-put-job-search-on-autopilot/ |
| AIApply | 求職者向け | 自動応募、面接中の補助 | 一般提供 | 送信前に確認できる | https://aiapply.co/ |
| Final Round AI | 求職者向け | 本番の面接中に回答を出す | 一般提供 | 画面共有に映らないと宣伝 | https://www.finalroundai.com/ |
| ミイダス AI 転職アドバイザー | 求職者向け(国内) | 会話で希望を整理し、求人を出す | ベータ | 相談内容の扱いの記載なし | https://www.value-press.com/pressrelease/367400 |

### 汎用アシスタント(詳しくは general-assistants.md)

| 名前 | 対象 | AI とエージェントでしていること | 提供の段階 | 権限とデータの扱い | 出典 |
|---|---|---|---|---|---|
| ChatGPT(apps、agent) | 求職者向けにも使われる汎用 | アプリ、ファイル、ブラウザをまたいで作業し、承認が要る所で止まる | 一般提供(Atlas は廃止と記載) | アプリはツールごとの OAuth の範囲 | https://developers.openai.com/apps-sdk/build/auth |
| Claude(in Chrome、computer use、コネクタ) | 同上 | ブラウザとデスクトップの操作、MCP のコネクタ | Chrome は有料プラン。computer use は API で安定版 | ツールごとに許可/承認/禁止(管理者)。コネクタは本人の権限を引き継ぐ | https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities |
| Gemini(タスク、Personal Intelligence) | 同上 | 手元かクラウドのブラウザでの操作、Workspace の操作 | タスクは有料プラン。PI は米国でベータ | アプリの操作ごとに許可。手元の Chrome ではログイン中の全サイトに入れる | https://support.google.com/gemini/answer/18766567?hl=en |
| Grok(Grok Bot) | 同上 | クラウドの PC での作業 | 不明 | 承認のカード、保存したログイン、MCP | https://docs.x.ai/grok-bot/overview |
| Microsoft Copilot(Cowork、Autopilot) | 企業の利用者 | Microsoft 365 の中の長い作業 | Cowork は一般提供、Autopilot は限定プレビュー | エージェントごとの Entra の ID、Purview のラベル | https://www.microsoft.com/en-us/copilot/blog/2026/06/02/introducing-microsoft-scout-your-always-on-personal-agent/ |
| Perplexity Comet | 個人 | ブラウザでの作業、買い物 | 一般提供 | 閲覧のデータは手元に保存。記憶は答えの出典から消せる | https://www.perplexity.ai/hub/legal/comet-privacy-notice |
| Apple(Siri AI) | 個人 | アプリの中の操作(App Intents) | ベータ | 権限の決め方の記載なし | https://www.apple.com/apple-intelligence/ |
| Meta(Muse) | 個人 | 買い物、予約、メールと予定の管理 | 一般提供(シンガポール) | 機微な操作の前に確認。パスワードと支払いは別の VM | https://about.fb.com/news/2026/10/muse-is-now-available-in-singapore-the-worlds-first-personal-ai-agent-built-for-everyone/ |
| LINEヤフー Agent i | 個人(国内) | 領域ごとのエージェント | 一般提供(一部はベータ) | 自社の 100 を超えるサービスのデータを使う。同意の取り方の記載なし | https://www.lycorp.co.jp/ja/news/release/020366/ |

### 人事のデータの置き場(詳しくは hr-data.md)

| 名前 | 対象 | AI とエージェントでしていること | 提供の段階 | 権限とデータの扱い | 出典 |
|---|---|---|---|---|---|
| SmartHR | 企業向け(国内) | 公式 MCP は見つからなかった | 不明 | 管理者がトークンを発行。エンドポイントと従業員項目ごとに参照/更新 | https://developer.smarthr.jp/api/about_api |
| freee人事労務 | 企業向け(国内) | 公式 freee-mcp(従業員、勤怠、給与明細) | 一般提供(公開済み) | OAuth 2.0。多くの API は管理者のみ | https://github.com/freee/freee-mcp |
| KING OF TIME | 企業向け(国内) | 見つからなかった | API は一般提供 | Bearer トークン | https://developer.kingoftime.jp/ |
| カオナビ | 企業向け(国内) | 公式 MCP は見つからなかった | API v2 は一般提供 | Consumer Key/Secret。評価の流れは API の外 | https://help.kaonavi.jp/hc/ja/article_attachments/47219709329933 |
| Workday HCM | 企業向け | Agent-Ready Tools(MCP) | 一般提供(2026-10-13) | 利用者の権限と監査の記録を引き継ぐ(会社の発表) | https://en-sg.newsroom.workday.com/2026-10-13-Workdays-Trusted-Agent-Platform-Now-Delivers-Headless-Access-to-HR-and-Finance,-Letting-Customers-Build-and-Run-Lawful-AI-Agents |
| SAP SuccessFactors | 企業向け | Joule の Assistant | 不明 | read-only の OData 権限でロールの権限を飛ばして全データが返る | https://userapps.support.sap.com/sap/support/knowledge/en/2639949 |
| BambooHR | 企業向け | 公式 MCP | ベータ | 利用者の権限を超えない | https://documentation.bamboohr.com/docs/mcp-server |
| Rippling | 企業向け | Rippling AI | 不明 | スコープと作った人の権限の両方で絞る | https://developer.rippling.com/documentation/rest-api/essentials/api-tokens |
| HiBob | 企業向け | 公式 MCP(読み書き) | ベータ(段階的に提供) | 項目ごとの閲覧/編集と対象者の範囲で絞れる | https://apidocs.hibob.com/docs/api-service-users |
| Merge | 開発者向け | Agent Handler(MCP) | 不明 | データの種類単位のスコープ。呼び出しの監査記録あり | https://docs.merge.dev/merge-agent-handler |
| Finch | 開発者向け | 公式 MCP は確かめられなかった | 不明 | 製品単位のスコープ。全権の管理者の許可が要る | https://developer.tryfinch.com/implementation-guide/Connect/Set-Up-Finch-Connect |

## ファイルの案内

| ファイル | 中身 | PRD での主な使い道 |
|---|---|---|
| [job-platforms.md](job-platforms.md) | 求人の大手(Indeed、Recruit の国内事業、LinkedIn、ZipRecruiter、ビズリーチ、エン、パーソル、ディップ など)の AI とエージェント | 課題、機会、大手との位置 |
| [ats.md](ats.md) | 主な ATS 13 件の AI、外部 API、権限の形 | 企業向けの bot の接続先 |
| [ai-hiring-tools.md](ai-hiring-tools.md) | 企業向けの AI 採用ツール、求職者向けの AI、資金調達 | 競合、求職者向けの差 |
| [general-assistants.md](general-assistants.md) | 汎用アシスタント 9 件の操作、権限、記憶、つなぐ口 | 汎用アシスタントとの違い |
| [a2a-and-permissions.md](a2a-and-permissions.md) | A2A、MCP の認可、OAuth の委任、決済の約束、VC、監査の記録 | A2A の流れ、権限の設計 |
| [regulation.md](regulation.md) | 日本、EU、米国の採用と AI の法と規制 | 権限とプライバシー、未決の論点 |
| [hr-data.md](hr-data.md) | 人事労務、勤怠、給与、評価のサービスの API | 企業向けの bot の前提 |
| [stripe-modular-agentic.md](stripe-modular-agentic.md) | Stripe のモジュール化と agentic な設計のうち使えるもの | 流程の部品化、bot に渡す鍵 |
| [market.md](market.md) | 国内の人材紹介、求人広告、HRTech の市場 | 課題の大きさ、収益の当てどころ |
| [risks.md](risks.md) | AI 採用で起きた問題と教訓 | 権限とプライバシー、安全の設計 |
| [source-check.md](source-check.md) | 出典 15 件の確かめと直し | 調べものの確からしさ |

## 見つからなかったこと

各ファイルの「見つからなかったこと」に詳しい。PRD に効くものを挙げる。

- 企業の bot と求職者の bot が A2A で直接やり取りする、公開された製品、実装、標準。
- 採用流程そのものを自然言語で設計できる製品。
- データの中身の種類(求職に関係するものだけ)で見せる範囲を決める、汎用アシスタントの設定。
- 国内の ATS(HERP Hire 以外)の公開 API と、API の操作が監査ログに残るかの文書。
- Recruit Holdings の 2026 年度 Q2 の決算資料(見た日までに見つからなかった)。
- 国内の ATS だけの市場の大きさと、ダイレクトリクルーティングの市場の大きさ。
- 運営者が見た Stripe のセミナー(2026-10-26)の公開資料。Stripe Sessions 2026 の Developer keynote などの公開文書で代えた。
- 米国イリノイ州の AI Video Interview Act と HB 3773 の一次資料(ilga.gov に接続できなかった)。施行の日は二次資料で確かめた(regulation.md「3.1」)。
- コロラド州 SB 24-205 の、2026-06-30 の後の状態。
- 国内の大手(リクナビ、タウンワーク、Airワーク)の、単独の AI 機能の一次情報。

### 調べ方の限り

- 調べものの途中で、この回の Web 検索の上限(200 回、全エージェントで共有)に達した。それ以後は、分かっている URL を直接開いて確かめた。上の「見つからなかった」には、検索を続ければ見つかるものが含まれうる。
- ログインが要るページと有料のページは読んでいない。403 や 404 で開けなかったページは、各ファイルに書いた。
