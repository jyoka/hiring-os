# 求人検索と求人メディアの大手の AI とエージェント(2026-11 時点)

## 結論

- 大手の AI 投資は企業向けが先だった。Recruit は「過去 2〜3 年の AI 開発投資は企業向けの道具に集中した」と決算説明で述べた。Indeed の応募の 70% は、キーワード検索ではなく AI の提案から来ている(会社の発表)。
- 企業向けは「ソーシングと書類選考の自動化」が一般提供に入った。Indeed の Sourcing Assistant と Smart Screening、LinkedIn の Hiring Assistant がある。ただし、どれも自社の求人と自社の候補者の範囲で動く。内定、条件交渉、入社手続きは対象外で、Indeed の CEO は「多くの企業のシステムと連携すると遅くなる」と述べた。
- 求職者向けの「代わりに動く」機能は、まだ試験か下書きどまりだった。Indeed の Apply For Me は米国の限定試験で、自動応募のモードは 2026-08 に止めた。LinkedIn と Indeed の利用規約は、外部の bot による自動化を禁じている。
- 外部の AI への窓口は、求職者向けの「求人の検索」だけ開いた。Indeed と ZipRecruiter は ChatGPT アプリを出した。Indeed は Claude 向けの MCP サーバーをベータで出した。応募はどれも自社のサイトに戻す。企業向けの API は、ATS の提携先にだけ開いている。
- 国内の大手(ビズリーチ、エン、パーソル、ディップ)は、求人票やスカウト文の生成、面接練習など、工程ごとの AI 機能が中心だった。国内の求人大手が ChatGPT アプリや MCP を出したのは、確かめた範囲では Indeed Japan だけだった。
- 企業の bot と求職者の bot が直接やり取りする仕組み(A2A)を出した大手は見つからなかった。Indeed の利用規約は「応募を企業かその Agentic AI に送る」と書いており、企業側のエージェントは想定し始めている。

## 比べる表

| 名前 | 対象 | AI とエージェントでしていること | 提供の段階 | 権限とデータの扱い | 出典 | 見た日 |
|---|---|---|---|---|---|---|
| Indeed Sourcing Assistant(Smart Sourcing の機能) | 企業向け | 自然言語で候補者像を受け、常に探して応募を誘う。送る文は採用担当が承認する | 一般提供(米国、Smart Sourcing の Professional と Enterprise) | Indeed の 3.7 億件の Sourceable Profiles を見る。ATS とは Indeed Apply の同期でつなぐ | https://www.indeed.com/news/releases/indeeds-ai-powered-sourcing-assistant-helps-employers-hire-over-30-faster?co=US | 2026-11-11 |
| Indeed Smart Screening(Smart Fit Score) | 企業向け | 企業の基準で応募者に 0〜100 の点を付け、要約を出す | 一般提供(提供範囲の一次情報なし) | 求職者が出した情報だけで採点し、他社データは使わない(会社の発表) | https://www.indeed.com/news/releases/introducing-indeeds-smart-fit-score?co=US | 2026-11-11 |
| Indeed Talent Scout | 企業向け | 会話型のエージェント。候補者の一覧、スカウト文の下書き、市場の情報 | 不明(米国のみ。段階の表示なし) | Premium Sponsored Jobs か Smart Sourcing が必要。Workable などの ATS からはパートナートークンでつなぐ | https://www.indeed.com/employers/talentscout | 2026-11-11 |
| Indeed Career Scout | 求職者向け | 求人の推薦、応募の事前入力、履歴書の調整、面接練習 | 一般提供(2025-09 の発表。2026 年の提供国は不明) | Indeed のプロフィールと会話の内容を使う | https://www.indeed.com/news/releases/indeed-introduces-new-suite-of-hiring-products-career-scout-talent-scout-premium-sponsored-jobs-and-indeed-connect?co=US | 2026-11-11 |
| Indeed Apply For Me | 求職者向け | プロフィールから応募の文面を下書きする | ベータ(米国の限定試験。自動応募は 2026-08-04 に停止) | 応募数の上限あり。使っていない人の応募は止める | https://www.indeed.com/news/releases/indeed-tests-apply-for-me-job-search?co=US | 2026-11-11 |
| Indeed アプリ(ChatGPT) | 求職者向け | ChatGPT の中で Indeed の求人を検索し、表示する | 一般提供(米国 2026-02-10、日本を含む 14 か国 2026-05-14) | Indeed のアカウントで連携する。詳細の確認と応募は Indeed で行う | https://d341ezm4iqaae0.cloudfront.net/press/sites/2/2026/05/14094032/20260514_uP5HZ.pdf | 2026-11-11 |
| Indeed MCP サーバー | 求職者向け | 求人の検索と詳細、本人の履歴書、企業の評判データを AI に渡す | ベータ(Claude のコネクタのみ) | Indeed のアカウントでログインする。OAuth の範囲の記載なし | https://docs.indeed.com/mcp | 2026-11-11 |
| Indeed PLUS AI アシスタント | 企業向け(国内) | 応募の状況を分析し、求人原稿の改善を提案する | ベータ(2026-09-07 から順次) | 企業の承認なしに原稿を変えない。匿名化した求職者データと他社の求人データを使う | https://jp.indeed.com/news/releases/20260907 | 2026-11-11 |
| リクルートエージェント AI 面接練習 | 求職者向け(国内) | 音声と映像で AI と面接を練習し、助言を受ける | 一般提供(会員は無料) | 結果は企業に渡さず、アドバイザーにも自動で連携しない | https://www.r-agent.com/guide/?p=38627 | 2026-11-11 |
| LinkedIn Hiring Assistant(2) | 企業向け | 要件のヒアリング、ソーシング、応募者の評価、音声やテキストの事前選考、日程調整 | 一般提供(英語は 2025-09。版 2 は順次展開中) | LinkedIn Recruiter の追加契約。LinkedIn と ATS の応募者を見る。指示した作業だけをする | https://business.linkedin.com/talent-solutions/hiring-assistant | 2026-11-11 |
| LinkedIn AI 求人検索、Job Match | 求職者向け | 自然な言葉で求人を探す。自分と求人の合い具合を示す | 一般提供(5 言語で世界に展開中) | 外部の AI 向けの窓口は見つからなかった | https://news.linkedin.com/2026/LinkedIn-Research-Talent-2026? | 2026-11-11 |
| ZipRecruiter ChatGPT アプリ | 求職者向け | ChatGPT の中で条件を伝え、求人を探す | 一般提供(2026-03-19) | 応募は ZipRecruiter で行う。データの扱いの記載なし | https://www.01net.it/ziprecruiter-launches-chatgpt-app-for-ai-powered-job-discovery/ | 2026-11-11 |
| ZipRecruiter 企業向け AI | 企業向け | 選考の質問を AI が提案する。ZipIntro で面談を組む | 一般提供 | ATS 連携 180 以上(Workday、Bullhorn を含む) | https://d18rn0p25nwr6d.cloudfront.net/CIK-0001617553/3f6efbcd-c86a-4295-a03c-b36dbbf4aa12.pdf | 2026-11-11 |
| ビズリーチ AI | 企業向けと求職者向け(国内) | 求人票の自動作成、スカウト文の調整、会員向けのキャリア相談 AI | 一般提供(相談 AI はアプリのみ) | 自社の転職データで学習した生成 AI。個人データの扱いの記載なし | https://www.bizreach.co.jp/pressroom/pressrelease/2026/0701.html | 2026-11-11 |
| エン PeopleX | 企業向け(国内) | PeopleX の AI 面接、AI 面談、AI ロープレを OEM で売る | 発表(2026-04-14)。自治体の導入の発表あり | 記載なし | https://prtimes.jp/main/html/rd/p/000001186.000000725.html | 2026-11-11 |
| ディップ(バイトル)面接コボット、dip AI エージェント | 企業向けと求職者向け(国内) | 応募者への自動連絡、日程調整、事前質問。求職者には対話で求人を提案 | 面接コボットは一般提供。AI エージェントは 2024 年の開始のみ確認 | 37 媒体の応募を取り込む(2024-02)。AI の使用は明示なし | https://www.baitoru.com/solution/?p=344 | 2026-11-11 |

## Indeed(Recruit Holdings の HR テクノロジー)

### 経営の方針(決算説明)

- 対象は企業向けが先。CEO の出木場氏は「過去 2〜3 年の AI 開発投資は企業向けの道具に集中した」と述べた（出典: https://file.recruit-holdings.com/files/en/Recruit_202603Q4_call-transcript_en.pdf、見た日 2026-11-11）。
- 理由は「採用は両方が yes と言う必要がある」から。求職者側のデータをいくら集めても、企業が採るかどうかは分からない、という説明だった（出典: 同上、見た日 2026-11-11）。
- キーワード検索から来る応募は 30% だけだった。残りの 70% は、AI の提案や、AI ソーシングと AI 選考のデータに基づくメールやポップアップから来る（出典: 同上、見た日 2026-11-11）。(会社の発表)
- 他社の自動応募は「効率を全く上げていない」と批判した。月額で 1,000〜2,000 件の応募を代行するスタートアップを例に挙げた（出典: 同上、見た日 2026-11-11）。
- Indeed 自身も自動応募を試している。ただし「お金を取って無差別に送ることは絶対にしない」と述べ、両方に合うときだけ送る仕組みを試すとした（出典: 同上、見た日 2026-11-11）。
- CEO は「AI の道具を本格的に売り始めたのは、この 1 年ほど」と述べた（出典: 同上、見た日 2026-11-11）。AI 製品だけの売上の数字は、この説明の中に見つからなかった。
- 2026-08-07 の Q1 説明では、米国の売上が前年比 30% 増えた。HR テクノロジーの通期の見通しを前年比 18.7% 増に上げた（出典: https://file.recruit-holdings.com/files/en/Recruit_202703Q1_call-transcript_en.pdf、見た日 2026-11-11）。
- 同じ説明で、医療の顧客の例を挙げた。「自動の AI リクルーター」が候補者に声をかけ、面接まで組む。顧客は「採用担当 X 人分」と評価する、という話だった（出典: 同上、見た日 2026-11-11）。
- 大企業は AI 製品の法務の審査に時間がかかる、とも述べた（出典: 同上、見た日 2026-11-11）。
- 内定、条件交渉、入社手続きの自動化を問われ、CEO は慎重に答えた。「多くの顧客のシステムと連携すると実行が大きく遅くなる」。まず候補者を届ける段の強化に集中する。そうしないと多くの FDE(顧客先に入る技術者)が要る、という説明だった（出典: 同上、見た日 2026-11-11）。

### 企業向け

- Sourcing Assistant は 2026-06-15 に発表された。Boolean 検索の代わりに自然言語で候補者像を伝える。常に候補者を探し、応募を誘う（出典: https://www.indeed.com/news/releases/indeeds-ai-powered-sourcing-assistant-helps-employers-hire-over-30-faster?co=US、見た日 2026-11-11）。
- 提供の段階は一般提供。米国の企業で、Smart Sourcing の Professional か Enterprise の契約が要る。他の市場は「近く」とだけ書いている（出典: 同上、見た日 2026-11-11）。
- 人の関与: 送る量は採用担当が決め、個別の文面は採用担当が承認する（出典: 同上、見た日 2026-11-11）。
- 効果の数字は会社の試験と自己申告だった。週 7 時間の節約は、ベータの 17 社の自己申告の中央値だった（出典: 同上、見た日 2026-11-11）。(会社の発表)
- Smart Screening は、企業の基準で応募者を並べる。Smart Fit Score は 0〜100 の点で、求職者が出した履歴書、質問への回答、勤務地だけを使う。他社データや他の候補者との比較は使わない（出典: https://www.indeed.com/news/releases/introducing-indeeds-smart-fit-score?co=US、見た日 2026-11-11）。(会社の発表)
- Talent Scout は会話型のエージェントとして 2025-09-10 に紹介された。候補者を探し、スカウト文を下書きする（出典: https://www.indeed.com/news/releases/indeed-introduces-new-suite-of-hiring-products-career-scout-talent-scout-premium-sponsored-jobs-and-indeed-connect?co=US、見た日 2026-11-11）。
- Talent Scout は今も米国の求人とアカウントだけで使える。候補者の全体を見るには Premium Sponsored Jobs か Smart Sourcing が要る（出典: https://www.indeed.com/employers/talentscout、見た日 2026-11-11）。
- 2026-09-04 の FutureWorks 2026 のまとめは、Sourcing Assistant と Smart Screening を挙げた。Talent Scout と Career Scout の名前は出てこなかった（出典: https://www.indeed.com/news/releases/indeed-futureworks-2026-recap?co=US、見た日 2026-11-11）。
- 推測: 「Scout」という名前のエージェントより、Smart Sourcing と Smart Screening の機能として売る形に重心が移った可能性がある。根拠は上の 2026 年の発表の並びだけで、会社はそう述べていない。
- AI の設計方針(2026-07-14): 採用の判断は人がする。AI の要約や点は、採用の判断の唯一の根拠にしない。企業は自動の道具を止められる（出典: https://www.indeed.com/news/releases/humans-in-the-loop-ai-hiring?co=US、見た日 2026-11-11）。

### 求職者向け

- Career Scout は Indeed アプリの中の AI のキャリアコーチ。求人の推薦、応募の事前入力、履歴書の調整、面接練習をする（出典: https://www.indeed.com/news/releases/indeed-introduces-new-suite-of-hiring-products-career-scout-talent-scout-premium-sponsored-jobs-and-indeed-connect?co=US、見た日 2026-11-11）。
- Apply For Me は 2026-07-07 に始めた限定試験。米国の一部の求職者だけが対象で、「早い段階の試験で、本格提供ではない」と書いている（出典: https://www.indeed.com/news/releases/indeed-tests-apply-for-me-job-search?co=US、見た日 2026-11-11）。
- 2026-08-04 の更新で、確認なしに送る自動のモードを止めた。今は下書きを本人が確かめてから送るモードに絞っている（出典: 同上、見た日 2026-11-11）。
- 応募数に上限があり、本人が使っていないと応募を止める（出典: 同上、見た日 2026-11-11）。

### 外部の AI との連携(ChatGPT アプリ、MCP)

- ChatGPT の Indeed アプリは、米国で 2026-02-10 に出た（出典: https://www.indeed.com/news/releases/indeed-launches-app-in-chatgpt?co=US、見た日 2026-11-11）。
- 日本では 2026-05-14 に出た。この時点で日本、英国、フランス、ドイツを含む 14 か国で使える（出典: https://d341ezm4iqaae0.cloudfront.net/press/sites/2/2026/05/14094032/20260514_uP5HZ.pdf、見た日 2026-11-11）。
- ChatGPT の中でできるのは求人の検索と閲覧だけ。詳細の確認と応募は Indeed で行う。使うには Indeed のアカウントでログインする（出典: 同上、見た日 2026-11-11）。
- 企業にとっての価値は「これまでどおり Indeed 上で応募を管理できる」こととされた（出典: 同上、見た日 2026-11-11）。
- MCP サーバーはベータで、Claude のコネクタでだけ使える。道具は 4 つ。求人の検索、求人の詳細、本人の履歴書の取得、企業データ(満足度、報酬、文化、評判)の取得（出典: https://docs.indeed.com/mcp、見た日 2026-11-11）。
- MCP のページに OAuth の範囲、回数の制限、データの保持の記載はなかった（出典: 同上、見た日 2026-11-11）。

### 外から使える API と、権限とデータの扱い

- 求人掲載: Job Sync API は ATS の提携先向けの GraphQL API。求人の作成、更新、終了、状態の確認ができる（出典: https://docs.indeed.com/job-sync-api、見た日 2026-11-11）。
- 応募: Indeed Apply は、Indeed と開発者契約を結んだ ATS の提携先が組み込む。応募は JSON で ATS に POST され、HMAC の署名を付ける。採否の結果は Disposition Sync で Indeed に返す（出典: https://docs.indeed.com/indeed-apply/ats、見た日 2026-11-11）。
- ATS 連携の数は 350 以上(会社の発表)（出典: https://www.indeed.com/news/releases/indeed-31-hires-per-minute-ai-matching?co=US、見た日 2026-11-11）。
- 利用規約(2026-09-29 更新)は「Agentic AI」を定義した。Indeed Apply で応募すると「Indeed は応募を企業かその Agentic AI に送る」と書いている（出典: https://www.indeed.com/legal、見た日 2026-11-11）。
- 同じ規約は、Indeed の公式のベンダーと道具以外の自動化、スクリプト、bot で Indeed Apply を自動化することを禁じている。サイトで知らせた後に 1 日の応募数を制限しうる、とも書いている（出典: 同上、見た日 2026-11-11）。
- 同じ規約は、Apply For Me による「Auto Apply」に企業への課金が起きうると書いている（出典: 同上、見た日 2026-11-11）。

## Recruit の国内の求人事業(Indeed Japan、リクナビ、タウンワーク、Airワーク、リクルートエージェント)

- 体制: Recruit の国内の人材事業は、Indeed リクルートパートナーズ(IRP)と Indeed リクルートテクノロジーズ(IRT)に分かれた。2 社は HR テクノロジーの下で一体で運営する（出典: https://jp.indeed.com/news/releases/20250212、見た日 2026-11-11）。
- リクルートの発表の一覧では、「しごと」の分類の発表は 2025-04 に Indeed Japan と IRP に移った（出典: https://www.recruit.co.jp/newsroom/pressrelease/、見た日 2026-11-11）。
- Indeed PLUS は、ATS に一度載せた求人を、Indeed のマッチングで連携する求人サイトに自動で載せる仕組み。2026-02 に最大 15 サイトに広がった（出典: https://jp.indeed.com/news/releases/20260216、見た日 2026-11-11）。
- Indeed PLUS はリクナビ、リクナビNEXT、タウンワークなどと連携している、と 2025-02 の発表は書いている（出典: https://jp.indeed.com/news/releases/20250212、見た日 2026-11-11）。
- Indeed PLUS AI アシスタントは 2026-09-07 にベータで始まった。応募の状況を分析し、原稿の改善を提案する（出典: https://jp.indeed.com/news/releases/20260907、見た日 2026-11-11）。
  - 対象: Indeed への直接投稿か Airワーク 採用管理を使う企業。国内の正社員、アルバイト・パート、契約社員のスポンサー求人。
  - 権限: 提案は 1 求人に週 1 回まで。企業の承認なしに原稿は変えない。
  - データ: 求職者の属性と行動、他社の求人のデータを、匿名化と統計の処理をして使う(会社の発表)。
- 決算説明では、国内の Q1 売上は前年比 6.7% 増だった。Indeed PLUS は想定を上回った（出典: https://file.recruit-holdings.com/files/en/Recruit_202703Q1_call-transcript_en.pdf、見た日 2026-11-11）。
- リクルートエージェントの「AI 面接練習」は、音声と映像で AI と練習する機能。会員は無料で使える（出典: https://www.r-agent.com/guide/?p=38627、見た日 2026-11-11）。
  - 練習の結果は企業に渡さず、キャリアアドバイザーにも自動で連携しない、と書いている(会社の説明)。
- リクナビ、リクナビNEXT、タウンワーク、Airワークの単独の AI 機能の一次情報は見つからなかった。

## Glassdoor

- Recruit は Glassdoor の運営を Indeed に統合すると、2025-07 に社内に伝えた。約 1,300 人の削減と同時だった（出典: https://www.thestar.com.my/tech/tech-news/2025/07/11/indeed-glassdoor-to-cut-1300-jobs-amid-ai-integration-memo-shows、見た日 2026-11-11）。(報道)
- CEO は社内の文書で「AI が世界を変えており、適応しなければならない」と書いた（出典: 同上、見た日 2026-11-11）。(報道)
- Indeed の MCP サーバーは、企業の満足度、報酬、文化、評判のデータを AI に渡す（出典: https://docs.indeed.com/mcp、見た日 2026-11-11）。
- 推測: Glassdoor 型の企業の評判データは、Indeed の窓口を通じて外部の AI に出ていく流れにある。MCP の企業データが Glassdoor 由来かどうかは、ページに書かれていない。
- Glassdoor 単独の AI 機能(対話型の求人検索など)の一次情報は開けなかった。

## LinkedIn

- 対象: 企業向け。Hiring Assistant は LinkedIn 初の採用担当向けの AI エージェント。2025-09 末に英語で世界に提供すると発表した（出典: https://news.linkedin.com/2025/hiring-assistant-globally-available、見た日 2026-11-11）。
- 今の製品ページは「Hiring Assistant 2」の展開を始めたと書く。できることは次のとおり（出典: https://business.linkedin.com/talent-solutions/hiring-assistant、見た日 2026-11-11）。
  - 要件のヒアリングと、好みの記憶
  - LinkedIn 上の複数の検索と、フィードバックからの学習
  - LinkedIn と ATS の応募者の評価
  - 文面の下書き、音声やテキストでの事前選考、面接の日程調整
- 提供の段階は一般提供。LinkedIn Recruiter の追加の契約で、7 言語に対応する（出典: 同上、見た日 2026-11-11）。
- 権限: 「指示した作業だけをする」と書き、支援する求人を選べる。ATS 連携は相手により異なる（出典: 同上、見た日 2026-11-11）。
- 中小企業向けには、Hiring Pro という AI エージェントが英語で世界に提供されている。AI 面接と会話型の画面を、今後数か月で出すとしている（出典: https://news.linkedin.com/2026/LinkedIn-Research-Talent-2026?、見た日 2026-11-11）。
- 求職者向け: AI の求人検索は、自然な言葉で探せる。毎日 130 万人以上が使い、5 言語で世界に展開中（出典: 同上、見た日 2026-11-11）。(会社の発表)
- Job Match は、自分と求人の合い具合を示す。米国の Premium 会員が「合わない」求人に応募する率を 10% 下げた（出典: 同上、見た日 2026-11-11）。(会社の発表)
- API: 求人掲載、Apply Connect、Apply with LinkedIn、CRM Connect、Recruiter System Connect がある（出典: https://learn.microsoft.com/en-us/linkedin/talent/、見た日 2026-11-11）。
- Apply Connect は「LinkedIn の提携先」が ATS から使う。LinkedIn 上の応募と、スキルの一致のデータを ATS に送る（出典: https://learn.microsoft.com/en-us/linkedin/talent/apply-connect/apply-connect-overview、見た日 2026-11-11）。
- 利用規約(2025-11-03 発効)は、bot など許可のない自動の手段でサービスを使うことを禁じている（出典: https://www.linkedin.com/legal/user-agreement、見た日 2026-11-11）。
- LinkedIn の ChatGPT アプリや MCP サーバーの一次情報は見つからなかった。

## ZipRecruiter

- 求職者向け: ChatGPT アプリを 2026-03-19 に出した。ChatGPT のアプリ一覧から「接続」し、@ziprecruiter で呼ぶ（出典: https://www.01net.it/ziprecruiter-launches-chatgpt-app-for-ai-powered-job-discovery/、見た日 2026-11-11）。(会社の発表の転載)
- 応募は「View Job Details」から ZipRecruiter で行う。データの扱いの記載はなかった（出典: 同上、見た日 2026-11-11）。
- 企業向け: Q4 2025 の株主への手紙によると、求人の掲載時に AI が選考の質問を提案する。新しい企業の 93% が使った（出典: https://d18rn0p25nwr6d.cloudfront.net/CIK-0001617553/3f6efbcd-c86a-4295-a03c-b36dbbf4aa12.pdf、見た日 2026-11-11）。(会社の発表)
- ZipIntro は AI で企業と求職者の面談を組む仕組み。ATS 連携は 180 以上で、Workday と Bullhorn が加わった（出典: 同上、見た日 2026-11-11）。
- 生成 AI の検索から来る求職者の訪問は、前年比で 2 倍を超えた（出典: 同上、見た日 2026-11-11）。(会社の発表)
- 対話型のキャリアアドバイザー「Phil」の公式ページは開けなかった(403)。

## ビズリーチ(Visional)

- 企業向け: 「ビズリーチ AI」の求人自動作成を 2025-04-23 に一般提供した。人材の要件と企業の URL から求人票を作る（出典: https://www.bizreach.co.jp/pressroom/pressrelease/2025/0423.html、見た日 2026-11-11）。
- 企業向け: スカウト文の AI 調整を 2025-10-22 に出した。求人と職務経歴書を読み、文案を出す。採用担当が確かめて直してから送る（出典: https://www.bizreach.co.jp/pressroom/pressrelease/2025/1022.html、見た日 2026-11-11）。
- 求職者向け: キャリア相談の AI を 2026-07-01 に出した。職務経歴を読み、強みや市場価値を対話で整理する。今はアプリだけで使える（出典: https://www.bizreach.co.jp/pressroom/pressrelease/2026/0701.html、見た日 2026-11-11）。
- データ: どれも自社の転職データで学習した生成 AI を使う。個人データの保存や学習への利用は書かれていなかった（出典: 同上、見た日 2026-11-11）。
- 新卒(ビズリーチ・キャンパス)では「就活×AI エージェント」の立ち上げのエンジニアを募集していた。求人は「AI エージェントを入口に様々なサービスを呼び出す未来」を仮説に掲げ、既存サービスへの脅威とも書いていた（出典: https://sincereed-agent.com/offer/bizreach-76/、見た日 2026-11-11）。募集は終了しており、掲載日はページで確かめられなかった。

## エン・ジャパン

- エンと PeopleX は 2026-04 に合弁会社「エン PeopleX」を作った。最初は PeopleX の AI 面接、AI 面談、AI ロープレを OEM で売る、としている（出典: https://prtimes.jp/main/html/rd/p/000001186.000000725.html、見た日 2026-11-11）。
- 同じ発表は、エンの既存の製品に AI 機能を組み込むとも書いた。提供の時期と料金はなかった（出典: 同上、見た日 2026-11-11）。
- エンの発表の一覧には、2026-08-04 に鎌倉市が「エン PeopleX AI 面接」を教員の採用に入れたという題がある（出典: https://corp.en-japan.com/newsrelease/、見た日 2026-11-11）。本文は開けなかった(404)。
- エン転職、engage の AI 機能の 2026 年の一次情報は見つからなかった。

## パーソルキャリア(doda、doda X)

- パーソルキャリアの発表のページは開けなかった(403)。
- doda と doda X の、求職者向けか企業向けの AI エージェントの一次情報は見つからなかった。
- 検索の結果には、社内で求人票を作る生成 AI のアプリの発表(2026-05-22)が出た。本文は開けず、確かめていない。

## ディップ(バイトル)

- 求職者向け: 「dip AI エージェント」は、バイトルのキャラクターと対話して求人の提案を受けるサービス。2024 年に始まった（出典: https://www.businessinsider.jp/article/287667/、見た日 2026-11-11）。(報道)
- 同じ記事によると、ディップは「マッチングの精度を上げた後に成果課金を入れる」ことを目標に掲げた。時期は未定だった（出典: 同上、見た日 2026-11-11）。(報道)
- 企業向け: 「面接コボット」は、応募者への SMS とメールの自動送信、日程調整、最大 6 問の事前質問をする（出典: https://www.baitoru.com/solution/?p=344、見た日 2026-11-11）。
  - 37 種類の求人媒体の応募を取り込み、まとめて管理できる(2024-02 時点)。
  - ページに AI を使うとの記載はなく、「チャットボット」と書いている。
- 「バイトルトーク」は、店長とアルバイトの業務連絡とシフト調整のアプリ。2026-10 の発表に AI の記載はなかった（出典: https://www.dip-net.co.jp/news/2194、見た日 2026-11-11）。
- dip AI エージェントの 2026 年の状態の一次情報は見つからなかった。

## 横断の論点: 大手は外部の AI に何を開いているか

| 窓口 | Indeed | LinkedIn | ZipRecruiter | 国内(Indeed 以外) |
|---|---|---|---|---|
| 求職者の AI からの求人検索 | ChatGPT アプリ(一般提供)、MCP(ベータ、Claude のみ) | 見つからなかった | ChatGPT アプリ(一般提供) | 見つからなかった |
| 求職者の AI からの応募 | 不可。自社のサイトに戻す。外部の自動化は規約で禁止 | 規約で bot を禁止 | 不可。自社のサイトに戻す | 見つからなかった |
| 企業の ATS からの求人掲載と応募の受け取り | Job Sync API、Indeed Apply(ATS の提携先のみ) | 求人掲載 API、Apply Connect(提携先のみ) | ATS 連携 180 以上(API の公開の一次情報は未確認) | Indeed PLUS 経由(ATS から配信) |
| 企業の AI エージェントの受け入れ | 規約に「企業かその Agentic AI に送る」 | 見つからなかった | 見つからなかった | 見つからなかった |

出典は各節の記載のとおり。

## このプロダクトへの示唆

中心の問い「大手は本当にまだ AI ネイティブでないのか」に、このファイルの範囲で答える。

### 確かめられた事実

- 大手は「AI がない」のではない。Indeed は応募の 70% を AI の提案から生み、AI のソーシングと選考を有料で売り、売上を伸ばしている(会社の発表)。
- ただし、大手のエージェントは自社の求人と自社の候補者の中で動く。Indeed の CEO は、内定から入社までの自動化を「多くの顧客のシステムと連携すると遅くなる」として後回しにした。
- 求職者が自分の AI に応募を任せることを、大手は規約で止めている。Indeed は自社の Apply For Me だけを例外にし、それも自動応募のモードを止めた。
- 外部の AI(ChatGPT、Claude)への窓口は、求人の検索に限られる。応募と企業とのやり取りは自社のサイトに戻す設計だった。
- 企業向けの API は ATS の提携先にだけ開いている。中小企業が自分の bot に権限を渡して管理させる入口は、大手の側には見つからなかった。
- 国内の大手は、求人票やスカウト文の生成、面接練習など、工程ごとの機能が中心だった。

### 推測

- 推測: 「AI ネイティブでない」というより、「自社のマーケットプレイスの中だけで AI ネイティブになろうとしている」が近い。大手の強みは両側のデータで、外部の bot に開くほど、そのデータと課金点(応募、スポンサー求人)が弱まる。
- 推測: このため、次の 3 つは大手が自分からは作りにくい。根拠は、上の CEO の発言と規約の書き方だけ。
  - 企業の中の人事データ全体に権限を持つ bot(大手は「候補者を届ける段」に集中すると述べた)
  - 企業が自然言語で自社の採用流程を設計する仕組み(大手の道具は、自社の求人と応募を前提にしている)
  - 複数の求人サイトをまたいで動く、求職者の側の bot(規約で外部の自動化を禁じている)
- 推測: 逆に、hiring-os が大手と正面から競うのは不利。Indeed は求人と応募者の量と、採否の結果のデータを持つ。hiring-os は、大手の Job Sync API や Indeed PLUS、Apply Connect の「外側」で、企業の ATS や社内の人事データに座る位置の方が、大手の方針とぶつかりにくい。
- 推測: A2A の相手として、大手は「企業側のエージェント」を先に受け入れる可能性がある。Indeed の規約がすでに「企業の Agentic AI」に応募を送ると書いているからだ。求職者側のエージェントは、規約の上で締め出されている。
- 推測: 求職者向けの「求職に関係するデータだけを見る」アシスタントは、大手の ChatGPT アプリや MCP と同じ求人の検索の窓口を使える。ただし応募の段で大手のサイトに戻されるので、応募の代行は大手の規約と衝突する。

### 確かめていないこと

- 大手が 2026-11 以降に応募の API や A2A を出すかどうかは分からない。Recruit の 2026 年度 Q2 の決算説明(2026-11)は、見た日までに見つからなかった。

## 見つからなかったこと

- Recruit Holdings の 2026 年度 Q2 の決算資料(2026-11 の発表見込み)。URL の形を推して開いたが 404 だった。
- Indeed の Talent Scout と Career Scout の、2026 年の提供の段階と提供国の一次情報。
- Indeed の ChatGPT アプリで OpenAI に渡すデータの一次情報。ヘルプセンターのページは 403 で開けなかった。
- Indeed の MCP サーバーと ChatGPT アプリの OAuth の範囲。
- Glassdoor 単独の 2026 年の AI 機能の一次情報(公式ブログは 403)。
- LinkedIn の ChatGPT アプリ、MCP サーバー、求職者向けの応募の代行。
- ZipRecruiter の Phil の現状(公式ページは 403)と、2026 年 Q3 の決算の内容。
- リクナビ、リクナビNEXT、タウンワーク、Airワーク 採用管理の、単独の AI 機能の一次情報。
- doda、doda X、マイナビ、エン転職、engage の AI 機能の 2026 年の一次情報(パーソルキャリアのページは 403)。
- dip AI エージェントの 2026 年の状態と、成果課金を入れたかどうか。
- タイミー、Google の求人検索と Gemini、OpenAI Jobs Platform の 2026 年の状態。調べたが一次情報に届かなかった。
- 国内の求人大手(Indeed Japan 以外)の ChatGPT アプリや MCP への対応。
- 調べものの途中で、この回の Web 検索の上限に達した。上の項目の一部は、検索を追加すれば見つかる可能性がある。
