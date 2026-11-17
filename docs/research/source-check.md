# 出典の確かめ(33 件)

調べものを書き終えた後、出典を選んで開き直し、書いた主張を支えているかを確かめた。合わせて 33 件だ。#1〜#18 は初版の調べもの(2026-11-11 に開き直した)、#19〜#33 は第 2 版で足した 3 ファイル(integrations-company.md、integrations-seeker.md、business-model.md。2026-11-18 に開き直した)の分だ。

## 選び方(#1〜#15)

Goal の順に従って選んだ。7 つのファイルから選んでいる。

1. PRD が根拠に引く主張(大手の囲い、規約、権限の形、A2A)
2. `market.md` の数字
3. `regulation.md` の施行の日
4. 提供の段階

## 結果

判定は「支えている / 一部 / 支えていない」。直した後の判定は「支えている」か「消した」。

| # | URL | 主張(ファイルと節) | 最初の判定 | 直したこと | 直した後の判定 |
|---|---|---|---|---|---|
| 1 | https://www.mhlw.go.jp/stf/shoukaibosyuukubun.html | AI による自動処理かどうかに関わらず、選別、加工、連絡の差配をすれば職業紹介の許可が要る。面接を評価し「採用すべき人材」と付けて渡すのも当たる(regulation.md 1.2) | 支えている | なし。ページに「電子情報処理組織(人工知能関連技術(AI)を活用したものを含む。)により自動的に行われているかどうかに関わらず」と例 4-8 があった | 支えている |
| 2 | https://www.shugiin.go.jp/internet/itdb_gian.nsf/html/gian/keika/1DE26F2.htm | 個人情報保護法の改正法は 2026-04-07 に衆議院が受理し、衆議院で 2026-05-26、参議院で 2026-07-10 に可決、2026-07-17 に公布(令和 8 年法律第 56 号)(regulation.md 1.3) | 支えている | なし。ページは Shift_JIS で、最初の取得は文字化けした。文字コードを直して読み、議案名、各日付、法律番号 56 を確かめた | 支えている |
| 3 | https://digital-strategy.ec.europa.eu/en/news/ai-omnibus-enters-force | AI Omnibus は 2026-07-27 に発効。附属書 III の高リスクは 2027-12-02、附属書 I は 2028-08-02 から適用(regulation.md 2.2) | 支えている | なし | 支えている |
| 4 | https://www.mhlw.go.jp/content/11600000/001683019.pdf | 人材紹介の手数料収入は約 9,835 億円(前年度比 17.6% 増)。常用就職 1 件あたりの手数料は約 103 万円(10.9% 増)(market.md 1、2) | 支えている | なし。資料は令和 6 年度の速報(2026-03-31 公表)で、market.md も「速報」と書いている | 支えている |
| 5 | https://www.zenkyukyo.or.jp/wp/wp-content/uploads/2026/02/5dd7a287f9e2438e16a351103968ef83.pdf | 求人広告の市場は 6,661 億円(2024 年度)。新形態サービスの 3,938 億円は含まない(market.md 1) | 支えている | なし。推移の表の 7,267(2023 年度)も確かめた | 支えている |
| 6 | https://www.yano.co.jp/press-release/show/press_id/4264 | AI マッチング分は 2025 年度 8.4%、2026 年度 11.4%。2026 年度は普及が速く、大きな AI の規制がない場合の見込み(market.md 5) | 支えている | なし。注 2 に「法改正や制度改定等による大規模なAI規制が生じないことを前提」とあった | 支えている |
| 7 | https://file.recruit-holdings.com/files/en/Recruit_202603Q4_call-transcript_en.pdf | 過去 2〜3 年の AI 開発投資は企業向けの道具に集中した。キーワード検索から来る応募は 30% で、70% は AI の提案などから来る(job-platforms.md「経営の方針」) | 支えている | なし。Slide 08 と Slide 11 の発言で確かめた | 支えている |
| 8 | https://www.indeed.com/news/releases/indeed-tests-apply-for-me-job-search?co=US | Apply For Me は 2026-07-07 に始めた米国の限定試験。2026-08-04 に確認なしで送る自動のモードを止めた(job-platforms.md「求職者向け」) | 一部(2 回目のレビューで直した。最初は「支えている」と判定した) | 2026-07-07 は発表の日で、試験を始めた日はページにない(「In July, we shared that we were performing a limited test」)。job-platforms.md の本文を「2026-07-07 に発表した限定試験」に直した。「This remains an early test, not a full launch.」と 2026-08-04 の更新は確かめた | 支えている |
| 9 | https://docs.indeed.com/mcp | Indeed の MCP サーバーはベータで、Claude のコネクタでだけ使える。道具は求人の検索、詳細、本人の履歴書、企業データの 4 つ(job-platforms.md「外部の AI との連携」) | 支えている | なし | 支えている |
| 10 | https://www.indeed.com/legal | 利用規約(2026-09-29 更新)は「Agentic AI」を定義し、「応募を企業かその Agentic AI に送る」と書く。公式の道具以外での Indeed Apply の自動化を禁じ、1 日の応募数を制限できる(job-platforms.md「外から使える API」) | 一部 | 禁止の対象は「Indeed の公式のベンダーと道具以外」の自動化、スクリプト、bot だった。応募数の制限は「サイトで知らせた後に」と条件が付いていた。この 2 点を本文に合わせて直した | 支えている |
| 11 | https://www.ashbyhq.com/product-updates/mcp 、https://docs.ashbyhq.com/ashby-mcp-server-beta | Ashby MCP の「段階と日付は書かれていなかった」(ats.md「Ashby」) | 一部 | 元の出典(ashbyhq.com/ai)には段階がなかったが、別の一次情報で 2026-06-29 に全プランで公開ベータと分かった。ats.md の結論、表、本文、見つからなかったことを直し、ai-hiring-tools.md の記載とそろえた | 支えている |
| 12 | https://support.greenhouse.io/hc/en-us/articles/53944054829083-Greenhouse-MCP-security-FAQ | Greenhouse MCP は OAuth 2.0 と PKCE を使う。不採用や採用などの 5 つの操作は人がはっきり確認するまで動かない。添付の中身は返さない(ai-hiring-tools.md「ATS が AI に口を開け始めた」) | 支えている | なし。5 つは不採用、採用、候補者の統合、匿名化、利用者権限の一括取り消しだった | 支えている |
| 13 | https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities | Team と Enterprise の管理者がツールごとに「Always allow / Needs approval / Blocked」を選べ、個人は上書きできない。コネクタは本人の権限を引き継ぎ、Claude 側では狭めるだけ(general-assistants.md「Claude」) | 支えている | なし | 支えている |
| 14 | https://newsroom.workday.com/2026-10-13-Workday-Launches-Autopilot-Agents-That-Get-Real-Work-Done-Across-HR,-Finance,-and-IT | Talent Acquisition Agent の autopilot は早期導入の企業に提供中で、一般提供は 2027 年初めの予定。候補者への連絡は採用担当の承認が要る(ats.md「Workday Recruiting」) | 支えている | なし | 支えている |
| 15 | https://github.com/a2aproject/A2A/releases | A2A は v1.0.0 が 2026-03-12、v1.0.1 が 2026-05-28(a2a-and-permissions.md「A2A」) | 一部 | v1.0.1 の GitHub の公開は 2026-05-28 だが、変更履歴の見出しは 2026-05-26 だった。両方の日付を書くように直した(一覧表と本文) | 支えている |

## 追加の確かめ(2 回目のレビューの後、3 件)

2 回目のレビューが「PRD の確定の根拠なのに開き直していない」と挙げた 3 件を、同じ形で確かめた。開き直した日は 2026-11-11。

| # | URL | 主張(ファイルと節) | 最初の判定 | 直したこと | 直した後の判定 |
|---|---|---|---|---|---|
| 16 | https://docs.stripe.com/mcp.md | 2026-12 から、Stripe MCP は全権の秘密鍵と、印のない RAK を受けつけなくなる。移行の期限は 2026-11-30(stripe-modular-agentic.md「MCP サーバーの認証」。PRD の D10) | 支えている | なし。「2026 年 11 月 30 日までに移行を完了してください。12 月以降、Stripe MCP ではフルアクセスのシークレットキー、および Agent タグのない制限付き API キーの受け付けを停止します」とあった。使えない鍵には 401 を返す | 支えている |
| 17 | https://calcivilrights.ca.gov/2025/06/30/civil-rights-council-secures-approval-for-regulations-to-protect-against-employment-discrimination-related-to-artificial-intelligence/ | カリフォルニア州の規則は、自動判断のデータを含む雇用の記録を 4 年以上残す。2025-10-01 施行(regulation.md「3.1」。PRD の 5.3 節と U5) | 支えている | なし。「maintain employment records, including automated-decision data, for a minimum of four years」と「set to go into effect on October 1, 2025」があった。「agent」の定義の文言はこのページにない(regulation.md の記載のとおり) | 支えている |
| 18 | https://www.ppc.go.jp/files/pdf/190826_houdou.pdf 、https://www.ppc.go.jp/files/pdf/191204_houdou.pdf 、https://www.mhlw.go.jp/stf/kaiken/daijin/0000194708_00148.html | リクナビ DMP フォロー: 2019-08-26 に勧告と指導(7,983 人)、2019-12-04 に改めて勧告(合わせて 26,060 人、「法の趣旨を潜脱した」)と利用企業への指導。2019-09-06 に東京労働局が職業安定法に基づく指導(risks.md「リクナビ DMP フォロー」。PRD の D6) | 支えている | なし。PDF は文字を取り出して、日付(令和元年 8 月 26 日、12 月 4 日)、人数、「人生をも左右しうる」「潜脱」、サービスの廃止を確かめた。会見の記録で、9 月 6 日の指導と「職業紹介にあたるもの」の発言を確かめた | 支えている |

## 新しい 3 ファイルの確かめ(#19〜#33)

integrations-company.md、integrations-seeker.md、business-model.md から 15 件を選んだ。PRD が根拠に引く主張、料金と法の区分、OS の決まりの順に選び、開き直した日はすべて 2026-11-18。

| # | URL | 主張(ファイルと節) | 最初の判定 | 直したこと | 直した後の判定 |
|---|---|---|---|---|---|
| 19 | https://www.apideck.com/integrations/country/japan/hris.md | Apideck は SmartHR、KING OF TIME、freee人事労務、ジョブカンなど国内のサービスを「まだ対応していない」と明記(integrations-company.md「結論」「Apideck」「統合 API の範囲、粗さ、料金の形」「このプロダクトへの示唆」。PRD の 4.3 節と U15) | 支えている | なし。見出し「Notable local systems not yet supported」の下に、SmartHR、KING OF TIME、freee HR、Money Forward Cloud Payroll、Jobcan、jinjer、COMPANY があった。対応は Workday など 7 つ | 支えている |
| 20 | https://www.indeed.com/legal | 利用規約(2026-09-29 更新)の D.21 が「AI or Agentic AI」を含む自動のシステムでのアクセスとデータの採掘を禁じる。D.22(4) の Permitted AI Connector(integrations-company.md「結論」「規約の問題」「このプロダクトへの示唆」。PRD の 1.4 節、4.3 節、D15) | 支えている | なし。「Last Updated: September 29, 2026」。Section D の 21「Site Rules」に「Use any automated system (bots, scrapers, spiders, AI or Agentic AI) to access, data-mine」があった。22 の 4 つ目「Third Party Automations」に「Permitted AI Connector」「is in Beta」「suspend or terminate access at any time」があった | 支えている |
| 21 | https://smarthr.jp/terms/terms-smarthr/ | 利用規約(最終改定 2026-05-26)の第 12 条 14 号がスクレイピングを禁じる。第 10 条の 2 はスクリプトや bot での AI 機能へのアクセスを禁じる。第 17 条は API 連携サービスの結果を利用ユーザーの責任とする(integrations-company.md「結論」「規約の問題」「このプロダクトへの示唆」。PRD の 1.4 節、4.3 節、D15) | 支えている | なし。変更履歴の最後は「2026年05月26日改定」。第 12 条の 14 番目の号が「スクレイピング等、手段を問わず、本サービスの仕様若しくは情報、又は他のユーザーの情報を収集する行為」。第 10 条の 2 に「自動化された手段(スクリプト、ボット等)を用いてAI機能にアクセスし」、第 17 条に「全ての結果について自ら責任を負う」があった | 支えている |
| 22 | https://apidocs.hibob.com/docs/hibob-mcp-server | HiBob は 2026-11-09 から、サービス用の利用者での MCP の新しい接続を止めた。今の接続も今後止まりうる(integrations-company.md「結論」「HiBob」「このプロダクトへの示唆」。PRD の 4.1 節) | 支えている | なし。「As of November 9, 2026, new service user connections are blocked.」と、今の接続は「will keep working for now」、サービス用の利用者は「will stop being supported in the future」があった | 支えている |
| 23 | https://docs.indeed.com/indeed-apply/ats 、https://docs.indeed.com/legal-terms/additional-api-terms-and-guidelines | Indeed Apply は ATS の提携先向けで、開発者契約が要る。統合は約 6 週間。追加の API 規約は API の許可を Indeed の裁量とする(integrations-company.md「結論」「比べる表」「Indeed」「このプロダクトへの示唆」) | 支えている | なし。「This guide is for applicant tracking system (ATS) partners.」、前提に「A signed Developer Agreement」、「Integrations usually take about six weeks」があった。規約に「entirely in Indeed's sole discretion」「may restrict or terminate your API access or API Key at any time」があった | 支えている |
| 24 | https://slack.com/terms-of-service/api 、https://docs.slack.dev/changelog/2025/05/29/rate-limit-changes-for-non-marketplace-apps | Slack は Marketplace 外の商用アプリの履歴の取得を 1 分 1 回・15 件に絞った(2025-05-29 以降)。API の規約(発効 2025-10-10)は LLM の学習と一括の書き出しを禁じる(integrations-company.md「結論」「比べる表」「Slack」「このプロダクトへの示唆」。PRD の 1.4 節、4.3 節) | 支えている | なし。変更履歴に「limited to 1 request per minute」と `limit` の上限「15 objects」、対象は 2025-05-29 以降に作ったアプリと新しいインストールとあった。規約は「発効日 : 2025 年 10 月 10 日」。組織の外に出すアプリの禁止に「API データを使用して大規模言語モデルをトレーニングすること」と「一括でエクスポートすること」があった | 支えている |
| 25 | https://raw.githubusercontent.com/apple/device-management/release/mdm/profiles/com.apple.TCC.configuration-profile-policy.yaml | macOS の構成プロファイルは画面の収録(ScreenCapture)の許可を与えられず、拒否だけができる(integrations-company.md「結論」「端末の管理(macOS)」「このプロダクトへの示唆」。PRD の 4.3 節) | 支えている | なし。ScreenCapture に「A profile can't grant access to the contents; it can only deny it.」があった。`AllowStandardUserToSetSystemService` は ListenEvent と ScreenCapture だけに効く | 支えている |
| 26 | https://developers.google.com/identity/protocols/oauth2/production-readiness/restricted-scope-verification 、https://developers.google.com/workspace/gmail/api/auth/scopes | restricted のデータをサーバーに保存か送信するなら、第三者のセキュリティ評価を 12 か月ごとに受ける。gmail.readonly と gmail.metadata は restricted、gmail.send は sensitive(integrations-company.md「結論」「比べる表」「Gmail(Google Workspace)」「このプロダクトへの示唆」、integrations-seeker.md「結論」「比べる表」「4. メールの API」。PRD の 4.3 節、5.3 節) | 一部 | 評価の条件(「If you store or transmit restricted scope data on servers」)、「at least every 12 months」、scope の区分は合っていた。ただし seeker の結論の「本文を読む scope がすべて restricted」は誤り。`gmail.addons.current.message.readonly`(「View your email messages when the add-on is running.」)は Sensitive の欄にあった。seeker の結論と比べる表、company の結論を「本文を広く読む scope(gmail.readonly など)は restricted」に直した。「年 1 回」の書き方も「12 か月ごと」にそろえた(seeker の結論、company の比べる表と示唆) | 支えている |
| 27 | https://support.google.com/googleplay/android-developer/answer/10964491?hl=en | Google Play は AccessibilityService で自律で計画して動く使い方を禁じ、アシスタントはアクセシビリティの道具に当たらない(integrations-seeker.md「結論」「比べる表」「Google Play」「作れない道」。PRD の 1.4 節、4.3 節、D15) | 支えている | なし。「Any use of the Accessibility API that enables an app to autonomously initiate, plan, and execute actions or decisions is strictly prohibited.」と、当たらない例に「automation tools, assistants」があった。認められたアクセシビリティの道具は例外 | 支えている |
| 28 | https://support.google.com/googleplay/android-developer/answer/9888170?hl=en | Google Play は SMS と通話履歴の権限を既定の SMS、電話、アシスタントのアプリに限る(integrations-seeker.md「結論」「比べる表」「Google Play」「作れない道」。PRD の 1.4 節、4.3 節) | 一部 | 通話履歴は「default Phone or Assistant handler」、SMS は「default SMS or Assistant handler」で、権限ごとに違った。seeker の結論の「SMS と通話履歴は既定の SMS かアシスタントのアプリに限る」は通話履歴の分が誤り。結論と「Google Play」の節を権限ごとに分けて書き直した | 支えている |
| 29 | https://developer.android.com/ai/appfunctions | 他社の AppFunctions を呼ぶ権限は、認められたシステムのアシスタントだけに与える(integrations-seeker.md「結論」「比べる表」「2. Android」の「ほかのアプリの中身」「作れない道」。PRD の 4.3 節、6 節) | 支えている | なし。FAQ に「requires the privileged EXECUTE_APP_FUNCTIONS permission, which Android grants only to authorized system assistants」があった。「Experimental」の表示と Android 16 以上も確かめた | 支えている |
| 30 | https://www.mhlw.go.jp/content/001328411.pdf | 募集情報等提供の成果報酬型の料金徴収は禁止されていない。2025-04-01 から求職者への金銭等の提供は原則禁止。料金と違約金の事前の明示(business-model.md「結論」「1. 収益の形ごとの実例」「2. 収益の形と職業安定法の区分」「どの案でも先に決めること」。PRD の U4) | 一部 | PDF の文字を取り出して読んだ。「成果報酬型の料金徴収を禁止したものではありません」、「令和７年４月１日から」、ポイントも「原則禁止の対象」、例外の「500円程度の電子ギフト券」があった。ただし結論の「採用の報告を集めるために求職者へお金やギフト券を渡すことは原則禁止」は目的を狭めていた。資料は「様々な趣旨・目的・態様で行われている労働者への金銭等の提供」を対象とする。「結論」を「目的を問わず原則禁止」に直した。明示の方法も、資料は「書面または電子メールその他の適切な方法」だった。「どの案でも先に決めること」の「書面か電子メールで」を「書面か電子メールなど企業が読み返せる方法で」に直した | 支えている |
| 31 | https://www.mhlw.go.jp/content/001250191.pdf | Q&A 問 5-1(応募に関係ないシステム利用料は第 43 条の 3 で禁止されない)、問 9-1(応募時に雇用契約が成立するサービスは職業紹介)、問 9-2、問 9-6、問 1-6(business-model.md「結論」「2. 収益の形と職業安定法の区分」「このプロダクトへの示唆」。PRD の U4) | 支えている | なし。PDF の文字を取り出して読んだ。問 5-1 に「応募に関係なくシステム利用料や登録料として料金を徴収することは同条で禁止されるものではありません」。問 9-1 に「応募・連絡した時点で原則として雇用契約が成立するようなサービス」。問 9-2 に看護師資格の例。問 9-6 に「採用可能性が高いと思われる求職者の連絡を当該者の判断により優先的に求人企業に届ける」。問 1-6 に「メールアドレス、サイトの閲覧履歴」があった | 支えている |
| 32 | https://www.baitoru.com/solution/?p=344 | 面接コボットは 1 か月 30,000 円、12 か月 180,000 円(税抜)、月の応募 999 件まで(business-model.md「結論」「比べる表」「1. 収益の形ごとの実例」「このプロダクトへの示唆」。PRD の H18、U4) | 支えている | なし。料金の表(税抜)に 1 か月 30,000 円、3 か月 75,000 円、6 か月 120,000 円、12 か月 180,000 円があった。表は月の応募 999 件までのプランで、1,000 件以上は別のプランで相談 | 支えている |
| 33 | https://www.merge.dev/pricing 、https://www.tryfinch.com/pricing | Merge は月 650 ドルで 10 接続まで(3 つ無料、超過 1 接続 65 ドル)。Finch の Starter は 1 接続につき月 65 ドル、15 接続まで(business-model.md「結論」「比べる表」「1. 収益の形ごとの実例」、integrations-company.md「比べる表」「Merge」「Finch」「統合 API の範囲、粗さ、料金の形」「このプロダクトへの示唆」。PRD の 4.3 節、U4) | 一部 | 金額は合っていた。Merge は「Link 3 production Linked Accounts for free」「Pay $650/month for up to 10 total production Linked Accounts. $65 per Linked Account after.」、Finch は「$65/month per connection」「Up to 15 connections」だった。ただし integrations-company.md は Merge の Linked Account を「社」と書き、料金の形を「顧客の数で払う(Merge、Finch、Apideck、Kombo)」とまとめていた。ページが数えるのは接続で、会社の数ではない。比べる表、「Merge」の節、「統合 API の範囲、粗さ、料金の形」の表と本文、「このプロダクトへの示唆」を「接続」に直した。Apideck と Kombo は顧客の数のまま | 支えている |

## まとめ

- 33 件のうち、最初から支えていたのは 25 件だった。8 件は「一部」で、本文を直して「支えている」にした。消した主張はない。
- #1〜#15: 11 件は最初から支えていた。4 件は「一部」で、本文を直して「支えている」にした。#8 は最初「支えている」としたが、2 回目のレビューで「一部」と分かった。
- #16〜#18(追加の 3 件): すべて最初から支えていた。
- #19〜#33(新しい 3 ファイル): 11 件は最初から支えていた。4 件(#26、#28、#30、#33)は「一部」で、本文を直して「支えている」にした。
  - #26: Gmail の本文を読む scope のうち、アドオンの scope は sensitive だった。「本文を広く読む scope は restricted」に直した。
  - #28: 通話履歴の条件は既定の電話かアシスタントで、SMS とは違った。権限ごとに分けて書いた。
  - #30: 求職者への金銭等の提供の禁止は、目的を問わない。目的を狭めた書き方を直した。
  - #33: Merge の料金が数えるのは接続で、会社の数ではない。「接続」に直した。
- 選んだファイル(#1〜#18): regulation.md(4 件)、market.md(3 件)、job-platforms.md(4 件)、ats.md(2 件)、ai-hiring-tools.md、general-assistants.md、a2a-and-permissions.md、stripe-modular-agentic.md、risks.md(各 1 件)。
- 選んだファイル(#19〜#33): integrations-company.md(9 件、うち #26 と #33 は他のファイルと共通)、integrations-seeker.md(4 件)、business-model.md(4 件)。
- 確かめていないこと: この表の 33 件の外の主張は、各ファイルを書いた時に一度開いただけで、開き直していない。
