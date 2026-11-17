# 出典の確かめ(15 件と追加の 3 件)

調べものを書き終えた後、出典から 15 件を選んで開き直し、書いた主張を支えているかを確かめた。開き直した日はすべて 2026-11-11。

## 選び方

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

## まとめ

- 15 件のうち 11 件は最初から支えていた。4 件は「一部」で、本文を直して「支えている」にした。#8 は最初「支えている」としたが、2 回目のレビューで「一部」と分かった。消した主張はない。
- 追加の 3 件(#16〜#18)は、すべて最初から支えていた。
- 選んだファイル: regulation.md(3 件)、market.md(3 件)、job-platforms.md(4 件)、ats.md(2 件)、ai-hiring-tools.md、general-assistants.md、a2a-and-permissions.md(各 1 件)。
- 確かめていないこと: この表の 18 件の外の主張は、各ファイルを書いた時に一度開いただけで、開き直していない。
