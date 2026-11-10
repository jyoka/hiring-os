# 採用 AI ツールと求職者向け AI アシスタント(2026-11 時点)

## 結論

- 企業向けでは「面接」「ソーシング」「日程調整」などの工程ごとに AI エージェントが一般提供に入った。Paradox(Workday)、Eightfold、LinkedIn、Alex などがある。ただし、確かめた範囲では、採用流程の全体を 1 つのエージェントに任せる製品は、現場職向けの Paradox の会話型 ATS に近いものしか見つからなかった。
- 2026 年に Ashby、Greenhouse、Wantedly Hire が ATS の MCP サーバーを出した。どれもベータか提供開始直後で、利用者の権限の範囲で外部の AI に読み書きさせる形になっている。「bot に権限を与えて管理を任せる」ための入口は、ATS 側でできつつある。
- 求職者向けの「応募の代行」は、LinkedIn の利用規約が bot やブラウザ拡張による自動化を禁じている。採用側も、なりすましや大量応募への対策(本人確認、スパム遮断)を製品にしている。代行と対策のいたちごっこになっている。
- 求職者向けの拡張機能は、個人情報、認証情報、私的な通信などを広く扱うと自己申告している。「求職に関係するデータだけを見る」設計を打ち出した製品は見つからなかった。
- 大きな資金は「AI 採用」から「AI ラボ向けの専門家の供給」に移った会社に集まった(Mercor の評価額 100 億ドル、micro1)。純粋な採用エージェントのラウンドは数千万ドル規模だった(Juicebox、Alex、Paraform、Metaview)。国内では PeopleX が 54.5 億円を調達した。
- 企業のエージェントと求職者のエージェントが直接やり取りする仕組み(A2A)は、確かめた範囲では見つからなかった。

## 比べる表

| 名前 | 対象 | AI とエージェントでしていること | 提供の段階 | 権限とデータの扱い | 出典 | 見た日 |
|---|---|---|---|---|---|---|
| Paradox(Workday) | 企業向け(現場職) | 会話(テキスト)で応募、選考、日程調整、内定、入社手続き | 一般提供(2026-01 に Workday 経由で提供) | Workday、SAP、Oracle と連携(会社の発表)。カレンダー連携の一次情報は見つからなかった | https://newsroom.workday.com/2026-01-08-Paradox-Conversational-Applicant-Tracking-System-ATS-Now-Available-Through-Workday,-Helping-Organizations-Hire-Frontline-Workers-Faster | 2026-11-11 |
| HireVue | 企業向け | 求職者との会話と職種の推薦(Talent Engagement)。音声の AI 面接官(Hireguide の技術を買収) | Talent Engagement は不明。AI 面接官は発表のみ | 発表に ATS 連携の記載なし | https://www.hirevue.com/press-release/hirevue-acquires-hireguide-technology-to-accelerate-agentic-ai-hiring | 2026-11-11 |
| Eightfold AI Interviewer | 企業向け | 構造化面接を並行して実施し、書き起こしと要約を作る | 一般提供(2025-10-08) | 回答の内容だけを評価し、顔認識や声の調子は使わない(会社の発表) | https://eightfold.ai/company/press/press-releases/eightfold-ai-launches-ai-interviewer-to-deliver-faster-and-more-equitable-hiring/ | 2026-11-11 |
| LinkedIn Hiring Assistant | 企業向け | 要件のヒアリング、ソーシング、応募者の確認、音声やテキストでの事前選考、日程調整 | 一般提供(英語は 2025-09 末。現在 7 言語) | LinkedIn と ATS の応募者を見る。ATS 連携は相手により異なる。採用担当が指示した作業だけをする | https://business.linkedin.com/hire/hiring-assistant | 2026-11-11 |
| Indeed Talent Scout | 企業向け | プロフィールを探し、合う人を出し、スカウト文の下書きを作る | 不明(2025-09-10 に「紹介」) | isolved、Workable、Workday(Chrome 拡張経由)と連携 | https://www.indeed.com/news/releases/indeed-introduces-new-suite-of-hiring-products-career-scout-talent-scout-premium-sponsored-jobs-and-indeed-connect?co=US | 2026-11-11 |
| Juicebox | 企業向け | 常に動くソーシングのエージェント、送信と追いかけをするアウトリーチのエージェント | 一般提供 | 8 億件のプロフィール、30 以上のデータ源(会社の発表)。Greenhouse、Lever、Ashby ほか。文面は人が承認する | https://juicebox.ai/ | 2026-11-11 |
| Metaview | 企業向け | 面接の記録から始め、ソーシング、応募書類の確認、選考、レポートのエージェントへ | 一般提供(エージェントごとの課金) | Ashby、Greenhouse、Lever、Gem、SmartRecruiters。管理者がエージェントの可否を決め、判断の記録を残す | https://www.metaview.ai/ | 2026-11-11 |
| Alex | 企業向け | 動画と電話の面接、書類選考、次の面接の日程調整、記録を ATS に上げる | 一般提供 | ATS 連携 33 以上。面接中に身分証と自撮りを照合する機能がある | https://www.alex.com/ | 2026-11-11 |
| ConverzAI | 企業向け(人材会社) | 音声、テキスト、メールで求職者と会話し、ソーシングから成約まで | 一般提供(会社の発表から推定) | ATS 連携の記載なし | https://www.reworked.co/the-wire/converzai-secures-16m-series-a-to-transform-recruitment-with-ai-powered-virtual-recruiters/ | 2026-11-11 |
| Paraform | 企業向け | 外部の専門リクルーター 1 万人以上と、企業ごとのエージェントを組み合わせる | 一般提供 | ATS 連携の記載なし。リクルーター向けの AI 道具は無料 | https://www.paraform.com/ | 2026-11-11 |
| Mercor | 企業向け(AI ラボ) | AI 採用から始め、今は AI ラボに専門家をつなぐ | 一般提供 | 専門家 3 万人以上(報道) | https://techcrunch.com/2025/10/27/mercor-quintuples-valuation-to-10b-with-350m-series-c/ | 2026-11-11 |
| micro1(Zara) | 企業向け(AI ラボ) | AI 面接官 Zara が業務委託の候補者を面接し、評価する | 一般提供 | 記載なし | https://dataconomy.com/2025/09/16/ai-data-startup-micro1-raises-35-million-at-a-500-million-valuation | 2026-11-11 |
| PeopleX AI 面接 | 企業向け(国内) | デジタルヒューマンが 24 時間面接し、評価レポートを自動で作る | 一般提供(2025-04-24) | ATS 連携の記載なし | https://ascii.jp/elem/000/004/265/4265392/ | 2026-11-11 |
| harutaka AI 面接(ZENKIGEN) | 企業向け(国内) | 応募者に合わせて質問を動的に作る。結果を後の Web 面接に引き継ぐ | 提供開始(2025-08-02) | 自社の harutaka 内でデータを引き継ぐ | https://www.excite.co.jp/news/article/Prtimes_2025-08-02-35867-121/ | 2026-11-11 |
| VARIETAS AI 面接官 | 企業向け(国内) | エントリーシートを読み、一次面接をし、社会人基礎力で評価する | 一般提供(導入企業の記載あり) | 記載なし | https://kepple.co.jp/articles/dkjrjum3yma | 2026-11-11 |
| HireRoo | 企業向け(国内、エンジニア) | コーディング試験と面接での掘り下げ | 一般提供 | 記載なし | https://thebridge.jp/2025/02/engineer-focused-platform-hireroo-raises-313-million-yen-in-series-a-funding | 2026-11-11 |
| リクルタ AI ダイレクト採用(Algomatic Works) | 企業向け(国内) | 候補者を探し、転職意欲が上がった時にスカウトを送る | ベータ(2025-01-30) | どの媒体でどう操作するかの記載なし。プロフィールを匿名化して判定 | https://ascii.jp/elem/000/004/248/4248479/ | 2026-11-11 |
| Wantedly AI エージェントモード | 企業向け(国内) | 採用要件の理解から、候補者の選別とリスト化まで | 提供開始(2025-11-25) | スカウト付きプランで追加費用なし | https://aismiley.co.jp/ai_news/wantedly-ai-agent-mode/ | 2026-11-11 |
| Ashby MCP Server | 企業向け(ATS の口) | 外部の AI から候補者の検索、選考段階の変更、メモの追加など | 公開ベータ(2026-06-29) | 利用者ごとの OAuth。利用者の権限の範囲だけ。管理者が有効にする | https://docs.ashbyhq.com/ashby-mcp-server-beta | 2026-11-11 |
| Greenhouse MCP | 企業向け(ATS の口) | 外部の AI から読み書き。不採用や採用は人の確認が必要 | 公開ベータ | OAuth 2.0 + PKCE。管理者が範囲の上限を決める | https://support.greenhouse.io/hc/en-us/articles/53944054829083-Greenhouse-MCP-security-FAQ | 2026-11-11 |
| Wantedly Hire MCP Server | 企業向け(ATS の口、国内) | 選考データの閲覧、検索、集計 | 提供開始(2026-08-31)。今は読み取りだけ | 個人のアクセストークン。利用者の権限に従う | https://www.tv-tokyo.co.jp/plus/external-pr/entry/225784.html | 2026-11-11 |
| LazyApply | 求職者向け | 複数の求人サイトに自動で応募し、社員に紹介依頼メールを自動で送る | 一般提供 | Gmail のアカウントが必須。拡張機能は認証情報や私的な通信も扱うと申告 | https://lazyapply.com/ | 2026-11-11 |
| Simplify Copilot | 求職者向け | 応募フォームの自動入力。固有の質問への回答を AI が下書き | 一般提供(Firefox 版はベータ) | ページへのアクセス権が必要。送信は本人が押す | https://help.simplify.jobs/articles/8686025-manage-autofill-settings-in-the-simplify-extension | 2026-11-11 |
| Jobright Agent | 求職者向け | 求人を探し、書類を合わせ、代わりに応募する | 一般提供(自動応募は有料の解放と読める) | 送信の方法と必要な権限の記載なし | https://jobright.ai/blog/jobright-launches-first-ai-agent-to-put-job-search-on-autopilot/ | 2026-11-11 |
| AIApply | 求職者向け | 求人を探し、書類を合わせて応募。面接中に回答を出す機能も | 一般提供 | 送信前に下書きを確認できる。権限の記載なし | https://aiapply.co/ | 2026-11-11 |
| Final Round AI | 求職者向け | 本番の面接中に回答を画面に出す | 一般提供(有料) | 画面共有や録画に映らないと宣伝 | https://www.finalroundai.com/ | 2026-11-11 |
| Indeed Career Scout | 求職者向け | キャリアの相談、求人の推薦、応募の事前入力、履歴書の調整、面接練習 | 不明(2025-09-10 に「紹介」) | Indeed アプリの中で動く | https://www.indeed.com/news/releases/indeed-introduces-new-suite-of-hiring-products-career-scout-talent-scout-premium-sponsored-jobs-and-indeed-connect?co=US | 2026-11-11 |
| ミイダス AI 転職アドバイザー | 求職者向け(国内) | 会話で希望を整理し、検索条件と求人を出す | ベータ(2026-01-06) | 相談内容の扱いの記載なし | https://www.value-press.com/pressrelease/367400 | 2026-11-11 |

## 企業向け(海外)

### Paradox(Workday が買収)

- Workday は 2025-10-01 に Paradox の買収を終えた。金額は公表していない（出典: https://newsroom.workday.com/2025-10-01-Workday-Completes-Acquisition-of-Paradox、見た日 2026-11-11）。
- Workday は Paradox を、HiredScore(候補者の発見)と Workday Recruiting(採用と入社)と合わせた一つの基盤として売る（出典: 同上、見た日 2026-11-11）。
- 2026-01-08 に、会話型 ATS が Workday 経由で提供された。応募はテキストの会話で約 2 分。選考と日程調整は AI が求職者と直接行い、内定と入社書類もテキストで送る（出典: https://newsroom.workday.com/2026-01-08-Paradox-Conversational-Applicant-Tracking-System-ATS-Now-Available-Through-Workday,-Helping-Organizations-Hire-Frontline-Workers-Faster、見た日 2026-11-11）。
- 同じ発表で、平均の採用までの日数が 3.5 日、応募の完了率が 72% としている（会社の発表）（出典: 同上、見た日 2026-11-11）。
- 勤務時間やシフトの変更をテキストで扱う Workday Frontline Agent は「2026 年春」の予定とされた（出典: 同上、見た日 2026-11-11）。今の提供状況は確かめていない。
- 連携先として Workday、SAP、Oracle を挙げている（会社の発表）（出典: https://www.paradox.ai/llms.txt、見た日 2026-11-11）。

### HireVue

- 2025-08-12 に、求職者と会話して合う職種を推薦するエージェント「Talent Engagement」を発表した。発表には提供の時期も ATS 連携も書かれていない（出典: https://www.hirevue.com/press-release/hirevue-launches-talent-engagement-agent-to-solve-the-hiring-speed-vs-quality-trade-off、見た日 2026-11-11）。
- 同じ発表で、顧客 1,150 社以上、動画面接 7,000 万件以上としている（会社の発表）（出典: 同上、見た日 2026-11-11）。
- 2026-03-10 に Hireguide の技術を買収した。音声の AI 面接官を「最初の到達点」と位置づけた。提供の時期は書かれていない（出典: https://www.hirevue.com/press-release/hirevue-acquires-hireguide-technology-to-accelerate-agentic-ai-hiring、見た日 2026-11-11）。

### Eightfold AI

- 2025-10-08 に AI Interviewer を出した。中小企業と大企業に「本日から」提供とした（出典: https://eightfold.ai/company/press/press-releases/eightfold-ai-launches-ai-interviewer-to-deliver-faster-and-more-equitable-hiring/、見た日 2026-11-11）。
- 評価は回答の内容だけで、顔認識、声の調子、生体情報は使わないとしている。NYC Local Law 144 などへの準拠と ISO/IEC 42001 などの認証を挙げる（会社の発表）（出典: 同上、見た日 2026-11-11）。
- 2026-04-08 に、人が行う面接を補助する AI Interview Companion と、職能別とコーディングの面接を足した（出典: https://eightfold.ai/company/press/press-releases/eightfold-ai-expands-talent-agents-across-the-full-interview-journey-introducing-ai-interview-companion-and-new-interview-capabilities/、見た日 2026-11-11）。Companion の提供段階は書かれていない。

### LinkedIn Hiring Assistant

- 2024-10 に一部の顧客に出し、2025-09 末に英語で全世界に提供するとした（出典: https://news.linkedin.com/2025/hiring-assistant-globally-available、見た日 2026-11-11）。
- 初期の利用者で 1 職種あたり 4 時間以上の削減、確認したプロフィールが 62% 減としている（会社の発表）（出典: 同上、見た日 2026-11-11）。
- 製品ページでは、要件のヒアリング、ソーシング、LinkedIn と ATS の応募者の確認、音声やテキストでの事前選考、日程調整までを挙げる（出典: https://business.linkedin.com/hire/hiring-assistant、見た日 2026-11-11）。
- 「指示した作業だけをする」と書く。LinkedIn Recruiter の追加機能として売られ、ATS 連携は相手により異なる（出典: 同上、見た日 2026-11-11）。

### Indeed Talent Scout

- 2025-09-10 に、企業向けの Talent Scout と求職者向けの Career Scout を同時に紹介した（出典: https://www.indeed.com/news/releases/indeed-introduces-new-suite-of-hiring-products-career-scout-talent-scout-premium-sponsored-jobs-and-indeed-connect?co=US、見た日 2026-11-11）。
- Talent Scout は、検索できるプロフィールを調べ、合う人を出し、スカウト文の下書きを助ける。isolved、Workable、Workday(Chrome 拡張経由)の ATS とつながる（出典: 同上、見た日 2026-11-11）。
- 発表には提供段階が書かれていない。

### Juicebox(PeopleGPT)

- 2025-09-25 に Sequoia が主導する 3,000 万ドルのシリーズ A を発表した。累計は 3,600 万ドル。顧客 2,500 社以上、ARR 1,000 万ドル超（報道）（出典: https://techcrunch.com/2025/09/25/juicebox-raises-30m-from-sequoia-to-revolutionize-hiring-with-llm-powered-search/、見た日 2026-11-11）。
- 常に動くソーシングのエージェントが候補を出し、アウトリーチのエージェントが送信と追いかけと返信の追跡をする。文面は人が承認する（出典: https://juicebox.ai/、見た日 2026-11-11）。
- 8 億件のプロフィールと 30 以上のデータ源を使うとする（会社の発表）。Greenhouse、Lever、Ashby ほか 40 以上の ATS とつながり、Gmail と Outlook のロゴを出している。SOC 2 Type II（出典: 同上、見た日 2026-11-11）。

### Metaview

- 2025-06-27 に GV が主導する 3,500 万ドルのシリーズ B を発表した。累計 5,000 万ドル（報道）（出典: https://www.unleash.ai/hr-technology/news/google-ventures-leads-35-million-series-b-funding-in-metaview、見た日 2026-11-11）。
- CEO は面接の記録(ノートテイカー)を「入り口」と呼び、採用の各段階のエージェントに広げるとした（報道）（出典: 同上、見た日 2026-11-11）。
- 今はソーシング、書類の確認、選考、記録、レポートのエージェントを出す。使うエージェントの分だけ払う（出典: https://www.metaview.ai/、見た日 2026-11-11）。
- 連携先は Ashby、Greenhouse、Lever、Gem、SmartRecruiters。管理者が「エージェントができること、できないこと」を決め、判断の手順を記録で見られる（出典: 同上、見た日 2026-11-11）。

### Alex

- 2025-09-29 に、Peak XV が主導する 1,700 万ドルのシリーズ A と、300 万ドルのシード(計 2,000 万ドル)を発表した（出典: https://www.alex.com/blog/we-raised-20m-to-help-ai-hire-more-humans、見た日 2026-11-11）。
- 動画と電話の面接、書類選考、次の面接の日程調整、記録を ATS に上げる作業など、20 以上の自動の作業をこなすとする（出典: 同上、見た日 2026-11-11）。
- 電話、動画、SMS、WhatsApp で動く。面接中に身分証と自撮りを照合する「Identity」と、面接を見張る「Proctor」がある（出典: https://www.alex.com/、見た日 2026-11-11）。

### ConverzAI

- 2025-02-11 に Menlo Ventures が主導する 1,600 万ドルのシリーズ A を発表した（出典: https://www.reworked.co/the-wire/converzai-secures-16m-series-a-to-transform-recruitment-with-ai-powered-virtual-recruiters/、見た日 2026-11-11）。
- 仮想のリクルーターが音声、テキスト、メールで求職者と会話し、ソーシングから成約までを担うとする（会社の発表）（出典: 同上、見た日 2026-11-11）。

### Paraform

- 外部の専門リクルーター 1 万人以上と、企業ごとのエージェントを組み合わせる（出典: https://www.paraform.com/、見た日 2026-11-11）。
- リクルーターには、ソーシング、マッチング、CRM、記録、日程調整の AI 道具を無料で渡す。平均の採用日数 27 日としている（会社の発表）（出典: 同上、見た日 2026-11-11）。
- 2026-03 に Scale Venture Partners が主導する 4,000 万ドルのシリーズ B が報じられた（報道）（出典: https://hrtechfeed.com/?p=449861、見た日 2026-11-11）。

### Mercor と micro1(採用 AI から AI ラボ向けへ)

- Mercor は 2025-10-27 に、評価額 100 億ドルで 3 億 5,000 万ドルのシリーズ C を確認した。主導は Felicis（報道）（出典: https://techcrunch.com/2025/10/27/mercor-quintuples-valuation-to-10b-with-350m-series-c/、見た日 2026-11-11）。
- 同じ記事は、Mercor が AI 採用の基盤として始まり、今は AI ラボに専門家をつなぐと書く。専門家は 3 万人以上、平均時給 85 ドル超（報道）（出典: 同上、見た日 2026-11-11）。
- Mercor のサイトは、専門家の募集、人による評価、企業データの収益化を前に出している。採用ツールとしての説明は見つからなかった（出典: https://www.mercor.com/、見た日 2026-11-11）。
- micro1 は 2025-09 に評価額 5 億ドルで 3,500 万ドルのシリーズ A を調達した。AI 面接官 Zara が業務委託の候補者を面接し、AI ラボに専門家を出す（報道）（出典: https://dataconomy.com/2025/09/16/ai-data-startup-micro1-raises-35-million-at-a-500-million-valuation、見た日 2026-11-11）。

## 企業向け(国内)

### PeopleX AI 面接

- 2025-04-24 に、デジタルヒューマンの AI 面接「People XRecruit」を正式に出した（会社の発表の転載）（出典: https://ascii.jp/elem/000/004/265/4265392/、見た日 2026-11-11）。
- 24 時間面接でき、職種ごとに質問を決められる。面接後に動画、書き起こし、評価レポートを自動で作る。新卒、中途、アルバイトに対応（出典: 同上、見た日 2026-11-11）。
- 2026-09-02 に、シリーズA で 54.5 億円(増資と融資)を発表した。累計は 78.2 億円（報道）（出典: https://thebridge.jp/2026/09/peoplex-raises-series-a-to-develop-hr-llm-and-athena、見た日 2026-11-11）。
- 同じ記事で、AI 製品の提供開始から 15 か月で ARR 10 億円としている（会社の発表）。人事に特化した LLM と、複数の AI 製品を束ねる「Athena」は開発段階（報道）（出典: 同上、見た日 2026-11-11）。

### harutaka AI 面接(ZENKIGEN)

- 2025-08-02 に「harutaka AI 面接」の提供開始を発表した（会社の発表の転載）（出典: https://www.excite.co.jp/news/article/Prtimes_2025-08-02-35867-121/、見た日 2026-11-11）。
- AI 面接官が応募者の特性を分析し、質問や場面を動的に作る。結果は後の Web 面接に自動で引き継ぐ（出典: 同上、見た日 2026-11-11）。
- 企業ごとの質問のカスタマイズは「目指す」段階とされた（出典: 同上、見た日 2026-11-11）。

### VARIETAS(AI 面接官)

- AI がエントリーシートを読み、一次面接をする。経済産業省の社会人基礎力で評価する（報道）（出典: https://kepple.co.jp/articles/dkjrjum3yma、見た日 2026-11-11）。
- シリーズA で 6 億円を調達した。引受先は ALL STAR SAAS FUND とグローバル・ブレイン。記事の日付は 2025-03-11（報道）（出典: 同上、見た日 2026-11-11）。

### HireRoo

- 2025-02-06 に、シリーズA のファーストクローズで約 3.13 億円を発表した。累計 5.5 億円（報道）（出典: https://thebridge.jp/2025/02/engineer-focused-platform-hireroo-raises-313-million-yen-in-series-a-funding、見た日 2026-11-11）。
- コーディング試験と面接での掘り下げを出す。導入は約 150 社（報道）（出典: 同上、見た日 2026-11-11）。AI の機能は一次情報で確かめていない。

### リクルタ AI ダイレクト採用(Algomatic Works)

- 2025-01-30 に、スカウトに特化した AI エージェントのベータ版を出した（会社の発表の転載）（出典: https://ascii.jp/elem/000/004/248/4248479/、見た日 2026-11-11）。
- 募集要項からプロンプトを作り、プロフィールを匿名化してマッチ度を判定する。転職意欲が上がった時にスカウトを送り、文面を候補者に合わせる（出典: 同上、見た日 2026-11-11）。
- 採用コンサルタントが AI の設定を調整する。どの媒体でどう操作するかは書かれていない（出典: 同上、見た日 2026-11-11）。

### Wantedly(AI エージェントモードと Hire MCP Server)

- 2025-11-25 に「AI エージェントモード」を出した。採用要件の理解から候補者の選別、リスト化までを担う（報道）（出典: https://aismiley.co.jp/ai_news/wantedly-ai-agent-mode/、見た日 2026-11-11）。
- スカウト付きプランの企業は追加費用なしで使える。スカウトの送信を誰がするかは書かれていない（出典: 同上、見た日 2026-11-11）。
- 2026-08-31 に、ATS「Wantedly Hire」の MCP サーバーを出した。対応は Claude、Cursor、VS Code（会社の発表の転載）（出典: https://www.tv-tokyo.co.jp/plus/external-pr/entry/225784.html、見た日 2026-11-11）。
- 今は読み取りだけで、書き込みは予定。個人の画面でトークンを発行し、利用者の権限に従う（出典: 同上、見た日 2026-11-11）。

## ATS が AI に口を開け始めた(MCP)

- Ashby は 2026-06-29 に、MCP サーバーを全プランで公開ベータにした（出典: https://www.ashbyhq.com/product-updates/mcp、見た日 2026-11-11）。
- Ashby では、管理者が有効にした後、利用者ごとに OAuth で接続する。見られるのは、その利用者の Ashby の権限の範囲だけ（出典: https://docs.ashbyhq.com/ashby-mcp-server-beta、見た日 2026-11-11）。
- Ashby の道具には、候補者の作成、選考段階の変更(不採用での保管を含む)、メモの追加がある。メモは保存前に人が確かめる。上限は 1 トークンあたり毎分 120 件（出典: 同上、見た日 2026-11-11）。
- Greenhouse MCP は公開ベータで、Core、Plus、Pro の契約が対象。読み書きの両方ができる。管理者が決めた範囲を、利用者は超えられない（出典: https://support.greenhouse.io/hc/en-us/articles/52090956642075-Greenhouse-MCP、見た日 2026-11-11）。
- Greenhouse は OAuth 2.0 と PKCE を使う。不採用や採用などの 5 つの操作は、人がはっきり確認するまで動かない。添付の中身は返さない（出典: https://support.greenhouse.io/hc/en-us/articles/53944054829083-Greenhouse-MCP-security-FAQ、見た日 2026-11-11）。
- Greenhouse は、AI の会話の中身を受け取らず、保存もしない。保存は AI 側の会社の方針による（出典: 同上、見た日 2026-11-11）。

## 求職者向け

### LazyApply

- Greenhouse、Dice、Indeed、ZipRecruiter などで自動で応募するとする。応募先の会社の社員に紹介依頼のメールを自動で送る機能もある（出典: https://lazyapply.com/、見た日 2026-11-11）。
- 1 日の応募数の上限は、プランで 15、150、1,500 件。年額は 99、149、999 ドル。登録のメールは Gmail に限る（出典: 同上、見た日 2026-11-11）。
- Chrome 拡張は利用者 2 万人。扱うデータとして、個人を特定する情報、認証情報、私的な通信、位置、利用の記録、サイトの内容を申告している（出典: https://chromewebstore.google.com/detail/lazyapply-automate-your-j/pgnfaifdbfoiehcndkoeemaifhhbgkmm、見た日 2026-11-11）。

### Simplify Copilot

- 応募フォームを自動で入力する。有料版では、固有の質問への回答をプロフィールから AI が下書きする（出典: https://help.simplify.jobs/articles/8686025-manage-autofill-settings-in-the-simplify-extension、見た日 2026-11-11）。
- 設定は「Copilot に応募を送信させない」。最後の送信は本人が押す（出典: 同上、見た日 2026-11-11）。
- Chrome 拡張は利用者 50 万人。扱うデータは個人を特定する情報、位置、サイトの内容。自動入力にはページへのアクセス権が要る（出典: https://chromewebstore.google.com/detail/simplify-copilot-autofill/pbanhockgagggenencehbnadejlgchfc、見た日 2026-11-11）。

### Jobright Agent

- 2025-06-24 に、求人を探し、応募書類を作り、代わりに送る「Jobright Agent」を出した（出典: https://jobright.ai/blog/jobright-launches-first-ai-agent-to-put-job-search-on-autopilot/、見た日 2026-11-11）。
- 同時に、Translink Capital が主導する 320 万ドルを調達した。Indeed の関連の投資会社 HR Tech Investments も加わった（出典: 同上、見た日 2026-11-11）。
- 利用者 52 万人以上、探す時間 80% 減としている（会社の発表）（出典: 同上、見た日 2026-11-11）。
- どう送信するか、どの権限が要るかは、発表にも製品ページにも書かれていない（出典: https://jobright.ai/ai-agent、見た日 2026-11-11）。

### AIApply

- Auto Apply は、条件に合う求人を探し、書類を合わせて送信する。送る前に下書きを確かめられる。クレジット制（出典: https://aiapply.co/、見た日 2026-11-11）。
- 「Interview Buddy」は、面接中に回答の候補を出す（出典: 同上、見た日 2026-11-11）。

### Final Round AI

- Interview Copilot は、本番の面接を聞き、本人だけに見える画面に回答を出す。「100% 検出されない」と宣伝し、Zoom などの画面共有や録画に映らないとする（出典: https://www.finalroundai.com/、見た日 2026-11-11）。
- 2025 年 1 月末に 688 万ドルのシードを調達した（報道）（出典: https://pulse2.com/final-round-ai-job-search-journey-company-closes-6-88-million-seed、見た日 2026-11-11）。

### Indeed Career Scout

- Indeed アプリの中の AI のキャリアコーチ。応募の事前入力、履歴書の調整、面接練習ができる。自分で応募を送るとは書かれていない（出典: https://www.indeed.com/news/releases/indeed-introduces-new-suite-of-hiring-products-career-scout-talent-scout-premium-sponsored-jobs-and-indeed-connect?co=US、見た日 2026-11-11）。
- 米国での試験で、探して応募するまでが 7 倍速く、応募あたりの採用が 38% 高いとする（会社の発表）（出典: 同上、見た日 2026-11-11）。

### ミイダス AI 転職アドバイザー(国内)

- 2026-01-06 にベータ版を出した。会話で希望を整理し、検索条件と求人を出す。気になる求人にはそのまま応募できる（会員登録が必要）（出典: https://www.value-press.com/pressrelease/367400、見た日 2026-11-11）。
- 「予告なく終了する可能性がある」と書く。相談内容の扱いは書かれていない（出典: 同上、見た日 2026-11-11）。

## 応募の代行と規約、採用側の反応

### 規約

- LinkedIn の利用規約(2025-11-03 施行)の 8.2 は、ブラウザのプラグインや拡張などを使ったデータの取得を禁じる。bot など許可のない自動の方法でサービスに入り、メッセージを送ることも禁じる（出典: https://www.linkedin.com/legal/user-agreement、見た日 2026-11-11）。
- 推測: LinkedIn の上で応募やメッセージを自動で送る求職者向けの道具は、この条項に触れやすい。LazyApply の公式サイトは、対応先に LinkedIn を挙げていなかった（出典: https://lazyapply.com/、見た日 2026-11-11）。

### 大量応募の実態

- Greenhouse の 2025 年の調査(2025-11-19 発表、4,136 人)では、米国の求職者の 49% が前の年より多く応募した（出典: https://www.greenhouse.com/newsroom/an-ai-trust-crisis-70-of-hiring-managers-trust-ai-to-make-faster-and-better-hiring-decisions-only-8-of-job-seekers-call-it-fair、見た日 2026-11-11）。
- 同じ調査で、米国の採用担当の 34% が、週の半分までをスパムやごみの応募の選別に使う。米国の求職者の 41% がプロンプトインジェクションを使ったと認めた（出典: 同上、見た日 2026-11-11）。
- LinkedIn 経由の応募は過去 1 年で 45% 超増えた。ある採用担当は、1 か月で応募が 4〜5 倍になった会社を見たと話した（報道）（出典: https://fortune.com/2025/11/18/hiring-job-seekers-recruiters-talent-acquisition-ai-doom-loop-application-technology/、見た日 2026-11-11）。

### 採用側の対策

- Greenhouse は、なりすましの定義に「AI や第三者を使って大量に応募する人」を含める。不正の検出、スパムの遮断(IP やメールのドメイン)、CLEAR による本人確認を出す（出典: https://greenhouse.com/greenhouse-real-talent、見た日 2026-11-11）。
- 不正の検出は AI を使わず、電話番号、メール、IP、位置から 26 の信号を出す。AI の照合は「候補者を進めたり落としたりしない」（出典: 同上、見た日 2026-11-11）。
- Real Talent は、本人確認、不正の検出、スパムの遮断、照合の 4 つでできている（出典: https://support.greenhouse.io/hc/en-us/articles/45127324799003-Real-Talent-overview、見た日 2026-11-11）。
- Alex は面接中に身分証と自撮りを照合し、面接を見張る機能を持つ（出典: https://www.alex.com/、見た日 2026-11-11）。

## 資金調達(2025-2026 年の主なもの)

| 会社 | 日付 | 内容 | 主導 | 出典の種類 | 出典 | 見た日 |
|---|---|---|---|---|---|---|
| Mercor | 2025-10-27 | シリーズ C 3.5 億ドル、評価額 100 億ドル | Felicis | 報道(会社が確認) | https://techcrunch.com/2025/10/27/mercor-quintuples-valuation-to-10b-with-350m-series-c/ | 2026-11-11 |
| micro1 | 2025-09 | シリーズ A 3,500 万ドル、評価額 5 億ドル | O1 Advisors | 報道 | https://dataconomy.com/2025/09/16/ai-data-startup-micro1-raises-35-million-at-a-500-million-valuation | 2026-11-11 |
| Paraform | 2026-03 | シリーズ B 4,000 万ドル | Scale Venture Partners | 報道 | https://hrtechfeed.com/?p=449861 | 2026-11-11 |
| Metaview | 2025-06-27 | シリーズ B 3,500 万ドル | GV | 報道 | https://www.unleash.ai/hr-technology/news/google-ventures-leads-35-million-series-b-funding-in-metaview | 2026-11-11 |
| Juicebox | 2025-09-25 | シリーズ A 3,000 万ドル(累計 3,600 万ドル) | Sequoia | 報道 | https://techcrunch.com/2025/09/25/juicebox-raises-30m-from-sequoia-to-revolutionize-hiring-with-llm-powered-search/ | 2026-11-11 |
| Alex | 2025-09-29 | シリーズ A 1,700 万ドル + シード 300 万ドル | Peak XV | 会社の発表 | https://www.alex.com/blog/we-raised-20m-to-help-ai-hire-more-humans | 2026-11-11 |
| ConverzAI | 2025-02-11 | シリーズ A 1,600 万ドル | Menlo Ventures | 会社の発表(配信) | https://www.reworked.co/the-wire/converzai-secures-16m-series-a-to-transform-recruitment-with-ai-powered-virtual-recruiters/ | 2026-11-11 |
| Final Round AI | 2025-01 末 | シード 688 万ドル | Uncork Capital | 報道 | https://pulse2.com/final-round-ai-job-search-journey-company-closes-6-88-million-seed | 2026-11-11 |
| Jobright | 2025-06-24 | 320 万ドル | Translink Capital | 会社の発表 | https://jobright.ai/blog/jobright-launches-first-ai-agent-to-put-job-search-on-autopilot/ | 2026-11-11 |
| Paradox | 2025-10-01 | Workday が買収(金額非公表) | - | 会社の発表 | https://newsroom.workday.com/2025-10-01-Workday-Completes-Acquisition-of-Paradox | 2026-11-11 |
| PeopleX | 2026-09-02 | シリーズA 54.5 億円(増資と融資)、累計 78.2 億円 | - (引受先はエン、WiL など) | 報道 | https://thebridge.jp/2026/09/peoplex-raises-series-a-to-develop-hr-llm-and-athena | 2026-11-11 |
| VARIETAS | 2025-03(記事の日付) | シリーズA 6 億円 | ALL STAR SAAS FUND、グローバル・ブレイン | 報道 | https://kepple.co.jp/articles/dkjrjum3yma | 2026-11-11 |
| HireRoo | 2025-02-06 | シリーズA 約 3.13 億円(累計 5.5 億円) | DEEPCORE ほか | 報道 | https://thebridge.jp/2025/02/engineer-focused-platform-hireroo-raises-313-million-yen-in-series-a-funding | 2026-11-11 |

- Juicebox の会社のブログ(資金調達の記事)は、開いても本文が取れなかった。金額は TechCrunch による。

## このプロダクトへの示唆

### 点の自動化か、流程全体か(確かめた範囲)

| 分類 | 製品 | 根拠 |
|---|---|---|
| 点の自動化(1 つの工程) | PeopleX AI 面接、harutaka AI 面接、VARIETAS、HireRoo、Eightfold AI Interviewer、HireVue の AI 面接官、Final Round AI、Simplify Copilot | 面接、試験、入力などの 1 工程だけを扱う。上の各節を参照 |
| 点の自動化(ソーシングとスカウト) | Juicebox、リクルタ AI、Wantedly AI エージェントモード、Indeed Talent Scout | 探す工程とスカウトの工程。文面の承認や送信は人が残る例が多い |
| 複数の工程をまたぐ | LinkedIn Hiring Assistant、Alex、Metaview、ConverzAI | ヒアリングから事前選考、日程調整までをまたぐ。ただし採用担当の指示の範囲で動く |
| 流程全体に近い | Paradox の会話型 ATS | 応募から選考、日程調整、内定、入社書類までを会話で扱う。対象は現場職で、自社の ATS の中に限る |
| 求職者側の流程 | Jobright Agent、AIApply、LazyApply | 探す、書類を作る、送るをまたぐ。ただし企業側の仕組みとは直接つながらず、フォームへの入力で送る |

- 自然言語で採用流程そのものを設計させる製品は、確かめた範囲では見つからなかった。Metaview の「エージェントができること、できないことを管理者が決める」が最も近い。
- 推測: 既存の製品は、ATS や求人媒体の上に「工程ごとのエージェント」を足す形が中心。「流程の設計」と「工程の実行」を同じ自然言語の層で扱う製品は、まだ空いている。

### 「bot に権限を与える」の土台

- Ashby、Greenhouse、Wantedly Hire の MCP は、利用者の権限を超えない、管理者が範囲を決める、重い操作は人が確かめる、という形でそろってきた。
- 推測: このプロダクトは、ATS を作り直すより、これらの MCP や API の上で「権限の設計」と「流程の設計」を担う方が早い。ただし、どれもベータで、仕様は予告なく変わりうる（出典: https://docs.ashbyhq.com/ashby-mcp-server-beta、見た日 2026-11-11）。

### 求職者向けの差別化

- 既存の自動応募の道具は、ブラウザ拡張で広いデータを扱う(LazyApply は認証情報や私的な通信まで)。「求職のデータだけ」に絞ることを打ち出した製品は見つからなかった。
- 推測: 「見るデータを求職に関係するものに限る」は、汎用アシスタントとの差として打ち出せる。Gmail を読む場合も、応募と面接の連絡だけに絞る設計が要る。
- 推測: フォームへの自動入力と大量応募は、LinkedIn の規約と採用側のスパム対策の両方とぶつかる。求職者のエージェントを広げるなら、企業側と正規の口(A2A や API)でつながる方が持続しやすい。

### 大手の位置

- Indeed、LinkedIn、Workday は、2025 年にエージェントを出した。「大手は AI ネイティブでない」は、「エージェントを出していない」という意味では当てはまらない。
- 一方で、Indeed の Career Scout は応募の事前入力までで、Talent Scout は下書きの支援まで。提供段階も書かれていない。LinkedIn Hiring Assistant は「指示した作業だけをする」。
- 推測: 大手は自社の媒体や ATS の中でエージェントを動かしており、企業と求職者の双方のエージェントが媒体をまたいでやり取りする形にはなっていない。ここが機会になりうる。

### 資金の流れ

- 推測: Mercor と micro1 の例は、「AI で面接と評価をする」技術が AI ラボ向けの専門家の市場で大きく稼いだことを示す。採用の流程そのものを担う会社のラウンドは、数千万ドル規模にとどまる。

## 見つからなかったこと

- 企業のエージェントと求職者のエージェントが直接やり取りする(A2A)採用の製品や標準。
- 採用流程そのものを自然言語で設計できる製品。
- リクルート(リクナビ、リクルートエージェント)と doda の、求職者向けの AI エージェントの公式発表。検索では求人票しか見つからなかった。
- 国内で、求職者の代わりに応募を送る AI のサービス。
- Sansan や Eight の採用の AI、YOUTRUST の AI、Spready、MatchBox などの日程調整、ラプラス。今回は調べきれなかった。
- Sonara の現状。2024 年の終了と、その後の再開を書いた記事は、競合の会社のブログばかりで、一次情報は見つからなかった。開いて確かめてもいない。
- Paradox のカレンダー連携(Google や Outlook)の一次情報。
- Jobright Agent の送信の方法と、必要な権限。
- Moonhub、BrightHire、Tezi、Apriora、Classet、Massive、LoopCV は、今回は一次情報を開いていない。
- 採用側が 1 人あたりの応募数に上限を設けた一次情報(OpenAI の採用ページは 403 で開けなかった)。
- HireRoo の AI 評価の機能の一次情報。
- Juicebox の資金調達のブログ記事の本文(開いても本文が取れなかった)。Paraform のシリーズ B の Axios 記事(403 で開けなかった)。
