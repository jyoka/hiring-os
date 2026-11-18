# 導入と成果を売る型: 同じ型、近い型、うまくいかなかった型(2026-11 時点)

数字の単位は、断りがなければ百万ドル。見た日はすべて 2026-11-18。SEC の数字は、書類の本文か、SEC の XBRL の API(書類の数字を機械で読める形にしたもの)で確かめた。

## 運営者の考えの確かめ

運営者が 2026-11-18 に話したことを、文ごとに分けた。1 文に事実と規範が混ざるものは、行を分けた。

| 番号 | 文 | 種類 | 判定 | 根拠 |
|---|---|---|---|---|
| 1a | Palantir の最新の年次の売上と年次報告を、よく見るべきだ | 規範の文 | - | 規範の文。事実で確かめる対象でない。palantir-implications.md で答える |
| 1b | (1a の前提) Palantir に最新の年次の売上と年次報告がある | 事実の文 | 合っている | 最新の年次報告は FY2025 の 10-K(2026-02-17 提出)。FY2025 の売上 4,475.4、GAAP の純利益 1,625.0。最新の四半期は Q3 2026(売上 2,313.4、GAAP の純利益 1,128.0)。出典: https://www.sec.gov/Archives/edgar/data/1321655/000132165526000011/pltr-20251231.htm と https://www.sec.gov/Archives/edgar/data/1321655/000132165526000045/a2026q3ex991pressrelease.htm (見た日 2026-11-18)。節「1. Palantir(基準)」 |
| 1c | 創業者の AI の未来への見立てと予測も含めて、学べることが多い | 規範の文 | - | 規範の文。事実で確かめる対象でない。palantir-implications.md で答える。なお CEO の手紙が四半期ごとに出ていることは、Q3 2026 の決算の発表で確かめた(「CEO Letter」の項)。手紙の中身は、このファイルでは確かめていない |
| 2a | AI の時代の製品は、もう広く使う製品として売るものではない | 事実の文 | 合っていない | Anthropic の S-1/A は、Claude の広がりの多くを「organic」と書く。直近 12 か月の売上の 26% は、各 10 万ドル未満の約 4,000 万の顧客から来た。Salesforce、Intercom などは公開の料金で広く売る。一方で、大口(10 万ドル以上)が売上の 74% で、各社は導入の部隊を増やしている。出典: https://www.sec.gov/Archives/edgar/data/2130357/000162828026072484/anthropicpbc-sx1ax2.htm (見た日 2026-11-18)。節 4、節 5 |
| 2b | サービスを売ることの方が大事だ | 規範の文 | - | 規範の文。事実で確かめる対象でない。palantir-implications.md で答える |
| 2c | この事業の形(サービスを売る形)はとても古く、SaaS よりずっと古い | 事実の文 | 合っている | EDS は 1962 年の創業で、Frito-Lay の計算の仕事を月額で請け負った。SaaS の前身の ASP は 1990 年代。SaaS という語の早い例は SIIA の 2001-02 の文書とされる(本文は開けなかった)。出典: https://hpalumni.org/edsHistoryCulture 、https://www.cio.com/article/272086/web-services-software-as-a-service-saas-definition-and-solutions.html (見た日 2026-11-18)。節 6 |
| 3a | AI の見立てで利益が出ることを続けて示している会社は、Palantir だけだ | 事実の文 | 一部合っている | 数え方で変わる。AI のモデルとエージェントを主に売る会社、上場の「AI プラットフォーム」の会社(C3.ai、SoundHound、BigBear.ai)に限ると、GAAP の黒字を続ける会社は見つからず、Palantir だけだ。AI 向けのデータのサービスの Innodata は、FY2024、FY2025、2026 の各四半期で GAAP の純利益が黒字。AI の基盤の Nvidia、AI の広告の AppLovin も黒字。節 4「反例」 |
| 3b | ほかの AI のモデルの会社は、投資を続けても回収が見えず、お金を失い続けている | 事実の文 | 一部合っている | 損失は合う。Anthropic は FY2025 の GAAP の純損失 41,965、OpenAI は 2025 年の純損失 約 38,530(報道)。ただし「回収が見えない」は一部合わない。Anthropic は Q2 2026 に GAAP の営業利益 974 を出した(Q3 2026 は営業損失 567)。SpaceX の SI 部門(Grok、Cursor、X を含む)は Q3 2026 に部門の営業利益 431。節 4 |
| 3c | AI エージェントの会社は、投資を続けても回収が見えず、お金を失い続けている | 事実の文 | 一部合っている | 上場の会社は合う。C3.ai は創業の 2009 年から毎期の純損失を 10-K に書く。SoundHound、BigBear.ai も純損失が続く。非上場の Sierra、Decagon は損益を出しておらず、不明。節 3、節 4 |
| 3d | 事業の形がうまく働いていないからだと思う | 事実の文(因果の推測) | 一部合っている | 支える部分: 費用が売上を上回る。Anthropic の計算資源の費用は FY2025 に売上の 160%。OpenAI の 2025 年の研究開発費 19,180 は売上 13,070 を上回る(報道)。支えない部分: 純損失の大部分は、転換社債などの評価の変動という現金の出ない費用だ(Anthropic の FY2025 は 34,308)。Palantir 自身も同じ型で、2003 年の創業から Q4 2022 まで黒字の四半期がなかった(会社の発表)。導入を先に売る C3.ai も赤字だ。Anthropic は、製品が自然に広がる形で営業損失を縮めた。「売り方が原因」を示す一次情報は見つからなかった。節 1、節 3、節 4 |
| 4a | だから Palantir は良い手本だ | 規範の文 | - | 規範の文。事実で確かめる対象でない。palantir-implications.md で答える |
| 4b | Prototype Studio も AI ネイティブな hiring OS も、Palantir の型を考えに入れる必要がある | 規範の文 | - | 規範の文。事実で確かめる対象でない。palantir-implications.md で答える |
| 5a | 会社としてすでにいろいろな SaaS を持っているなら、製品に AI エージェントを組み込める | 事実の文 | 合っている | 他社の例がある。Salesforce は Agentforce を既存の製品に組み込み、Workday と ServiceNow も AI エージェントを既存の契約に足した。出典: https://www.salesforce.com/agentforce/pricing/ 、https://blog.workday.com/en-us/introducing-workday-flex-credits-smarter-more-flexible-way-access-ai-innovation.html (見た日 2026-11-18)。節 5 |
| 5b | (SaaS を持つ会社は) AI ネイティブな製品もたくさん作れる | 事実の文(見込みを含む) | 一部合っている | 「作れる」は他社の例が支える。既存の顧客対応の SaaS を持つ Intercom は、AI エージェントの Fin を成果ごとの別の料金で売り、ほかの会社の道具とも使えるようにした。出典: https://fin.ai/pricing (見た日 2026-11-18)。節 2「Intercom(Fin)」。「たくさん」と、運営者の会社の力は、外の資料では確かめられない |
| 5c | この新しい Palantir の型 | 事実の文 | 一部合っている | 型そのものは新しくない。Palantir の創業は 2003 年で、FY2020 の 10-K は forward deployed engineers(FDE)を書く。新しいのは、AI のモデルの会社が FDE を取り入れたこと(OpenAI、Anthropic、Cohere の 2026 年の求人)。出典: https://www.sec.gov/Archives/edgar/data/1321655/000119312521060650/d65934d10k.htm (見た日 2026-11-18)。節 1、節 2 |
| 5d | この型を、比べる相手として、AI の機能の代わりの道として持っておく必要がある | 規範の文 | - | 規範の文。事実で確かめる対象でない。palantir-implications.md で答える |

## 結論

- Palantir の GAAP の黒字は確かだ。純利益は Q4 2022(30.9)から 16 四半期続けて黒字で、年では FY2023(209.8)が初めて。FY2025 は 1,625.0、Q3 2026 は 1,128.0。会社は Q4 2022 を「First Quarter of Positive GAAP Net Income」と書く。創業の 2003 年から約 20 年、黒字の四半期がなかったことになる(FY2020 は -1,166.4)。
- 「黒字を続けるのは Palantir だけ」は、数え方で答えが変わる。AI のモデル、エージェント、AI プラットフォームを主に売る会社では、ほかに見つからなかった。AI 向けのデータのサービスの Innodata、AI の基盤の Nvidia、AI の広告の AppLovin は黒字だ。
- AI のモデルの会社は大きな損失を出している。Anthropic(S-1/A、GAAP)は FY2025 に純損失 41,965、2026 年 1〜9 月に 104,039。OpenAI(報道)は 2025 年に純損失 約 38,530。ただし純損失の多くは、評価の変動などの現金の出ない費用だ。営業の段階では Anthropic が Q2 2026 に黒字(974)を出し、Q3 2026 に赤字(567)へ戻った。
- 損失の主な中身は、計算資源と研究開発だ。Anthropic の計算資源の費用は、売上に対して FY2024 に 653%、FY2025 に 160%、2026 年 1〜9 月に 57%。損失の原因を「売り方」に結びつける一次情報は見つからなかった。
- FDE の型は AI のモデルの会社に広がった。OpenAI、Anthropic、Cohere、Scale AI が 2026 年に FDE を募集している。Anthropic は S-1/A で、FDE を含む Applied AI の部隊を説明する。ただし同じ書類は、広がりの多くが「organic」で、大きな営業の組織によらないと書く。
- 「サービスをソフトウェアのように売る」形は、主に料金の形として広がった。Intercom Fin は 1 件 0.99 ドルの成果課金、Zendesk は自動で解決した件の課金、Sierra は成果課金だ。一方で Decagon は、多くの顧客が会話ごとの課金を選ぶと書く。Salesforce は会話ごと(2 ドル)、アクションごと(0.10 ドル)、席数(月 125 ドルから)を並べて売る。
- 同じ「導入を先に売る」型でも失敗はある。C3.ai は最大 6 か月の有料の導入の段階を置くが、創業から毎期赤字で、FY2026 の売上は前年から 35.7% 減った。Builder.ai は「AI で作る」と売り、2025 年に破綻した(報道)。IBM は Watson Health の資産を 2022 年に売った。
- 席数の課金は揺らいでいる、と大きな SaaS の会社自身が書く。Salesforce の FY2026 の 10-K は「顧客の利用者数の減り」と「使用量の課金の広がり」を解約の要因に挙げる。Accenture の FY2026 の 10-K は、AI に合った新しい料金の形を顧客が受け入れなければ業績が悪くなる、と書く。
- 推測: Palantir の型の利益は、型そのものより、長い赤字の期間を耐えた後の規模と、売上原価の低さから来ているように見える。型を写すなら、導入の段階の赤字をどこまで許すかを先に決める必要がある。

## 比べる表

| 会社 | 型 | 売るもの | 売り方 | 料金の形 | 売上と損益(期、区分) | 出典 | 見た日 |
|---|---|---|---|---|---|---|---|
| Palantir | 基準(FDE の型の元) | データと AI の基盤(Foundry、AIP)と導入 | FDE。無料か安い試行(bootcamp を含む)から広げる | サブスクリプション、専門のサービス | FY2025: 売上 4,475.4、純利益 1,625.0(GAAP)。Q3 2026: 売上 2,313.4、純利益 1,128.0(GAAP) | https://www.sec.gov/Archives/edgar/data/1321655/000132165526000011/pltr-20251231.htm | 2026-11-18 |
| OpenAI | 同じ型・近い型 | モデル、ChatGPT、API | FDE の部隊(Forward Deployed Engineering)。多くは自社のサイトと API | 個人と企業の定額、API の使用量 | 2025 年: 売上 13,070、営業損失 20,920、純損失 約 38,530(報道)。Q1 2026: 売上 5,700、営業損失 9,300(報道) | https://analyticsindiamag.com/ai-news/openai-spent-34-billion-in-2025-report | 2026-11-18 |
| Anthropic | 同じ型・近い型 | モデル(Claude)、API、アプリ | 製品が自然に広がる形が主。FDE を含む Applied AI の部隊と営業が深める | API の使用量、定額 | FY2025: 売上 4,585、営業損失 8,060、純損失 41,965(GAAP)。2026 年 1〜9 月: 売上 33,242、営業損失 1,260、純損失 104,039(GAAP) | https://www.sec.gov/Archives/edgar/data/2130357/000162828026072484/anthropicpbc-sx1ax2.htm | 2026-11-18 |
| Cohere | 同じ型・近い型 | 企業向けのモデルと North(AI の作業の場) | FDE を多く募集(北米、欧州、韓国、中東、公共) | 公開の料金は確かめていない | 年換算の売上(run-rate) 150(2025-10、会社の CEO の発言の報道)。損益は非公開 | https://thelogic.co/briefing/gomez-says-cohere-on-path-to-profitability-as-it-targets-ipo-soon/ | 2026-11-18 |
| Scale AI | 同じ型・近い型 | AI のデータと AI エージェントの開発 | FDE、Forward Deployed の製品の担当を募集 | 確かめていない | 確かめていない | https://job-boards.greenhouse.io/scaleai/jobs/4694861005 | 2026-11-18 |
| Sierra | サービスをソフトウェアのように売る | 顧客対応の AI エージェント | Agent PM が顧客と一緒にエージェントを作る | 成果課金が主。会話ごとの課金も混ぜる | 年換算の売上(ARR) 100(2025-11、会社の発表の報道)。損益は非公開 | https://sierra.ai/blog/outcome-based-pricing-for-ai-agents | 2026-11-18 |
| Decagon | サービスをソフトウェアのように売る | 顧客対応の AI エージェント | Agent PM が経営層と一緒に導入する | 会話ごと、または解決ごと。多くは会話ごとを選ぶ | 非公開 | https://decagon.ai/blog/pricing-ai-agents | 2026-11-18 |
| Intercom(Fin) | サービスをソフトウェアのように売る | 顧客対応の AI エージェント | 自社のサイトで売る | 1 成果 0.99 ドル。ほかの道具と使う場合は月 50 成果の最低。Intercom の helpdesk と使う場合は席が別 | 非公開(調べていない) | https://fin.ai/pricing | 2026-11-18 |
| Zendesk | サービスをソフトウェアのように売る | 顧客対応の道具と AI エージェント | 既存の契約に足す | AI が自分で解決した件だけ課金(2024-08 から) | 非公開(2022 年に非上場化。調べていない) | https://zendesk.co.uk/newsroom/articles/zendesk-outcome-based-pricing | 2026-11-18 |
| Salesforce | サービスをソフトウェアのように売る(既存の SaaS) | CRM と Agentforce | 既存の顧客に足す | 席数、会話ごと 2 ドル、アクションごと 0.10 ドル | FY2026(2026-01 まで): 売上 41,525、純利益 7,457(GAAP) | https://www.sec.gov/Archives/edgar/data/1108524/000110852426000060/crm-20260131.htm | 2026-11-18 |
| Accenture | サービスをソフトウェアのように売る(古い型の代表) | IT のサービス、コンサル、AI の導入 | 人が客先で作る | 人月、成果の指標に結びつく契約も多い | FY2026(2026-08 まで): 売上 74,183、純利益 8,367(GAAP) | https://www.sec.gov/Archives/edgar/data/1467373/000146737326000049/acn-20260831.htm | 2026-11-18 |
| Innodata | サービスをソフトウェアのように売る(AI 向けのデータのサービス) | AI の学習と評価のデータの作業 | 大きな AI の会社に人と道具で納める | 確かめていない | FY2025: 売上 251.7、純利益 32.2(GAAP)。Q3 2026: 売上 95.6、純利益 10.3(GAAP) | https://www.sec.gov/Archives/edgar/data/903651/000110465926020655/inod-20251231x10k.htm | 2026-11-18 |
| C3.ai | うまくいかなかった | 企業向けの AI のアプリと基盤 | 最大 6 か月の有料の導入の段階から広げる | 使用量の課金、サブスクリプション | FY2026(2026-04 まで): 売上 250.3、純損失 470.4(GAAP) | https://www.sec.gov/Archives/edgar/data/1577526/000157752626000078/ai-20260430.htm | 2026-11-18 |
| Builder.ai | うまくいかなかった | AI で作るとうたったアプリの開発 | 人のエンジニアが多くを作ったと報道 | 確かめていない | 2024 年の売上は 220 から 55 へ直された(報道)。2025 年に破綻 | https://techinformed.com/unicorn-builder-ai-collapses-fomo-investing/ | 2026-11-18 |
| IBM Watson Health | うまくいかなかった | 医療のデータと分析 | IBM の部門 | 確かめていない | 部門の損益は見つからなかった。2022-01 に資産を Francisco Partners へ売る合意 | https://newsroom.ibm.com/2022-01-21-Francisco-Partners-to-Acquire-IBMs-Healthcare-Data-and-Analytics-Assets | 2026-11-18 |
| SoundHound | AI の会社(上場) | 音声の AI | 確かめていない | 確かめていない | FY2025: 売上 168.9、純損失 14.0(GAAP)。Q3 2026: 売上 62.4、純損失 45.8(GAAP) | https://data.sec.gov/api/xbrl/companyconcept/CIK0001840856/us-gaap/NetIncomeLoss.json | 2026-11-18 |
| BigBear.ai | AI の会社(上場) | 防衛などの AI の分析 | 確かめていない | 確かめていない | FY2025: 売上 127.7、純損失 293.9(GAAP)。Q3 2026: 売上 43.6、純損失 91.9(GAAP) | https://data.sec.gov/api/xbrl/companyconcept/CIK0001836981/us-gaap/NetIncomeLoss.json | 2026-11-18 |
| SpaceX の SI 部門(xAI の Grok を含む) | AI の会社(上場の会社の部門) | Grok、Cursor、X、AI の基盤の契約 | 確かめていない | 確かめていない | Q3 2026: 部門の売上 7,560、部門の営業利益 431。2026 年 1〜9 月: 売上 10,939、営業損失 3,295(部門の数字。計算) | https://www.sec.gov/Archives/edgar/data/1181412/000162828026066880/spcx-20260930.htm | 2026-11-18 |
| Mistral | AI の会社(非上場) | モデルと企業向けの導入 | 確かめていない | 確かめていない | 年換算の売上(run-rate) 400 超(2026-02、CEO の発言の報道)。損益は見つからなかった | https://texxr.com/1163242/mistral-reports-400m-arr-aims-1b-2026 | 2026-11-18 |

## 1. 同じ型、近い型(FDE を取り入れた会社)

### Palantir(基準)

- 創業は 2003 年。米国の情報機関のテロ対策の仕事から始まった(FY2025 の 10-K、Item 1、出典: https://www.sec.gov/Archives/edgar/data/1321655/000132165526000011/pltr-20251231.htm、見た日 2026-11-18)。
- FDE は上場の後の最初の 10-K にある。「Our forward deployed engineers ("FDEs")」がアフガニスタンの基地や中西部の工場に出向いた、と書く(FY2020 の 10-K、出典: https://www.sec.gov/Archives/edgar/data/1321655/000119312521060650/d65934d10k.htm、見た日 2026-11-18)。
- 同じ 10-K は、試行の段階で赤字を出すことを明記する。短い試行は無料か安い値で行い、その間は「we operate the accounts at a loss」と書く。2019 年の Acquire の段階の顧客は、売上 0.6 に対し貢献損失 65.4。同じ顧客は 2020 年に売上 77.1、貢献利益 13.2 になった(出典: 同上、見た日 2026-11-18)。
- 狙う案件も書く。導入の費用と失敗の危険が高い大きな案件を、断らずに「actively seek them out」と書く。この方針は FY2025 の 10-K にも残る(出典: FY2025 の 10-K、見た日 2026-11-18)。
- 今の試行は AIP bootcamp だ。実際の顧客のデータで、数日で動く仕事の流れを届ける、と書く(FY2025 の 10-K、出典: 同上、見た日 2026-11-18)。
- 収益の区分は 3 つ。自社の環境のクラウド、顧客の環境のソフトウェア、専門のサービスだ。専門のサービスは、利用の支援、画面の設定、研修、データのモデル化の支援を含む(FY2025 の 10-K の会計方針、出典: 同上、見た日 2026-11-18)。
- GAAP の純利益(普通株主に帰属)。SEC の XBRL の API から取った(出典: https://data.sec.gov/api/xbrl/companyconcept/CIK0001321655/us-gaap/NetIncomeLoss.json、見た日 2026-11-18)。

| 期 | 売上(GAAP) | 純利益(GAAP) |
|---|---|---|
| FY2018 | - | -580.0 |
| FY2019 | 742.6 | -579.6 |
| FY2020 | - | -1,166.4 |
| FY2021 | - | -520.4 |
| FY2022 | 1,905.9 | -373.7 |
| FY2023 | 2,225.0 | 209.8 |
| FY2024 | 2,865.5 | 462.2 |
| FY2025 | 4,475.4 | 1,625.0 |
| Q3 2026 | 2,313.4 | 1,128.0 |

- 「-」は、このファイルでは取らなかった値。くわしい表は palantir-business.md にある。
- Q4 2022 の純利益 30.9 は、FY2022 から Q1〜Q3 を引いて計算した。Q4 2022 から Q3 2026 まで 16 四半期続けて黒字だ(計算)。
- 会社は Q4 2022 の決算の発表で、これを「First Quarter of Positive GAAP Net Income」と書く(出典: https://www.sec.gov/Archives/edgar/data/1321655/000132165523000005/a2022q4ex991pressrelease.htm、見た日 2026-11-18。palantir-business.md の節 5 で確かめた)。
- 会社は FY2026 の売上を 8,530〜8,534 と見込む(会社の見込み)。2026 年の各四半期で GAAP の営業利益と純利益が出るとも書く(Q3 2026 の決算の発表、出典: https://www.sec.gov/Archives/edgar/data/1321655/000132165526000045/a2026q3ex991pressrelease.htm、見た日 2026-11-18)。

### OpenAI

- FDE の部隊がある。Seattle の求人(2026-09-12 掲載)は、部隊を「customer delivery と core platform の間」で働くと書く。仕事は、最前線のモデルを本番に入れる導入を端から端まで率いること、顧客のチームに「Embed」すること、自分でコードを書くことだ(求人の写し、出典: https://jobs.thrivecap.com/companies/openai/jobs/92970121-forward-deployed-engineer-fde-seattle、見た日 2026-11-18)。公式の openai.com の求人ページは 403 で開けなかった。
- 検索の結果では、医療、法務、生命科学の業種ごとの FDE と、FDE の基盤のエンジニアの求人も出ていた(公式のページは開けなかった)。
- 損益は節 4 に書く。

### Anthropic

- 2026-11-10 に SEC へ S-1/A(上場の届出の修正 2 号)を出した。ティッカーは ANT と表示されている(出典: https://www.sec.gov/Archives/edgar/data/2130357/000162828026072484/anthropicpbc-sx1ax2.htm、見た日 2026-11-18)。
- S-1/A は「Applied AI」を定義する。Applied AI の部隊は「forward-deployed engineers」を含み、企業と一緒に、その会社の仕組みに合わせた解決を設計して導入する、と書く(出典: 同上、見た日 2026-11-18)。
- 同じ書類は、主な広がり方を別に書く。Claude の広がりの多くは「organic」で、大きな直販の組織によるものでない。直販の部隊が会う時点で、Claude はすでに使われていることが多い、と書く(出典: 同上、見た日 2026-11-18)。
- 求人の数(Greenhouse の公開の API、2026-11-18 時点): 題に「Forward Deployed」を含むものが 8 件(London、Paris、Munich、New York などの FDE と、その管理職)。題に「Applied AI」を含むものが 52 件(出典: https://boards-api.greenhouse.io/v1/boards/anthropic/jobs、見た日 2026-11-18)。
- Staff FDE の求人は、戦略的な顧客に入り込み、何を作るかを決めて作り上げる役と書く。年収の幅は 280,000〜320,000 ドル(出典: https://job-boards.greenhouse.io/anthropic/jobs/5449229008、見た日 2026-11-18)。

### Cohere

- 公開の求人(Ashby の公開の API)に、FDE が 10 件あった。種類は Agentic Platform、Infrastructure、Sovereign AI、Inference。場所は米国、カナダ、欧州、英国の公共、韓国、中東だ(出典: https://api.ashbyhq.com/posting-api/job-board/cohere、見た日 2026-11-18)。
- 米国の FDE(Agentic Platform)の求人は、North(企業向けの AI の作業の場)を顧客に入れる役だ。年収の幅は CA$175K〜CA$385K と表示(出典: https://jobs.ashbyhq.com/cohere/b0bcef37-1d20-414f-aade-c54942d63df9、見た日 2026-11-18)。
- 損益は節 4 に書く。

### Scale AI

- 公開の求人(Greenhouse の公開の API)に、題に「Forward Deployed」を含むものが 12 件あった。Forward Deployed の製品の担当(企業、公共)、公共の FDE、「Frontier Agents Engineer (Forward Deployed Engineering)」などだ(出典: https://boards-api.greenhouse.io/v1/boards/scaleai/jobs 、例: https://job-boards.greenhouse.io/scaleai/jobs/4694861005、見た日 2026-11-18)。
- 求人の本文と損益は確かめていない。

### Mistral

- FDE の求人は確かめられなかった。Lever の公開の API は 2 件しか返さず、読み取れなかった。

## 2. サービスをソフトウェアのように売る会社

### 考え方の出どころ

- 投資会社の Foundation Capital は「service as software」を唱える。売る側が道具でなく結果に責任を持ち、料金は席数から成果(例: 取れた商談や契約)へ移る、と書く。市場の大きさを 4.6 兆ドルとする(会社の記事、出典: https://foundationcapital.com/ai-service-as-software/、見た日 2026-11-18)。記事の元の公開日は、ページから確かめられなかった。

### Sierra

- 成果課金を自社のブログで説明する。解決しない会話は「in most cases」課金しない。「Sierra gets paid only when we complete a task for you」と書く(2024-12-10、出典: https://sierra.ai/blog/outcome-based-pricing-for-ai-agents、見た日 2026-11-18)。
- 同じ記事は、成果課金が合わない場面では、会話ごとの課金などを混ぜると書く(出典: 同上、見た日 2026-11-18)。
- 年換算の売上(ARR)が 100 を超えた。創業から 21 か月で、会社の発表を TechCrunch が報じた(2025-11-21、報道、出典: https://techcrunch.com/2025/11/21/bret-taylors-sierra-reaches-100m-arr-in-under-two-years/、見た日 2026-11-18)。損益は出ていない。
- 導入の人を置く。「Product Manager, Agent Development」の求人は、エンジニアと顧客と一緒に AI エージェントを作って出す役だ。年収の幅は 180K〜390K ドル(出典: https://jobs.ashbyhq.com/Sierra/effd7cd2-8a28-4bae-a3b8-40720ba09717、見た日 2026-11-18)。

### Decagon

- 2 つの課金を並べる。会話ごとの定額と、解決ごとの高めの定額(人に渡した会話は無料)だ。「the majority of our customers gravitate towards per-conversation pricing」と書く。理由は予算の読みやすさと、「解決」の定義の争いを避けられることだ(2024-12-10、出典: https://decagon.ai/blog/pricing-ai-agents、見た日 2026-11-18)。
- 導入の人を置く。「Senior Agent Product Manager」の求人は、Fortune 500 の経営層が相手で、顧客は「support tool」でなく変革を買う、と書く(出典: https://jobs.ashbyhq.com/decagon/dcf9b561-f2fb-422b-88a9-33ce76e96608、見た日 2026-11-18)。
- 公開の単価と損益は見つからなかった。

### Intercom(Fin)

- 1 成果 0.99 ドル。解決は「No further help is requested after Fin's last answer」で数える。1 会話で数回動いても 1 成果だ。ほかの道具と使う場合は月 50 成果の最低がある(月 49 ドルで 50 成果を含む。席の料金はない)。Intercom の helpdesk と使う場合は、席が月 19 ドルから別にかかる(出典: https://fin.ai/pricing、見た日 2026-11-18)。

### Zendesk

- 2024-08-28 に、AI エージェントを成果課金に変えたと発表した。AI が自分で解決した件だけ課金し、少しの利用は無料で付ける(会社の発表、出典: https://zendesk.co.uk/newsroom/articles/zendesk-outcome-based-pricing、見た日 2026-11-18)。発表に 1 件の単価はなかった。

### Salesforce(Agentforce)

- 料金は 3 つの形を並べる。Flex Credits は 10 万クレジットで 500 ドル(1 アクション 20 クレジット = 0.10 ドル)。会話は 1 件 2 ドル。従業員向けは席数で、Agentforce の add-on は 1 人月 125 ドル、Max Edition は 1 人月 550 ドルから(出典: https://www.salesforce.com/agentforce/pricing/、見た日 2026-11-18)。
- 料金の変遷: 2025-05-15 の発表で、それまでの会話ごと 2 ドルに、アクションごとの Flex Credits を足した。席の契約と AI の利用の間で、予算を移せる契約も出した(会社の発表、出典: https://www.salesforce.com/news/?p=87214、見た日 2026-11-18)。
- 損益は比べる表に書いた(FY2026 の 10-K)。

### Accenture(古い型の代表)

- FY2026 の 10-K は、多くの契約で報酬を「outcome-based measures」(費用の削減、売上の向上など)に結びつけると書く(出典: https://www.sec.gov/Archives/edgar/data/1467373/000146737326000049/acn-20260831.htm、見た日 2026-11-18)。
- 同じ 10-K は、AI による自動化で自社のサービスの需要が減ったことがある、と書く。AI に合った新しい料金の形を顧客が受け入れなければ業績が悪くなる、とも書く(出典: 同上、見た日 2026-11-18)。
- FY2026 の売上 74,183、純利益 8,367(GAAP、SEC の XBRL、出典: https://data.sec.gov/api/xbrl/companyconcept/CIK0001467373/us-gaap/NetIncomeLoss.json、見た日 2026-11-18)。

### Innodata(AI 向けのデータのサービス)

- AI の研究所とモデルの会社が主な顧客だ。いわゆる「Magnificent Seven」のうち 5 社を顧客に持つ、と FY2025 の 10-K に書く(出典: https://www.sec.gov/Archives/edgar/data/903651/000110465926020655/inod-20251231x10k.htm、見た日 2026-11-18)。
- 1 社への偏りが大きい。FY2025 は 1 社が売上の約 58%、FY2024 は約 48% だ(出典: 同上、見た日 2026-11-18)。
- GAAP の純利益: FY2024 は 28.7、FY2025 は 32.2。2026 年は Q1 14.9、Q2 14.4、Q3 10.3(SEC の XBRL、出典: https://data.sec.gov/api/xbrl/companyconcept/CIK0000903651/us-gaap/NetIncomeLoss.json、見た日 2026-11-18)。

## 3. うまくいかなかった会社

### C3.ai

- 売り方は Palantir に近い。顧客は、最大 6 か月の有料の「Initial Production Deployment」から始める。その後は、月額と使用量の課金か、期間を決めた複数年の契約に移る(FY2026 の 10-K、出典: https://www.sec.gov/Archives/edgar/data/1577526/000157752626000078/ai-20260430.htm、見た日 2026-11-18)。
- 損失は創業から続く。「We incurred net losses in each period since our founding in 2009」と書く。純損失は FY2024 279.7、FY2025 288.7、FY2026 470.4(GAAP)だ(出典: 同上、見た日 2026-11-18)。
- 売上は減った。FY2025 の 389.1 から FY2026 の 250.3 へ、35.7% の減少(計算)。Q1 FY2027(2026-05〜07)は売上 52.4、純損失 92.8(GAAP、SEC の XBRL、出典: https://data.sec.gov/api/xbrl/companyconcept/CIK0001577526/us-gaap/NetIncomeLoss.json、見た日 2026-11-18)。
- 会社は理由を書く。営業とサービスの組織の大きな作り直し、CEO の健康の問題、営業とサービスの実行の不十分さだ(FY2026 の 10-K、出典: 同上、見た日 2026-11-18)。
- 専門のサービスの売上のうち、優先の開発のサービスが 78%(FY2026)を占める(出典: 同上、見た日 2026-11-18)。

### Builder.ai

- 「AI で作る」とうたったアプリの開発の会社だった。報道では、約 700 人のエンジニア(主にインド)が裏で作業し、成果を AI の出力として見せていた。記事は特定の出典を挙げていない(2025-06-13、報道、出典: https://www.eweek.com/news/builderai-bankruptcy-ai-developers-coding/、見た日 2026-11-18)。
- 監査で売上が直された。2024 年は 220 から 55、2023 年は 180 から 45 へ。元は Financial Times の報道で、無料の記事で確かめた(2025-05-23、報道、出典: https://techinformed.com/unicorn-builder-ai-collapses-fomo-investing/、見た日 2026-11-18)。
- 会社は LinkedIn で、過去の決定から立ち直れず管財人を置くと述べた(報道の引用、出典: https://www.eweek.com/news/builderai-bankruptcy-ai-developers-coding/、見た日 2026-11-18)。会社の投稿そのものは開けなかった。
- 推測: サービス(人の作業)をソフトウェアと見せて売る形は、原価がソフトウェアのように下がらない。Builder.ai は、その差を売上の見せ方で埋めた例と読める。

### IBM Watson Health

- IBM は 2022-01-21、Watson Health の医療のデータと分析の資産を Francisco Partners へ売る合意を発表した。対象は Health Insights、MarketScan、Micromedex などだ。金額は公表していない(会社の発表、出典: https://newsroom.ibm.com/2022-01-21-Francisco-Partners-to-Acquire-IBMs-Healthcare-Data-and-Analytics-Assets、見た日 2026-11-18)。
- 部門の売上と損益の一次情報は見つからなかった。

## 4. AI のモデルの会社と AI エージェントの会社の売上と損失

### Anthropic(S-1/A、GAAP。四半期は監査前)

| 期 | 売上 | 計算資源の費用 | 営業損益 | 純損益 |
|---|---|---|---|---|
| FY2023 | 41 | 433 | -551 | -1,531 |
| FY2024 | 386 | 2,522 | -2,980 | -8,309 |
| FY2025 | 4,585 | 7,326 | -8,060 | -41,965 |
| 2026 年 1〜9 月 | 33,242 | 18,808 | -1,260 | -104,039 |
| Q2 2026 | 11,555 | 5,558 | 974 | -66,309 |
| Q3 2026 | 16,956 | 9,863 | -567 | -23,291 |

- 出典: https://www.sec.gov/Archives/edgar/data/2130357/000162828026072484/anthropicpbc-sx1ax2.htm (見た日 2026-11-18)。
- 純損失の多くは、転換社債、デリバティブ、SAFE の評価の変動だ。FY2025 は 34,308、2026 年 1〜9 月は 94,324。会社の価値が上がると、この費用が増える仕組みだ、と書く(出典: 同上、見た日 2026-11-18)。
- 計算資源の費用は、売上に対して FY2024 に 653%、FY2025 に 160%、2026 年 1〜9 月に 57% だった(出典: 同上、見た日 2026-11-18)。
- Q3 2026 の営業損失の理由も書く。短期の契約で買った計算資源 5,000(複数年の契約より高い)と、寄付のマッチングの現金の出ない費用 2,000 だ(出典: 同上、見た日 2026-11-18)。
- 年換算の売上(run-rate)は、会社の発表で 2026-02 に 14,000 だった(検索の要旨。発表のページは開けなかった)。

### OpenAI(非上場。数字はすべて報道)

- 2025 年: 売上 13,070、営業損失 20,920、純損失 38,530(調整の後)。売上原価 7,500、研究開発費 19,180(モデルの学習と計算の基盤を含む)。Microsoft への支払い 約 17,200 のうち 10,590 が研究開発費(報道)。元は記者 Ed Zitron の報道で、Financial Times が確かめたとされる(2026-06-16、出典: https://analyticsindiamag.com/ai-news/openai-spent-34-billion-in-2025-report、見た日 2026-11-18)。
- 同じ報道は、純損失の大部分を現金の出ない費用とする。非営利から営利への移行に伴う 41,550 の費用と、投資家の権利の評価の上げだ(報道、出典: 同上、見た日 2026-11-18)。
- Q1 2026: 売上 5,700(前年の約 3 倍)、現金の流出 約 3,700、営業損失 9,300、純損失 21,300 超(うち 12,400 が評価の損)。元は The Information が株主向けの資料をもとに報じた(2026-06-20、報道、出典: https://the-decoder.com/openai-tripled-revenue-to-5-7-billion-in-q1-but-burned-through-3-7-billion-to-get-there/、見た日 2026-11-18)。
- OpenAI の S-1 は、EDGAR の全文検索で見つからなかった(2026-11-18 時点)。

### SpaceX の SI 部門(xAI の Grok を含む。上場の会社の部門)

- SpaceX の Q3 2026 の 10-Q は、SI 部門(旧 AI 部門)に、Grok、Cursor(2026-08-14 に合併を完了)、X、企業向けの AI の基盤を含むと書く(出典: https://www.sec.gov/Archives/edgar/data/1181412/000162828026066880/spcx-20260930.htm、見た日 2026-11-18)。
- 部門の数字: Q3 2026 は売上 7,560、費用 7,129、営業利益 431。前年同期は売上 813、営業損失 1,722。2026 年 1〜9 月は売上 10,939、費用 14,234 で、営業損失 3,295(計算)(出典: 同上、見た日 2026-11-18)。
- Q3 2026 の売上の増加は、主に AI の基盤の契約と Cursor の売上による、と書く。SI Solutions & Infrastructure の売上は Q3 2026 に 7,022 だ(出典: 同上、見た日 2026-11-18)。推測: この部門の黒字は、モデルの販売より、計算の基盤を貸す契約から来ている。

### Cohere と Mistral(非上場)

- Cohere: CEO は 2025-10 に、年換算の売上(月の売上を年に引き延ばした値)を 150 と述べ、利益率は「really good」と言った。理由は、顧客が自分の機械でモデルを動かすことだ(報道、出典: https://thelogic.co/briefing/gomez-says-cohere-on-path-to-profitability-as-it-targets-ipo-soon/、見た日 2026-11-18)。損益の数字は出ていない。
- Mistral: CEO は 2026-02 に、年換算の売上(run-rate)を 400 超と述べた。1 年前は約 20。2026 年末に 1,000 を目指す(報道。元は Financial Times、出典: https://texxr.com/1163242/mistral-reports-400m-arr-aims-1b-2026、見た日 2026-11-18)。損益は見つからなかった。

### 上場の AI の会社(10-K と 10-Q、GAAP)

| 会社 | 期 | 売上 | 営業損益 | 純損益 | 出典 |
|---|---|---|---|---|---|
| C3.ai | FY2026(2026-04 まで) | 250.3 | - | -470.4 | https://www.sec.gov/Archives/edgar/data/1577526/000157752626000078/ai-20260430.htm |
| SoundHound | FY2024 | 84.7 | -341.4 | -350.7 | https://data.sec.gov/api/xbrl/companyconcept/CIK0001840856/us-gaap/NetIncomeLoss.json |
| SoundHound | FY2025 | 168.9 | -23.3 | -14.0 | 同上 |
| SoundHound | Q3 2026 | 62.4 | -46.0 | -45.8 | 同上 |
| BigBear.ai | FY2025 | 127.7 | -213.9 | -293.9 | https://data.sec.gov/api/xbrl/companyconcept/CIK0001836981/us-gaap/NetIncomeLoss.json |
| BigBear.ai | Q3 2026 | 43.6 | -100.0 | -91.9 | 同上 |
| CoreWeave(AI のクラウド) | FY2025 | 5,131 | - | -1,167 | https://data.sec.gov/api/xbrl/companyconcept/CIK0001769628/us-gaap/NetIncomeLoss.json |

- 見た日はすべて 2026-11-18。「-」は取らなかった値。
- SoundHound の FY2025 の損失が小さいのは、Q1 2025 に純利益 129.9 を計上したためだ。中身(評価の変動か)は確かめていない。

### 反例: AI で GAAP の黒字を続ける会社(数え方を分ける)

| 数え方 | 会社 | GAAP の純利益 | 出典 |
|---|---|---|---|
| AI のモデル、エージェント、AI プラットフォームを主に売る | Palantir | FY2023 209.8、FY2024 462.2、FY2025 1,625.0 | 節 1 |
| 同上 | (ほかに見つからなかった) | Anthropic は Q2 2026 に営業利益のみ黒字。純損益は赤字 | 節 4 |
| AI の会社向けのサービス(AI 専業に近い) | Innodata | FY2024 28.7、FY2025 32.2、2026 年の各四半期も黒字 | https://data.sec.gov/api/xbrl/companyconcept/CIK0000903651/us-gaap/NetIncomeLoss.json |
| AI を使う広告(AI を主に売るかは議論が分かれる) | AppLovin | FY2023 356.7、FY2024 1,579.8、FY2025 3,333.8 | https://data.sec.gov/api/xbrl/companyconcept/CIK0001751008/us-gaap/NetIncomeLoss.json |
| AI の基盤(半導体) | Nvidia | FY2026(2026-01 まで) 120,067 | https://data.sec.gov/api/xbrl/companyconcept/CIK0001045810/us-gaap/NetIncomeLoss.json |
| AI の導入のサービス(古い型) | Accenture | FY2026(2026-08 まで) 8,367 | 節 2 |

- 見た日はすべて 2026-11-18。
- 「AI の会社」を AI のモデル、エージェント、AI プラットフォームの会社に限ると、運営者の「Palantir だけ」は合う。AI の会社向けのサービスや、AI の基盤まで広げると合わない。
- Microsoft、Alphabet などの大きなクラウドの会社も黒字だが、AI の部分の損益は分けて出ていないので、表に入れなかった。

## 5. SaaS の席数の課金と、成果や導入の課金の比べ

| 課金の形 | 例の会社と公開の料金 | 収益の出方 | 売る側の危険 | 買う側の危険 | 出典 |
|---|---|---|---|---|---|
| 席数 | Salesforce の Agentforce の add-on 1 人月 125 ドル、Max Edition 1 人月 550 ドルから。Intercom の席 月 19 ドルから | 人の数に比例。予測しやすい | AI で顧客の利用者が減ると売上が減る。Salesforce の 10-K は「decreases in the number of users」を解約の要因に挙げる | 使わない席にも払う | https://www.salesforce.com/agentforce/pricing/ 、https://www.sec.gov/Archives/edgar/data/1108524/000110852426000060/crm-20260131.htm |
| 使用量 | Salesforce の Flex Credits 1 アクション 0.10 ドル。Workday の Flex Credits(単価は非公開)。ServiceNow の「assist」のパック。Decagon の会話ごと | 使った量に比例 | 利用が見込みを下回ると売上が減る(Salesforce の 10-K)。単位が会社ごとに違う | 請求の額が読みにくい | https://www.salesforce.com/news/?p=87214 、https://blog.workday.com/en-us/introducing-workday-flex-credits-smarter-more-flexible-way-access-ai-innovation.html 、https://www.constellationr.com/insights/news/servicenow-aims-goldilocks-software-model-saas-industry-likely-follow |
| 成果 | Intercom Fin 1 成果 0.99 ドル。Zendesk は自動の解決の件だけ。Sierra は成果課金が主 | 解決した件数に比例 | 解決できない件は無収入。計算の費用は解決しなくてもかかる(推測) | 「解決」の定義の争い。Decagon は、これを避けたい顧客が会話ごとを選ぶと書く | https://fin.ai/pricing 、https://zendesk.co.uk/newsroom/articles/zendesk-outcome-based-pricing 、https://sierra.ai/blog/outcome-based-pricing-for-ai-agents 、https://decagon.ai/blog/pricing-ai-agents |
| 導入の契約 | Palantir は無料か安い試行の後にサブスクリプションと専門のサービス。C3.ai は最大 6 か月の有料の導入。Accenture は成果の指標に結びつく契約も多い | 大口の長い契約。最初は赤字 | 試行の間は赤字(Palantir の 2019 年の Acquire の段階は売上 0.6 に貢献損失 65.4)。試行が本契約にならない危険(Palantir の 10-K) | 1 社に深く依存する。途中で解約できる契約も多い(Palantir の 10-K) | https://www.sec.gov/Archives/edgar/data/1321655/000119312521060650/d65934d10k.htm 、https://www.sec.gov/Archives/edgar/data/1577526/000157752626000078/ai-20260430.htm 、https://www.sec.gov/Archives/edgar/data/1467373/000146737326000049/acn-20260831.htm |

- 見た日はすべて 2026-11-18。
- 席数の課金が揺らいでいる、という会社の発言と記載:
  - Salesforce の FY2026 の 10-K は、解約の要因に「decreases in the number of users at our customers」と「the increased prevalence of consumption-based pricing models」を並べる(出典: https://www.sec.gov/Archives/edgar/data/1108524/000110852426000060/crm-20260131.htm、見た日 2026-11-18)。
  - Workday は、席数の課金は人の仕事を助ける道具には「has long been the right fit」だったが、AI では価値が作業の量で決まる、と書く(会社のブログ、日付の表示なし、出典: https://blog.workday.com/en-us/introducing-workday-flex-credits-smarter-more-flexible-way-access-ai-innovation.html、見た日 2026-11-18)。
  - ServiceNow の CEO は決算の説明会で「Our goal is to combine both subscription and consumption pricing」と述べた(2025-01-30、解説の記事の引用、出典: https://www.constellationr.com/insights/news/servicenow-aims-goldilocks-software-model-saas-industry-likely-follow、見た日 2026-11-18)。説明会の記録そのものは開けなかった。
  - Sierra は、旧来の顧客対応の会社は AI が良くなるほど席の売上が減る、と書く(出典: https://sierra.ai/blog/outcome-based-pricing-for-ai-agents、見た日 2026-11-18)。

## 6. 読み方の注意(推測を含む)

- 「SaaS よりずっと古い」の根拠: EDS は 1962 年の創業。Perot は Frito-Lay に計算の仕事の代金を月 5,128 ドルで請求したと語った(出典: https://hpalumni.org/edsHistoryCulture、見た日 2026-11-18)。CIO の 2007 年の記事は、SaaS が 1990 年代の ASP から育ち、ASP は 2000〜2001 年に行き詰まったと書く(出典: https://www.cio.com/article/272086/web-services-software-as-a-service-saas-definition-and-solutions.html、見た日 2026-11-18)。SaaS という語の早い例は、SIIA の 2001-02 の「Software as a Service: Strategic Backgrounder」とされる(検索の要旨のみ。本文は開けなかった)。IBM のサービスの歴史は確かめていない。
- 「新しい Palantir の型」の根拠: Palantir は 2003 年の創業で、FDE は 2021-02 提出の 10-K にすでにある。AI のモデルの会社が FDE を大きく募集しているのは 2026 年の求人で確かめた。新しいのは型でなく、使う会社の顔ぶれだ。
- Anthropic の数字は上場の届出(S-1/A、2026-11-10 の修正 2 号)だ。年の数字は監査済みの財務諸表から、四半期と 1〜9 月の数字は監査前の財務諸表から取った、と書かれている。上場が完了したかは確かめていない。
- GAAP の純損益は、未上場の AI の会社では、評価の変動で大きく揺れる。営業損益のほうが事業の様子を表しやすい。Anthropic の FY2025 は、純損失 41,965 のうち 34,308 が評価の変動だ。
- 年換算の売上(run-rate、ARR)は、直近の月や週を年に引き延ばした値で、会計の売上ではない。Sierra、Cohere、Mistral の数字はこれだ。
- SpaceX の SI 部門の営業利益は、会社の部門の測り方の数字で、GAAP の連結の営業利益とは違う。
- OpenAI の数字はすべて報道だ。元の報道は有料か個人のニュースレターで、無料の報道の要旨で確かめた。
- 推測: 運営者の「事業の形」の見立ては、2 つの意味に分けると確かめやすい。(1) 売上より費用が大きい、という意味なら、一次情報が支える。(2) 製品を広く売るのが悪く、サービスとして売れば利益が出る、という意味なら、一次情報は支えない。Palantir 自身が約 20 年赤字で、C3.ai は導入を先に売っても赤字だ。
- 推測: Palantir の利益率の高さは、粗利率(FY2024 で 80%。palantir-business.md)と、計算資源を大きく買わない事業であることに支えられている。モデルを自分で学習させる会社とは、費用の形がちがう。
- 推測: 成果課金は、AI のモデルの費用を売る側が負う形だ。解決率が低い間は、売る側の粗利が下がる。Decagon が会話ごとの課金を主にしているのは、その危険を顧客と分けるためと読める。

## 見つからなかったこと

- 開けなかったページ:
  - openai.com の FDE の求人(https://openai.com/careers/forward-deployed-engineer-(fde)-sf-san-francisco/): 403。求人の写しで代えた。
  - Palantir の Q4 2025 の決算の発表(https://www.businesswire.com/news/home/20260201154946/en/): 403。SEC の 10-K と XBRL で代えた。
  - Palantir の Q3 2026 の発表(https://investors.palantir.com/news-details/2026/Palantir-Reports-Q3-2026-U-S--Comm-Revenue-Growth-of-148-YY-and-Revenue-Growth-of-96-YY/): 本文が取れなかった。SEC の 8-K の添付で代えた。
  - barchart の Palantir の記事: 本文が空だった。
  - ServiceNow の Element AI の買収の発表(https://www.servicenow.com/company/media/press-room/servicenow-to-acquire-element-ai.html): 403。Element AI は表に入れなかった。
  - TechSpot の OpenAI の記事(https://www.techspot.com/news/112794-openai-made-13-billion-2025-lost-21-billion.html): 403。
  - Siècle Digital の Mistral の記事(https://siecledigital.fr/2026/01/22/mistral-ai-vise-le-milliard-de-dollars-de-revenus-des-2026/): 403。
  - Hargreaves Lansdown の Mistral の記事: 404。
  - SIIA の SaaS の文書(http://www.siia.net/estore/ssb-01.pdf): 404。
  - Anthropic の古い求人(Greenhouse の 4985877008、5012991008): 求人の一覧に戻され、本文がなかった(閉じた求人とみられる)。
- 見つからなかった数字:
  - Sierra、Decagon、Intercom、Zendesk、Scale AI、Cohere、Mistral の損益。
  - IBM Watson Health の部門の損益。
  - Workday の Flex Credits の単価。ServiceNow の決算の説明会の記録そのもの。
  - Zendesk の今の 1 件の単価(解説の記事は 1.50 ドルと書くが、会社の資料で確かめていない)。
  - AI のエージェントを主に売る会社で、GAAP の黒字を続ける会社。
- 確かめていないこと:
  - Palantir の CEO の手紙の中身(創業者の AI の見立て)。
  - Mistral の FDE の求人。
  - IBM の 1960 年代のサービスの事業の歴史。
