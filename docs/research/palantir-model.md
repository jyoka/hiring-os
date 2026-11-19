# Palantir の売り方と作り方(2026-11 時点)

## 結論

- Forward Deployed Engineer(FDE)は、顧客の現場に入り込み、顧客のデータで動く仕組みを作るエンジニアだ。採用ページでは、FDE の求人は「Delta」、組になる Deployment Strategist の求人は「Echo」に分類されている。顧客ごとの人数は、S-1 にも 10-K にも開示がない。S-1 は「伸びの大きい顧客に FDE を割り当て、短期の貢献利益が下がっても続ける」とだけ書く。
- S-1(2020-08)は、顧客を Acquire、Expand、Scale の 3 段で管理すると書いた。Acquire はその年の売上が 10 万ドル未満の顧客で、試験は無料か低額で会社が費用を持つ。Expand は貢献利益率がマイナスの顧客で、2019 年は (43)% だった。Scale はプラスの顧客で、2019 年は 55% だった(どれも非 GAAP)。段階ごとの数字は FY2021 の 10-K が最後だ。
- 2023 年から、長い試験(pilot)の代わりに AIP ブートキャンプを入れた。公式ページは「0 から使える例まで 5 日」と書く。2023-10 に「1 年で 500 回」を目標にし、2024-02 の決算説明会では 560 回超(465 組織)と話した。ケーブル TV の会社は 5 日のブートキャンプの後、同じ四半期に約 300 万ドルの契約を結んだ(会社の発言)。
- オントロジーは、既存のデータの上に載せる「業務のモデル」だ。公式の文書は、objects、properties、links(意味の側)と、actions、functions(操作の側)に分けて説明する。actions は webhook で SAP や Salesforce に書き戻せる。
- Palantir は既存のシステムを置き換えず、上に載せる形を取る。SAP には SAP の上で動く専用のコネクタがある。Snowflake、Databricks、BigQuery などのデータは、コピーせずに virtual tables で参照できる。SAP、Databricks、Snowflake、Microsoft、Oracle とは提携のページがある。
- 料金はサブスクリプション(Palantir のクラウドか顧客の環境)と専門サービスで、契約は 1〜5 年だ。使用量の契約もあり、公式の文書は compute-seconds で計る。AIP の価格は見つからなかった。政府では、米陸軍が 75 の契約を 1 つの enterprise agreement にまとめた(10 年、上限 100 億ドル)。
- 広がりの数字は大きく伸びた。上位 20 社の平均の売上は、2019 年の 2,480 万ドルから、2026-09 までの 12 か月で 1 億 4,600 万ドルになった。net dollar retention は 2023 年 Q4 の 108% から、2026 年 Q3 の 165% になった(後者は解説の記事で、会社の資料は開けていない)。
- 弱みは、売る前に人と試験の費用が先に出ることだ。2019 年は販売費が売上の 61%(GAAP、自分で計算)で、貢献利益率は 21% だった。2026 年 Q3 は、販売費が 17% に下がり、貢献利益率が 73% に上がった。それでも「ソフトの皮をかぶったコンサル」という批判は、元社員や VC の解説に残る。

## 1. 製品の役割(Gotham、Foundry、Apollo、AIP)

FY2025 の 10-K は「4 つの主な基盤」として Gotham、Foundry、Apollo、AIP を挙げる(出典: https://www.sec.gov/Archives/edgar/data/1321655/000132165526000011/pltr-20251231.htm、見た日 2026-11-18)。

| 製品 | 役割 | 誰向けか | 始まり | 出典 |
|---|---|---|---|---|
| Gotham | 大量のデータを結び、1 つの画面で判断を助ける | 防衛、情報機関、災害救援の組織 | 最初の製品。S-1 は「防衛と情報機関の分析者のために作った」と書く | S-1、10-K FY2025、https://www.palantir.com/platforms/gotham/ |
| Foundry | データ管理、ロジック、オントロジー、分析、業務の流れを作る土台(「foundational data operations platform」) | 大企業と業界全体 | 2016 年に出した(S-1) | S-1、10-K FY2025 |
| Apollo | 継続的な配信の基盤。更新、セキュリティの修正、設定を毎日配る | Palantir 自身と、自社のソフトを配りたい顧客。マルチクラウド、閉じた網(airgapped)、エッジでも動く | 10-K FY2025 に記載 | 10-K FY2025、https://www.palantir.com/platforms/apollo/ |
| AIP | 外部の LLM への安全な接続、エージェントと自動化を作る道具、評価の仕組み | 民間と政府の両方 | 2023 年に展開を始めた(10-K FY2025)。CEO の手紙「AIP in Action」は 2023-04-27 | 10-K FY2025、https://www.palantir.com/newsroom/letters/aip-in-action/april-27-2023/ |
| Warp Speed | 製造業向けの OS。会社のページは「業務に合わせて変わる manufacturing OS」と書く | 製造業、特に防衛の製造業 | 最初の利用企業は 2024-12 に発表(報道)。Anduril、L3Harris、Panasonic Energy of North America、Shield AI | https://www.palantir.com/warpspeed/、https://www.iotm2mcouncil.org/iot-library/news/connected-industries-news/first-companies-adopt-palantir-manufacturing-os/ |
| AI FDE | FDE の仕事をするエージェント。データの変換、オントロジーの作成と編集、関数、アプリ全体を作る | Foundry と AIP の利用者 | 開発者向けの催し DevCon 3 で発表(日付は確かめていない) | https://www.palantir.com/platforms/aip/agentcamp/ |
| Developer Tier | Foundry と AIP を限定して使える入口。「大きな初期費用なしに」試せる | 開発者(米国と一部の国) | 10-K FY2025 に記載 | 10-K FY2025 |

- 見た日はすべて 2026-11-18。
- Warp Speed は FY2025 の 10-K に名前が出てこない(本文の検索で 0 件)。会社の発表(Business Wire)は 403 で開けなかった。
- Warp Speed の報道は、使い道として「生産の計画」「設計変更の管理」「画像による品質検査」を挙げる(報道、出典: https://www.iotm2mcouncil.org/iot-library/news/connected-industries-news/first-companies-adopt-palantir-manufacturing-os/、見た日 2026-11-18)。

## 2. Forward Deployed Engineer(FDE)

### 何をする人か

- S-1 は、FDE がアフガニスタンの基地や中西部の工場まで行き、製品を入れたと書く。現場の時間が製品の改善につながる、とも書く(「Our forward deployed engineers ("FDEs") have travelled to bases in Afghanistan」)(出典: https://www.sec.gov/Archives/edgar/data/1321655/000119312520230013/d904406ds1.htm、見た日 2026-11-18)。
- 今の FDE の求人(ロンドン)は、役割を「顧客の中に入り、問題を自分のものにする」と書く。仕事は、顧客に合わせたアプリと LLM の流れを作ること、利用者から役員までの関係を持つことだ。出張は 25〜50%(出典: https://jobs.lever.co/palantir/5168e8fd-fec1-4fea-b7a1-81bdaea65850、見た日 2026-11-18)。
- 同じ求人は、FDE を「製品が今できることの外側まで作る」役と書く(「building past the perimeter of what the product currently offers」)。

### 社内の呼び名(Delta と Echo)

- 採用ページで、Forward Deployed Software Engineer の求人は「Delta」の区分に入っている(「Delta / Full-time / Hybrid」)(出典: https://jobs.lever.co/palantir/5168e8fd-fec1-4fea-b7a1-81bdaea65850、見た日 2026-11-18)。
- Deployment Strategist の求人は「Echo」の区分に入っている(「Echo / Full-time / Hybrid」)(出典: https://jobs.lever.co/palantir/e0ab8226-b928-4e3a-bf87-08fe7b1ea595、見た日 2026-11-18)。
- Deployment Strategist(Echo)の仕事は、現場で分析者の問いを聞くこと、使うデータを見つけること、FDE と組んでデータを流れに入れることだ。研修、役員への報告、デモ、新しい業界の案件の見積もりもする。出張は 25〜75%。米国(ニューヨーク)の年俸の目安は 11 万〜17 万ドル(出典: 同上、見た日 2026-11-18)。
- 公式ブログ「Dev versus Delta: Demystifying engineering roles at Palantir」は 403 で開けなかった。Delta を「FDE の社内の呼び名」とする説明は、検索で見た解説のサイトにもあるが、公式の本文では確かめていない。

### 人数の考え方

- S-1 は、顧客ごとの人数を書いていない。書いてあるのは配置の方針だ。各顧客の売上の伸びと利益を見続け、FDE を含む人を「伸びの一番大きい機会」に割り当てる。伸びが見込める間は、短期の貢献利益が下がっても人を置き続ける、と書く(「seek to allocate our personnel, including our FDEs, to the highest revenue growth opportunities」)(出典: S-1、見た日 2026-11-18)。
- S-1 は、FDE の力を広がりの条件の 1 つに挙げる。顧客が利用を広げるかは「新しい使い道を見つける FDE の力」などで決まる、という書き方だ(出典: 同上、見た日 2026-11-18)。この文は FY2022 の 10-K まで残り、FY2023 以降の 10-K には「forward deployed」の語がない(自分で本文を検索した)。
- FY2025 の 10-K は、代わりに「顧客の中に直接入る(We embed directly with customers)」と書く(出典: https://www.sec.gov/Archives/edgar/data/1321655/000132165526000011/pltr-20251231.htm、見た日 2026-11-18)。
- 元社員の文章は、顧客のチームを「たいてい 4〜5 人」と書く(解説、出典: https://nabeelqu.substack.com/p/reflections-on-palantir、見た日 2026-11-18、2024-10-15 の投稿)。会社の数字ではない。
- 2026-11-18 の採用ページの求人 301 件のうち、題名に「Forward Deployed」を含むものは 72 件、「Deployment Strategist」は 26 件だった(自分で数えた。勤務地ごとの重複を含み、人数ではない)(出典: https://jobs.lever.co/palantir、見た日 2026-11-18)。

### 費用はどこに入るか

- S-1 は、試験(pilot)と顧客の拡大に関わる人の給与を販売費に入れる、と書く。試験のためのクラウドの費用も販売費だ(出典: S-1、見た日 2026-11-18)。
- 運用と専門サービスに関わる人の給与は売上原価に入る(出典: S-1、見た日 2026-11-18)。FY2025 の 10-K も同じ区分で、販売費に営業の歩合が加わった(出典: 10-K FY2025、見た日 2026-11-18)。
- 推測: FDE の人件費は、試験中は販売費、契約後の運用は売上原価に入るとみられる。FDE の人件費の総額は開示されていない。

## 3. 顧客の段階と費用(acquire、expand、scale)

### 段階の定義と 2019 年の数字(S-1)

貢献利益(contribution)は、売上から売上原価と販売費を引いたものだ。どちらも株式報酬を除く(非 GAAP)。研究開発費と一般管理費は引かない。販売費には配賦した間接費も入る(出典: https://www.sec.gov/Archives/edgar/data/1321655/000119312520230013/d904406ds1.htm、見た日 2026-11-18)。

| 段階 | S-1 の定義 | 2019 年の売上 | 2019 年の貢献利益 | 同じ顧客の 2020 年上期 |
|---|---|---|---|---|
| Acquire | その年の売上が 10 万ドル未満 | 60 万ドル | 6,540 万ドルの損失 | 売上 1,880 万ドル、損失 1,390 万ドル |
| Expand | 売上 10 万ドル超で、貢献利益率がマイナス | 1 億 7,630 万ドル | (43)% | 売上 1 億 6,050 万ドル、35% |
| Scale | 売上 10 万ドル超で、貢献利益率がプラス | 5 億 6,570 万ドル | 55% | 売上 2 億 9,630 万ドル、68% |
| 全体 | - | 7 億 4,260 万ドル | 21% | 48%(2020 年上期の全体) |

- 段階は年末に、その年の数字で決める。顧客の評価は翌年の売上で見る(S-1)。
- S-1 は「Acquire の後に長い Expand が続く顧客もいれば、Expand を飛ばして Scale に行く顧客もいる」と書く。顧客は業界でなく、1 社ずつ管理する(出典: S-1、見た日 2026-11-18)。
- Scale の顧客は自分でアプリを作るようになり、Palantir の投資は売上に比べて減る、と書く(出典: 同上)。

### 最初の試験の費用を会社が持つ

- S-1 は、Acquire では短い試験を「無料か低額で」行い、その間は赤字で運営すると書く(「short-term pilot deployments of our software platforms at no or low cost to them」)(出典: S-1、見た日 2026-11-18)。
- 試験は「多くは自社の費用で、将来の見返りの保証なしに」行う、と書く(「generally at our own expense and without a guarantee of future returns」)(出典: 同上)。
- 試験が成功しても、大きな契約にならないことがある、とリスクに書く。販売の期間は 6〜9 か月が多く、1 年以上もある(出典: 同上)。
- FY2025 の 10-K も同じ文を、試験とブートキャンプの両方に使う(「We conduct pilots and bootcamps with customers, generally at our own expense」)(出典: https://www.sec.gov/Archives/edgar/data/1321655/000132165526000011/pltr-20251231.htm、見た日 2026-11-18)。

### 2020 年の顧客の段階(FY2021 の 10-K)

| 段階 | 2020 年の売上 | 2020 年の貢献利益 | 同じ顧客の 2021 年 |
|---|---|---|---|
| Acquire | 30 万ドル | 3,680 万ドルの損失 | 売上 4,510 万ドル、720 万ドルの利益 |
| Expand | 2,030 万ドル | (159)% | 売上 8,330 万ドル、45% |
| Scale | 11 億ドル | 63% | 売上 13 億ドル、63% |

- 出典: https://www.sec.gov/Archives/edgar/data/1321655/000119312522050913/d273589d10k.htm、見た日 2026-11-18。どれも非 GAAP。
- FY2022 以降の 10-K には「Acquire phase」の語がない(自分で本文を検索した。FY2022、FY2023、FY2025 で 0 件)。段階の数字は FY2021 の 10-K が最後だ。

### 今の貢献利益(区分は政府と民間)

| 期 | 政府 | 民間 | 全体 | 出典 |
|---|---|---|---|---|
| FY2023 | 59% | 52% | 56% | 10-K FY2025 |
| FY2024 | 60% | 60% | 60% | 10-K FY2025 |
| FY2025 | 66% | 66% | 66% | 10-K FY2025 |
| 2026 年 Q3 | 70% | 77% | 73% | 10-Q 2026 年 Q3 |

- どれも非 GAAP(株式報酬を除く)。出典: https://www.sec.gov/Archives/edgar/data/1321655/000132165526000011/pltr-20251231.htm と https://www.sec.gov/Archives/edgar/data/1321655/000132165526000048/pltr-20260930.htm、見た日 2026-11-18。

## 4. AIP のブートキャンプ

### いつ始めたか

- FY2023 の 10-K は「2023 年に AIP ブートキャンプを入れた」と書く。顧客の実データで、数日で実際の業務の流れを届ける、という説明だ(「deliver real workflows on actual customer data in days」)(出典: https://www.sec.gov/Archives/edgar/data/1321655/000132165524000022/pltr-20231231.htm、見た日 2026-11-18)。
- 2023 年 Q4 の決算説明会で、Ryan Taylor は「10 月に、1 年で 500 回の目標を立てた」と話した(決算説明会の発言。Motley Fool の書き起こし、出典: https://www.fool.com/earnings/call-transcripts/2024/02/05/palantir-technologies-pltr-q4-2023-earnings-call-t/、見た日 2026-11-18)。
- 2024 年 Q1 の説明会では「2 四半期前に、売り方としてブートキャンプを発表した」と話した(出典: https://www.fool.com/earnings/call-transcripts/2024/05/06/palantir-technologies-pltr-q1-2024-earnings-call-t/、見た日 2026-11-18)。

### 何日で、何をするか

- 公式ページは「0 から使える例まで 5 日」と書く(「customers go from 0 to use case in 5 days」)(出典: https://www.palantir.com/platforms/aip/bootcamp/、見た日 2026-11-18)。
- 同じページは、5 日でやることを 3 つ挙げる。AI を業務にどう使うかを理解する、最初の使い道をソフトの中で作る、利用者を研修して運用に乗せる、だ(出典: 同上)。
- 説明会では、長さは 1〜5 日と話された。「1〜5 日で、以前は 3 か月かかったことをする」(2024 年 Q1、Ryan Taylor)。Karp は「あなたのデータを 10 時間動かす」と話した(2023 年 Q4)(出典: 上の 2 つの書き起こし、見た日 2026-11-18)。
- Karp は 2023 年 Q4 に「2 年前は試験が 92 件だった。2023 年はブートキャンプが 500 回を超えた(多くは下期)」と話した(出典: 2023 年 Q4 の書き起こし、見た日 2026-11-18)。
- 新しい形として AgentCamp がある。会社のページは、帰る前に「本番で動くエージェント」を見せる、と書く。日数は書いていない(出典: https://www.palantir.com/platforms/aip/agentcamp/、見た日 2026-11-18)。

### 何回やったか

| 時点 | 数 | 出典 |
|---|---|---|
| 2023-10 | 「1 年で 500 回」を目標にした | 2023 年 Q4 の説明会(2024-02-05) |
| 2024-02-05 | 560 回超、465 組織 | 同上 |
| 2024-05-06 | 参加した組織が 915 超。回数は言っていない | 2024 年 Q1 の説明会 |

- 2024 年 Q2 より後の回数は見つからなかった。決算の発表(press release)には、2023 年 Q2 から 2026 年 Q3 まで「bootcamp」の語がない(自分で本文を検索した)。
- 契約への転換率は開示されていない。Karp は 2024 年 Q1 に「ブートキャンプは初期の動きで、売り方を解いたとは言わない」と話した(出典: 2024 年 Q1 の書き起こし、見た日 2026-11-18)。

### ブートキャンプから契約までの例(会社の発言)

- 米国のケーブル TV の会社: LinkedIn での飛び込みの連絡から 5 日のブートキャンプへ進み、enterprise agreement を結んだ。約 300 万ドルの契約で、すべて 2023 年 Q4 の中で起きた(Ryan Taylor、2023 年 Q4 の書き起こし、見た日 2026-11-18)。
- 世界最大の通信会社: ブートキャンプで「24 時間で」新しい使い道を出し、既存の契約の数百万ドルの拡大につながった(同上)。
- 大手の電力会社: ブートキャンプを終えて 5 日後に、7 桁ドル(100 万ドル台)の契約を結んだ(Ryan Taylor、2024 年 Q1 の書き起こし、見た日 2026-11-18)。
- 別の顧客: 数日のブートキャンプの 1 日目の後に有償の契約を結び、約 3 週間後に 7 桁ドルの契約にした(同上)。
- 会社名は出ていない。会社の発表(press release)で、ブートキャンプからの契約を名前つきで示したものは見つからなかった。

## 5. オントロジー(業務のデータと操作のモデル)

### 公式の文書の説明

- オントロジーは「組織の運用の層(operational layer)」で、多くの場面で「組織のデジタルツイン」になる(出典: https://www.palantir.com/docs/foundry/ontology/overview/、見た日 2026-11-18)。
- 中身は 2 つに分かれる。意味の側(semantic elements)は objects、properties、links。操作の側(kinetic elements)は actions、functions、dynamic security だ(出典: 同上)。
- オントロジーは「Palantir に取り込んだデジタルの資産の上に載る」。既存のデータソースを objects、properties、links に対応させて作る(「The Ontology sits on top of the digital assets integrated into the Palantir platform」)(出典: 同上)。
- 同じページは、action types で「既存のシステムとつながる意思決定の流れ」を組める、と書く。オントロジーに投資する目的は「組織の意思決定を大きな規模で良くすること」だ、とも書く(出典: 同上)。

### 操作(actions)

- action type は、利用者が一度に行う objects、property、links の変更の定義だ。変更は 1 つのトランザクションとして記録される(出典: https://www.palantir.com/docs/foundry/action-types/overview/、見た日 2026-11-18)。
- action は webhook で外部のシステムへ要求を送れる。文書は例に「Salesforce、SAP」を挙げる(出典: https://www.palantir.com/docs/foundry/action-types/webhooks/、見た日 2026-11-18)。
- 書き戻し(writeback)の webhook が失敗すると、オントロジーの変更もしない。文書はこれを「ある程度のトランザクション性」と呼び、完全ではないとも書く(出典: 同上)。

### AIP との関係

- AIP のページは、オントロジーが AI を 3 つにつなぐと書く。企業のデータ、企業のロジック(業務ルール、ML のモデル、最適化)、行動のシステム(業務のデータベースなど)だ(出典: https://www.palantir.com/platforms/aip/、見た日 2026-11-18)。
- AI が出した案は、人が確かめてから実行できる。すべての操作は監査できる、と書く(出典: 同上)。

### S-1 の説明(2020 年)

- S-1 は、オントロジーを objects(人や出来事)、properties(属性)、relationships(つながり)から作ると書く。Palantir が「種のオントロジー」を渡し、顧客の専門家が自分の業務のモデルを作る(出典: S-1、見た日 2026-11-18)。
- オントロジーから、その業務向けの SDK(DS-SDK)を作る。顧客はそれでオントロジーを使うアプリを作れる(出典: 同上)。
- 専門サービスの中身に「オントロジーとデータのモデルの支援」が入っている。これは FY2025 の 10-K も同じだ(出典: S-1、10-K FY2025、見た日 2026-11-18)。

## 6. 既存のシステムを置き換えずにつなぐ

### 会社の立ち位置

- 10-K は、大きな失敗の例を売り込みの前提に使う。米軍のある部門は ERP を一から作るのに 10 億ドル超を使い、完成せずに中止した、と書く(出典: S-1、10-K FY2025、見た日 2026-11-18)。
- 採用の基準の 1 つに「既存のシステムの中で働く力」がある。顧客のシステムと Palantir の間でデータをやり取りする仕事には、必ず他社の部品が入る、と書く(出典: https://www.palantir.com/careers/getting-hired/working-inside-existing-systems/、見た日 2026-11-18)。

### データをつなぐ仕組み

- Data Connection は、外部のシステムからデータを同期する道具だ。webhook とデータの書き出しで、外部への書き戻しもできる(出典: https://www.palantir.com/docs/foundry/data-connection/overview/、見た日 2026-11-18)。
- 文書のコネクタの一覧は、およそ 200 件ある(目次から数えた目安)(出典: 同上)。
- virtual tables は、外部のシステムの表への「指し示し(pointer)」で、データは元のシステムに残る。対応先は Amazon S3、OneLake、Azure Data Lake Storage Gen2、BigQuery、Databricks、Google Cloud Storage、Snowflake など。計算を元のシステムで行う compute pushdown もある(出典: https://www.palantir.com/docs/foundry/data-integration/virtual-tables/、見た日 2026-11-18)。

### SAP との接続

- SAP 用のコネクタ(Palantir Foundry Connector 2.0 for SAP Applications)は、SAP の上に入れる ABAP のアドオンだ。Diskover Limited と作った(出典: https://palantir.com/docs/foundry/sap/overview/、見た日 2026-11-18)。
- 接続はデータベースでなく SAP のアプリの層(ABAP platform)を通す。下のデータベースの種類によらない。対応は S/4HANA、ECC、Business Warehouse、SLT Replication Server だ(出典: 同上)。
- HyperAuto は、SAP ERP、S/4HANA、Oracle NetSuite、Salesforce などのデータの取り込みを数時間で済ませる、と書く。「高いコンサルの案件を避ける」とも書く(出典: https://www.palantir.com/offerings/hyperauto/、見た日 2026-11-18)。

### 提携(会社のページと発表)

| 相手 | 中身 | 出典 |
|---|---|---|
| SAP | 初の共同開発。SAP ECC から SAP Cloud ERP(RISE with SAP)への移行の間も、HyperAuto を主なコネクタとして残す。SAP Business Data Cloud とオントロジーを双方向でつなぐ | https://www.palantir.com/partnerships/sap/ |
| Databricks | 2025-03-13 に発表。Unity Catalog と Delta Sharing を通じてつなぐ。共通の顧客に国防総省、財務省、保健福祉省、bp | https://www.databricks.com/company/newsroom/press-releases/palantir-and-databricks-announce-strategic-product-partnership |
| Snowflake | Foundry と Snowflake の Iceberg 表で、双方向でコピーなし(zero-copy)の相互運用 | https://www.palantir.com/partnerships/snowflake/ |
| Microsoft | Azure Marketplace で Foundry を買える。Azure の消費の約束(MACC)を Foundry の購入に充てられる | https://www.palantir.com/partnerships/microsoft/ |
| Oracle | クラウドと AI を、各国の規制(主権)の条件に合わせて使う、と書く。具体的な仕組みはページになかった | https://www.palantir.com/partnerships/oracle/ |
| 富士通 | Foundry と AIP を Fujitsu Uvance のデータ基盤に組み込む世界規模の提携(10-K の記載) | 10-K FY2025 |

- 見た日はすべて 2026-11-18。
- Snowflake の提携の発表日(2025-10-16)は、検索結果の見出しで見ただけだ。発表の本文は開けなかった。
- 10-K は、クラウドの会社との提携を「大きな営業の力を持つ相手の顧客基盤に届く道」と書く(出典: 10-K FY2025、見た日 2026-11-18)。

## 7. 契約の形と料金の形

### 売上の種類と契約の長さ

- 売上は 3 種類だ。Palantir がホストするクラウドの利用(Palantir Cloud)、顧客の環境で使うソフトの期間ライセンス(On-Premises Software)、専門サービスだ。どれも契約の期間にわたって均等に計上する(出典: 10-K FY2025、見た日 2026-11-18)。
- 3 種類ごとの売上の内訳は、10-K に開示がない。開示は政府と民間、国別だけだ。
- 契約は多くが 1〜5 年だ。多くの契約は、通知の上で顧客が解約できる(出典: 同上)。
- 2025 年に結んだ契約は、金額で重みをつけた平均で、さらに 4 年売上を生むと見込む(出典: 同上)。
- 2025-12-31 の残りの契約額(remaining deal value)は 112 億ドルで、民間 68 億ドル、政府 44 億ドルだ。多くは任意の解約(termination for convenience)の条項つきだ(出典: 同上)。

### 政府の大きな契約

- 米陸軍は 2025-07-31 に Palantir と enterprise agreement を結んだ。15 の主契約と 60 の関連契約、計 75 を 1 つにまとめた(出典: https://www.army.mil/article/287506/、見た日 2026-11-18)。
- 期間は最長 10 年で、上限は 100 億ドルだ。陸軍は「上限で、約束の額ではない」と書く(出典: 同上)。
- 量に応じた割引があり、契約会社と再販会社の上乗せの手数料をなくす。必要な時に必要な分を買え、国防総省のほかの機関も使える(出典: 同上)。
- 10-K は、米政府が商用品を優先して買う法律(FASA)を挙げ、Palantir は「商用品とサービスを売り、受託開発はしない」と書く(出典: 10-K FY2025、見た日 2026-11-18)。

### 使用量の課金

- 10-K は、価格の形として「サブスクリプションか使用量の課金」を試していると書く(リスクの記載)(出典: 10-K FY2025、10-Q 2026 年 Q3、見た日 2026-11-18)。
- 公式の文書は、計算を compute-seconds で計る。オントロジーと保存の量はギガバイト月で計る(出典: https://www.palantir.com/docs/foundry/resource-management/usage-types/、見た日 2026-11-18)。
- 予算の機能は「使用量の契約(usage-based contract)を結んでいる顧客だけ」が使える、と書く。つまり使用量の契約は実在する(出典: https://palantir.com/docs/foundry/resource-management/budgets/、見た日 2026-11-18)。
- compute-second の単価は見つからなかった。

### 無料の試験と AIP の料金

- 試験とブートキャンプは、無料か低額で、会社の費用で行う(3 節を参照)。
- Developer Tier は「大きな初期費用なしに」Foundry と AIP を試せる、と書く(出典: 10-K FY2025、見た日 2026-11-18)。金額は見つからなかった。
- AIP の価格表は見つからなかった。公式サイトの地図(sitemap、627 ページ)に料金のページはなかった(自分で確かめた)。

## 8. 導入から広がるまでの流れと数字

### 広げ方(会社の説明)

- S-1 と FY2025 の 10-K は、顧客の中で広げる方法を 3 つ挙げる。顧客の取引先まで広げる、業界をまたぐ製品を足して売る、特定の使い道の実装を売る、だ(出典: S-1、10-K FY2025、見た日 2026-11-18)。
- 広げる向きは 2 つある。横は別の部門や機能、縦は利用者の数だ。「一番難しい問題を先に解いて信頼を得てから、全社に広げる」と書く(出典: 同上)。
- ブートキャンプの後の型として、Ryan Taylor は「ブートキャンプに来て、すぐに enterprise の契約を結ぶ新しい顧客」を最初に挙げた(2023 年 Q4 の書き起こし、見た日 2026-11-18)。

### 数字

| 指標 | 値 | 期と区分 | 出典 |
|---|---|---|---|
| 上位 20 社の平均の売上 | 2,480 万ドル | 2019 年(GAAP の売上) | S-1 |
| 上位 20 社の売上の割合 | 67%(4 億 9,520 万ドル)。平均の付き合いは 6.6 年 | 2019 年 | S-1 |
| 上位 20 社の平均の売上 | 6,460 万ドル → 9,390 万ドル(+45%) | 2024 年 → 2025 年の 12 か月 | 10-K FY2025 |
| 上位 20 社の平均の売上 | 8,300 万ドル → 1 億 4,600 万ドル(+76%) | 2025-09 → 2026-09 までの 12 か月 | 10-Q 2026 年 Q3 |
| 顧客数 | 125 | 2020 年上期 | S-1 |
| 顧客数 | 711 → 954 | 2024 年 → 2025 年の 12 か月 | 10-K FY2025 |
| 顧客数 | 911 → 1,090 | 2025-09 → 2026-09 までの 12 か月 | 10-Q 2026 年 Q3 |
| net dollar retention | 108% | 2023 年 Q4 | 2023 年 Q4 の説明会(CFO) |
| net dollar retention | 111% | 2024 年 Q1 | 2024 年 Q1 の説明会(CFO) |
| net dollar retention | 165%(前の四半期から 800bp 上昇) | 2026 年 Q3 | 解説(Futurum) |
| 米国の民間の残りの契約額 | 65 億 1,700 万ドル(+79%) | 2026-09-30 | 決算の発表 2026 年 Q3 |
| 100 万ドル以上の契約 | 212 件(500 万ドル以上 107 件、1,000 万ドル以上 64 件) | 2026 年 Q3 | 決算の発表 2026 年 Q3 |
| 売上 | 23 億 1,340 万ドル(+96%、GAAP) | 2026 年 Q3 | 決算の発表 2026 年 Q3 |

- 出典の URL(見た日はすべて 2026-11-18):
  - S-1: https://www.sec.gov/Archives/edgar/data/1321655/000119312520230013/d904406ds1.htm
  - 10-K FY2025: https://www.sec.gov/Archives/edgar/data/1321655/000132165526000011/pltr-20251231.htm
  - 10-Q 2026 年 Q3: https://www.sec.gov/Archives/edgar/data/1321655/000132165526000048/pltr-20260930.htm
  - 決算の発表 2026 年 Q3: https://www.sec.gov/Archives/edgar/data/1321655/000132165526000045/a2026q3ex991pressrelease.htm
  - 2023 年 Q4 の説明会: https://www.fool.com/earnings/call-transcripts/2024/02/05/palantir-technologies-pltr-q4-2023-earnings-call-t/
  - 2024 年 Q1 の説明会: https://www.fool.com/earnings/call-transcripts/2024/05/06/palantir-technologies-pltr-q1-2024-earnings-call-t/
  - Futurum: https://futurumgroup.com/?p=97554(2026-11-05 の記事)
- 顧客は「過去 12 か月に売上を計上した組織」と定義する。政府の機関は、別に契約して請求する部署ごとに 1 社と数える(出典: 10-K FY2025)。
- CFO は、net dollar retention が「過去 12 か月に取った新しい顧客の売上を含まない」と話した(2023 年 Q4 の書き起こし)。Futurum は 165% を「会社の定義の指標」と書く。会社の投資家向け資料は開けていないので、165% は会社の資料で確かめていない。
- 2026 年 Q3 は、米国の民間の売上(9 億 8,400 万ドル)が、初めて米国の政府の売上(9 億 5,300 万ドル)を上回った(出典: 決算の発表 2026 年 Q3)。

## 9. 型の弱みと批判

### 会社自身が書くリスク

- 試験とブートキャンプは、売上にならないことがある。FY2025 の 10-K は、ブートキャンプなど短い形を入れたが「売上がないか、わずかに終わる」ことがある、と書く(出典: 10-K FY2025、見た日 2026-11-18)。
- 販売の期間は 6〜9 か月が多い。営業は経営陣の深い関与に頼ってきた、と書く(出典: S-1、10-K FY2025、見た日 2026-11-18)。
- S-1 は、FDE の配置を「短期の貢献利益を下げても」続けると書く(2 節)。人を先に入れる型は、費用が先に出る。

### 数字で見る費用の重さ

| 期 | 販売費 | 売上に占める販売費 | 貢献利益率 | 出典 |
|---|---|---|---|---|
| 2019 年 | 4 億 5,010 万ドル | 61% | 21% | S-1 |
| 2025 年 | 10 億 5,690 万ドル | 24% | 66% | 10-K FY2025 |
| 2026 年 Q3 | 3 億 9,670 万ドル | 17% | 73% | 10-Q 2026 年 Q3 |

- 販売費は GAAP(株式報酬を含む)。割合は自分で計算した。貢献利益率は非 GAAP。
- 2019 年の純損失は 5 億 7,960 万ドル(GAAP)だった(出典: S-1、見た日 2026-11-18)。
- 粗利益率は 2025 年が 82%(GAAP、自分で計算)、株式報酬を除くと 84% だ(出典: 10-K FY2025)。2026 年 Q3 は 83%(GAAP、自分で計算)だ(出典: 10-Q 2026 年 Q3)。
- 推測: 1 人あたりの売上は、2019 年の約 31 万ドル(人数は 2020-06-30 の 2,398 人で割った目安)から、2025 年の約 101 万ドル(2025-12-31 の 4,429 人)に上がった。人数の基準日が違うので目安だ。2026-09-30 の正社員は 4,634 人だ(出典: S-1、10-K FY2025、10-Q 2026 年 Q3)。

### 批判(報道と解説)

- 元社員の Nabeel Qureshi は、2024 年以前の Palantir は「ソフトの皮をかぶったコンサル」と見下されていた、と書く(「dismissed as a consulting company masquerading as software」)。試験の 8〜12 週をデータへのアクセスを得るだけに使ったこともある、と書く(解説、出典: https://nabeelqu.substack.com/p/reflections-on-palantir、見た日 2026-11-18)。
- 同じ文章は、反論として 2023 年の粗利益率 80% を挙げ、Accenture の 32% と比べる(解説、出典: 同上)。
- a16z の Marc Andrusko は、Palantir の型をまねる会社への注意を書いた(2026-01-16)。共通の基盤がないと「保守も更新もできない、何千もの特注の導入」になる。「ソフトの評価倍率がついた高いサービス業」になる、という指摘だ(解説、出典: https://www.a16z.com/the-palantirization-of-everything、見た日 2026-11-18)。
- 同じ記事は、Palantir の型が頼る人材(技術が深く、顧客にも強い人)は珍しく、多くの会社は大量に雇えない、とも書く(解説、出典: 同上)。
- Futurum は、2026 年 Q3 について、契約が短いと顧客の「出口が増える」、米国の政府と米国の企業の AI 支出に偏る、と書く(解説、出典: https://futurumgroup.com/?p=97554、見た日 2026-11-18)。
- 推測: 「人が多いと粗利が下がる」という批判は、今の Palantir の数字には当たりにくい。FDE の費用の多くは粗利の下の販売費に入り、その販売費の割合は大きく下がったからだ。ただし Palantir は、FDE の人件費や、ブートキャンプの費用の総額を開示していない。

## 見つからなかったこと

- FDE の人数、顧客 1 社あたりの FDE の人数。S-1 と 10-K に開示がない。4〜5 人という数は元社員の文章だけだ。
- FDE の人件費の総額と、売上原価と販売費への分け方の数字。
- FY2022 以降の、段階(Acquire、Expand、Scale)ごとの数字。FY2021 の 10-K が最後だった。
- 2024 年 Q2 より後のブートキャンプの回数。ブートキャンプから契約への転換率。会社の発表で、ブートキャンプからの契約を会社名つきで示した例。
- 株主への手紙(CEO の手紙)でのブートキャンプの回数。手紙のページは本文を読み取れなかった。
- AIP の価格表。compute-second の単価。Developer Tier の金額。
- 売上の内訳(Palantir Cloud、On-Premises Software、専門サービス)。10-K は政府と民間、国別しか開示していない。
- net dollar retention の会社の資料(投資家向け資料)。165% は解説の記事、108% と 111% は説明会の書き起こしで確かめた。
- Warp Speed の会社の発表の本文と、10-K での記載(FY2025 の 10-K に名前がない)。
- Microsoft と Oracle の提携の発表日と、契約の中身。Snowflake の提携の発表の本文。
- 公式ブログ「Dev versus Delta」の本文。Delta と Echo の役割の公式の定義は、求人の区分の表示でしか確かめていない。
- 開けなかったページ:
  - blog.palantir.com/dev-versus-delta-demystifying-engineering-roles-at-palantir-ad44c2a6e87(403、Cloudflare の確認画面)
  - web.archive.org の上のブログの写し(429)
  - snowflake.com の提携の発表(403)
  - businesswire.com の Warp Speed の発表(403)
  - nabeelqu.co/reflections-on-palantir(429。substack の同じ文章で代わりに読んだ)
  - investors.palantir.com/news-events/press-releases(本文が取れなかった)
  - palantir.com/docs/foundry/available-connectors/sap/(404)
  - barchart.com の Snowflake の発表の転載(本文が空)
  - palantir.com/platforms/ontology/ と palantir.com/newsroom/letters/(本文を読み取れなかった)
