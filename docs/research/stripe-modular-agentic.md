# Stripe のモジュール化と agentic な製品設計: hiring-os に使えるもの

## 結論

- 運営者が見た「2026-10-26 の Stripe の agentic design のセミナー」の公開資料は見つからなかった。いちばん近い公開資料は Stripe Sessions 2026(2026-04-28〜30)の Developer keynote。
- Stripe は「部品を単独でも組み合わせでも使える」形を、決済の外の部品(Billing、Radar、Connect)にまで広げてきた。エージェント向けの道具も同じ形で出している。
- 権限の設計は 3 段になっている。権限を絞った鍵(制限付き API キー)、エージェント用の印をつけた鍵、重要な操作の前の二者承認(承認ルール)。bot に権限を渡す hiring-os の設計にほぼそのまま使える。
- 支払いの権限は、相手・金額・期限を絞った使い捨てのトークン(Shared Payment Token)で渡す。求職者の bot が企業に「見てよいデータ」を渡す形の手本になりそうだ(推測)。
- Stripe は「エージェントは考え、支払いはコードがする」と述べている。決定論的な道具とワークフローの上でエージェントを動かす考え方だ。自然言語は設計の入口で、実行は決まった定義で行う形が合いそうだ(推測)。
- 注意点が 2 つある。ChatGPT の Instant Checkout は 2026-03 に縮小したと報じられている。SPT と Link Agent Wallet は日本では使えない。

## 1. 2026-10-26 のセミナーの公開資料

見つからなかった。以下を探した。

| 探した場所 | 結果 | 出典 | 見た日 |
| --- | --- | --- | --- |
| Stripe のイベントのページ | stripe.com/jp/events は stripe.events に転送され、403 で開けなかった | https://stripe.com/jp/events | 2026-11-11 |
| Stripe Tour Tokyo 2026 | 開催日は 2026-09-30 で、10-26 ではない。16:15 からの「エージェントコマースの全貌」というセッションがある。登壇は Mercari、Stripe Japan、Stripe の Emily Sands | https://www.sbbit.jp/fj/eventinfo/89957 | 2026-11-11 |
| Stripe Tour Tokyo の公式ページ | stripe.com/jp/tour/tokyo は 404 だった | https://stripe.com/jp/tour/tokyo | 2026-11-11 |
| Web 検索(10 月 26 日、セミナー、webinar、YouTube、JP_Stripes、connpass) | 10-26 の Stripe のイベントは出てこなかった | なし(検索結果のみ) | 2026-11-11 |

代わりに、公開されているいちばん近い資料を使った。Stripe Sessions 2026 の Developer keynote(題「Advancing developer craft」)だ。登壇は Michelle Bu と Nilofer Rajpurkar。Sessions 2026 は 2026-04-28〜30 にサンフランシスコで開かれた（出典: https://stripe.com/sessions/2026/developer-keynote、見た日 2026-11-11）。

この keynote は、エージェントを強くする方法を 3 つ挙げている（出典: https://stripe.com/sessions/2026/developer-keynote、見た日 2026-11-11）。

- 賢くする: 製品をエージェントに読める形にする。どのドキュメントの URL も `.md` をつければ Markdown で読める。
- できることを増やす: 決定論的な道具(MCP、CLI、Workflows)を渡す。
- 信頼できるようにする: 暴走を防ぐ「ガードレール」を置く。高額の返金などは人が承認する。

デモでは、$50 の返金はそのまま通った。$250 の返金は承認ルールで止まり、エージェントが承認を申請した。人が承認すると、Workflows が Slack に通知し、フォローアップの記録を作った（出典: https://stripe.com/sessions/2026/developer-keynote、見た日 2026-11-11）。

Stripe によると、2025 年に Stripe のドキュメントへのエージェントのアクセスは 5% 未満から 40% 近くに増えた（会社の発表）（出典: https://stripe.com/sessions/2026/developer-keynote、見た日 2026-11-11）。

## 2. 項目ごとのまとめ

| 項目 | 何か | 提供の段階(2026-11 時点で確かめられたもの) | 権限とデータの扱い | 出典 | 見た日 |
| --- | --- | --- | --- | --- | --- |
| 製品のモジュール化 | Billing、Radar、Connect などを単独で使え、他社の決済とも組み合わせられる | 一般提供(Radar のリスクスコアの API は 2025-05 時点で提供中) | 部品ごとに API が分かれる | https://stripe.com/blog/biggest-updates-sessions-2024 | 2026-11-11 |
| API の版の管理 | 日付で名づけた版。アカウントごとに版を固定する | 一般提供(2017 年からの方式) | ヘッダーで 1 回ごとに版を変えられる | https://stripe.com/blog/api-versioning | 2026-11-11 |
| 冪等キー | 再送しても同じ操作が 2 回起きない | 一般提供 | v1 では 24 時間以上たったキーは消してよい | https://docs.stripe.com/api/idempotent_requests | 2026-11-11 |
| Webhook / イベント | 状態の変化を外へ送る。署名つき | 一般提供 | 署名の検証、最長 3 日の再送、順序は保証しない | https://docs.stripe.com/webhooks.md | 2026-11-11 |
| 制限付き API キー(RAK) | 資源ごとに None / Read / Write を選べる鍵 | 段階の表示なし(通常の機能として説明) | AI エージェントに渡す鍵として推奨 | https://docs.stripe.com/keys/restricted-api-keys | 2026-11-11 |
| エージェント用の鍵 | RAK に「エージェント」の印をつける | 段階の表示なし。Sessions 2026 では「Agent guardrails」をプレビューと発表 | 承認ルールが自動でかかる | https://docs.stripe.com/keys.md | 2026-11-11 |
| 承認ルール | 重要な操作を止め、指定した人の承認を待つ | 段階の表示なし。v2 の API の版は preview の番号 | 金額、実行者、回数の条件で止める | https://docs.stripe.com/account/approvals.md | 2026-11-11 |
| Stripe MCP サーバー | エージェントが Stripe の API を使う道具 | 提供中(一部の道具はプレビュー) | OAuth かエージェント用の鍵。12 月から全権の鍵は使えない | https://docs.stripe.com/mcp.md | 2026-11-11 |
| Agent Toolkit | エージェントのフレームワーク向けの SDK | 廃止(更新もセキュリティ修正もない) | MCP サーバーに移る | https://github.com/stripe/ai | 2026-11-11 |
| Sandboxes | 本番から分けた試しの環境 | 一般提供。Claimable Sandboxes API は提供中、本番の鍵の自動交換はプレビュー | 外部の人をサンドボックスだけに招ける | https://docs.stripe.com/sandboxes.md | 2026-11-11 |
| Stripe Workflows | ノーコードで多段の処理を組む | 一般提供。ループ、カスタムアクションなどはプレビュー | Connect の連結アカウントにも使える | https://stripe.com/blog/everything-we-announced-at-sessions-2026 | 2026-11-11 |
| Custom Objects | 独自のデータの型を Stripe に定義する | プライベートプレビュー | 1 アカウントの中だけで使える | https://docs.stripe.com/custom-objects.md | 2026-11-11 |
| Stripe Apps | ダッシュボードを拡張するアプリ | 一般提供。フルページのアプリはプレビュー | マニフェストで権限と理由を宣言し、導入時に同意を得る | https://docs.stripe.com/stripe-apps/reference/permissions.md | 2026-11-11 |
| Dashboard assistant | ダッシュボードで自然言語で操作する | 2025-05 に提供開始(会社の発表) | 作成などの操作をして、人が確かめる | https://docs.stripe.com/assistant.md | 2026-11-11 |
| Stripe Projects | 外部サービスをエージェントが CLI で用意する | 提供中(Sessions 2026) | 認証情報を暗号化して保存し、`.env` に同期する | https://docs.stripe.com/projects.md | 2026-11-11 |
| Agentic Commerce Protocol(ACP) | 買い手、AI エージェント、事業者の間の開かれた規格 | 公開(Apache 2.0) | 事業者が売り手(merchant of record)のまま | https://www.agenticcommerce.dev/ | 2026-11-11 |
| Shared Payment Token(SPT) | 相手・金額・期限を絞った支払いの権限 | Sessions 2026 で「提供中」。発行側の規約名は preview。対象は米国、カナダ、欧州の一部 | 取り消せる。状態の変化を Webhook で知らせる | https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens.md?agent-seller=agent | 2026-11-11 |
| Instant Checkout(ChatGPT) | ChatGPT の中で買い物を終える | 2025-09-29 に米国で開始。2026-03 に縮小と報道。今の状態は不明 | 支払いは SPT で渡す | https://stripe.com/newsroom/news/stripe-openai-instant-checkout | 2026-11-11 |
| Link Agent Wallet | エージェントが利用者の承認を得て支払う | 提供中。支払いは米国とカナダ、金融データは米国のみ | 利用者 1 人ごとの OAuth のトークン | https://docs.stripe.com/agentic-commerce/agents/link-agent-wallet.md | 2026-11-11 |

## 3. 製品の組み立て(モジュール化)

### 何か

- Stripe は Sessions 2024 で Connect を「よりモジュール化した」と発表した。どの機能を自社で持ち、どれを Stripe に任せるかを選べる（出典: https://stripe.com/blog/biggest-updates-sessions-2024、見た日 2026-11-11）。
- 同じ発表で、Payment Element を他社の決済代行(PSP)と使えるようにした。Billing と Radar も他社の決済と組めるようにすると予告した（出典: https://stripe.com/blog/biggest-updates-sessions-2024、見た日 2026-11-11）。
- 理由として「既存の技術の構成に合うよう、もっとモジュール化してほしいという声」を挙げている（出典: https://stripe.com/blog/biggest-updates-sessions-2024、見た日 2026-11-11）。
- 2024-10 には、Radar を自社の不正対策や複数の決済の構成と組めるようにした。Stripe のサブスクも、他社で処理した取引に対応した（出典: https://stripe.com/blog/our-top-product-updates-from-stripe-tour-ny、見た日 2026-11-11）。
- 2025-05 には、複数の決済代行を管理する Stripe Orchestration をプレビューで出した（出典: https://stripe.com/blog/top-product-updates-sessions-2025、見た日 2026-11-11）。
- エージェント向けでも同じ形だ。開発の道具、AI の課金、エージェントの売買の 3 部品を「単独でも組み合わせでも」使える（出典: https://docs.stripe.com/agents/how-it-works.md、見た日 2026-11-11）。

### このプロダクトへの使い方

- 推測: 採用の流程を、独立して使える部品に分ける。たとえば、求人の公開、応募の受付、書類の選考、面接の日程、評価、内定、入社の手続きの部品だ。
- 推測: 各部品は、他社の ATS や求人媒体と組めるようにする。Stripe が他社の決済と Radar を組めるようにした形と同じだ。中小企業は全部を使い、大企業は既存の ATS を残して一部だけ使える。
- 推測: 部品の境目を API とイベントで決めておく。そうすれば、自然言語で流程を組むときも、部品の組み合わせの問題に落とせる。

## 4. API の設計の原則

| 原則 | 何か | 出典 | 見た日 | このプロダクトへの使い方 |
| --- | --- | --- | --- | --- |
| 日付の版と固定 | 版は公開した日で名づける。最初の要求でアカウントの版を固定する。`Stripe-Version` ヘッダーで 1 回ごとに変えられる。古い版との差は「版の変更モジュール」に閉じこめ、新しい形から古い形へ変換する | https://stripe.com/blog/api-versioning | 2026-11-11 | 推測: 企業の bot と求職者の bot の間のやり取り(A2A)の形に使う。相手ごとに版を固定すれば、片方が変わっても壊れない |
| 冪等キー | 同じキーでの再送は、最初の結果を返す。引数が違えばエラーにする。v1 では 24 時間以上たったキーは消してよい | https://docs.stripe.com/api/idempotent_requests | 2026-11-11 | 推測: bot は失敗すると再送しがちだ。応募、面接の確定、内定の送付には必ず冪等キーを求める。二重の内定や二重の応募を防げる |
| Webhook とイベント | 署名(HMAC-SHA256)をつけて送る。本番では最長 3 日、再送する。順序は保証しない。同じイベントが何度も届きうるので、イベント ID で重複を除く | https://docs.stripe.com/webhooks.md | 2026-11-11 | 推測: 「応募が来た」「面接が確定した」などをイベントにする。bot も人の画面も同じイベントで動かす |
| ID でつなぐオブジェクトと `expand` | どのオブジェクトにも ID がある。関連は ID で持つ。`expand` で 1 回の呼び出しで中身まで取れる。深さは 4 段まで | https://docs.stripe.com/expand.md | 2026-11-11 | 推測: 求人、応募者、応募、面接、評価をそれぞれオブジェクトにして ID でつなぐ。bot は必要な分だけ展開して読む |
| 構造化したエラー | 承認が必要な操作には `approval_required` を返す。予約の例では `409` と `slot_unavailable` を返し、エージェントが別の枠を探せるようにする | https://docs.stripe.com/agentic-commerce/sellers/use-cases/booking.md | 2026-11-11 | 推測: 「この候補者は他社で内定承諾済み」「この枠は埋まった」などを、bot が読めるコードで返す |

## 5. 権限の設計(bot に渡す鍵)

### 制限付き API キー(RAK)

- 資源ごとに None、Read、Write を選ぶ。初めはすべて None だ（出典: https://docs.stripe.com/keys/restricted-api-keys、見た日 2026-11-11）。
- Stripe は「AI エージェントに渡す鍵は RAK を推奨する」と書いている。全権の秘密鍵ではなく、常に RAK を使うよう勧めている（出典: https://docs.stripe.com/keys/restricted-api-keys、見た日 2026-11-11）。
- サービスごとに別の RAK を作るよう勧めている。1 つが漏れても被害が小さくて済む（出典: https://docs.stripe.com/keys/restricted-api-keys、見た日 2026-11-11）。
- 鍵には、使ってよい IP、ASN、国を決めるアクセスポリシーをつけられる（出典: https://docs.stripe.com/keys.md、見た日 2026-11-11）。

### エージェント用の鍵と承認ルール

- RAK を作るときに「エージェントのアクセス」として印をつけられる。認証と権限は普通の RAK と同じだ。違いは管理の面にある。印のついた鍵には承認ルールが自動でかかる（出典: https://docs.stripe.com/keys.md、見た日 2026-11-11）。
- 承認ルールが動くと、操作は止まり、承認の申請ができる。指定した人が承認すれば操作は自動で終わる。拒否すれば何も変わらない。14 日で期限が切れる（出典: https://docs.stripe.com/account/approvals.md、見た日 2026-11-11）。
- 条件は 3 種類ある。金額、実行者(人かエージェント用の鍵か)、一定時間の回数だ（出典: https://docs.stripe.com/account/approvals.md、見た日 2026-11-11）。
- エージェント用の鍵には、返金、サブスクの解約、入金などに初めから承認ルールがかかっている（出典: https://docs.stripe.com/account/approvals.md、見た日 2026-11-11）。
- エージェントが止められると `approval_required` のエラーが返り、申請が自動で出る。エージェントは理由を書き足せる（出典: https://docs.stripe.com/account/approvals.md、見た日 2026-11-11）。
- 1 人だけのアカウントでは、エージェント用の鍵を条件にした承認ルールだけを保存できる。エージェントは管理者とは別の実行者だからだ（出典: https://docs.stripe.com/account/approvals.md、見た日 2026-11-11）。

### MCP サーバーの認証

- 認証は 2 通りある。人の権限で使うなら OAuth。人と離れて動き続けるなら、エージェント用の鍵を使う（出典: https://docs.stripe.com/mcp.md、見た日 2026-11-11）。
- OAuth では、本番とサンドボックスのどれに入れるかを選び、環境ごとに権限を変えられる。管理者はチーム全体の MCP の利用を止められる。他の人のセッションも取り消せる（出典: https://docs.stripe.com/mcp.md、見た日 2026-11-11）。
- 2026-12 から、Stripe MCP は全権の秘密鍵と、印のない RAK を受けつけなくなる。移行の期限は 2026-11-30（出典: https://docs.stripe.com/mcp.md、見た日 2026-11-11）。
- 返金の作成などには「人による確認」の印がついている。人がダッシュボードで承認すると、エージェントに承認のトークンが渡る。24 時間で期限が切れる（出典: https://docs.stripe.com/mcp.md、見た日 2026-11-11）。
- Stripe は、他の MCP サーバーと併用するときのプロンプトインジェクションに注意するよう書いている（出典: https://docs.stripe.com/mcp.md、見た日 2026-11-11）。

### Stripe Apps の権限

- アプリは、マニフェストの `permissions` に権限を並べる。権限ごとに「なぜ要るか」を書き、導入するときに利用者に見せる。利用者が同意しないと使えない（出典: https://docs.stripe.com/stripe-apps/reference/permissions.md、見た日 2026-11-11）。

### このプロダクトへの使い方

- 推測: 企業の採用 bot には、資源ごとに読み書きを分けた鍵を渡す。たとえば「応募者: 読み取り」「面接の枠: 書き込み」「給与の情報: なし」のようにする。
- 推測: bot には印をつけ、人と別の実行者として扱う。不採用の通知、内定の送付、給与の提示などは、初めから承認ルールで止める。中小企業で担当が 1 人でも、bot と人の二者承認が成り立つ。
- 推測: 「普段は簡単に見られないデータ」への入口は、OAuth(担当者の権限の範囲)と bot 用の鍵(担当者と離れて常に動く)に分ける。どちらも、環境ごと、相手先ごとに取り消せるようにする。
- 推測: 求職者のアシスタントにも同じ形を使う。権限は「求職に関係する資源」だけで、初めはすべて「なし」。入れるデータの種類と理由をマニフェストのように見せ、同意を得る。汎用アシスタントとの違いを、この「見えない範囲が決まっている」点で示せる。
- 推測: Stripe が全権の鍵を MCP から締め出したのと同じく、hiring-os でも bot が全権で動く道を最初から作らない。

## 6. エージェント向けの道具

### Stripe MCP サーバー

- `https://mcp.stripe.com` にある、リモートの MCP サーバーだ。API の検索、読み取り、書き込み、ドキュメントの検索などの道具がある（出典: https://docs.stripe.com/mcp.md、見た日 2026-11-11）。
- 道具の数を絞り、`stripe_api_read` と `stripe_api_write` から多くの API を呼べるようにしている。文脈の長さを増やさずに、API の大部分を使えるという（出典: https://docs.stripe.com/mcp.md、見た日 2026-11-11）。
- Connect の運営者は、`Stripe-Account` ヘッダーで連結アカウントとして呼べる。このとき OAuth は使えず、エージェント用の鍵を使う（出典: https://docs.stripe.com/mcp.md、見た日 2026-11-11）。
- 推測: hiring-os も、外の bot 向けに MCP サーバーを出す。道具は「検索」「読み取り」「書き込み」のように少なくまとめる。人の確認が要る操作には印をつける。

### Agent Toolkit

- `@stripe/agent-toolkit` と `stripe-agent-toolkit` は廃止された。今後は更新もセキュリティ修正もない。代わりに MCP を使うよう書いている（出典: https://github.com/stripe/ai、見た日 2026-11-11）。
- 推測: フレームワークごとの SDK より、MCP と CLI のような共通の入口に寄せる流れだ。hiring-os も個別の SDK より MCP を先に作るほうがよい。

### エージェントに読める資料(スキル、`.md`)

- docs.stripe.com のどの URL も `.md` をつければ Markdown で読める。スキルの一覧は機械が読める索引として公開している（出典: https://docs.stripe.com/agents.md、見た日 2026-11-11）。
- keynote によると、エージェントは古い連携の方法を勧めがちだった。スキルと MCP の道具を使うと、正しい方法を選んだ（出典: https://stripe.com/sessions/2026/developer-keynote、見た日 2026-11-11）。
- 推測: hiring-os でも、採用の流程の部品と使い方を、エージェントが読める形で公開する。

### Sandboxes

- 本番から分けた試しの環境だ。外部の人を、本番のデータに触れさせずにサンドボックスだけに招ける（出典: https://docs.stripe.com/sandboxes.md、見た日 2026-11-11）。
- コーディングエージェントは `stripe sandbox create` で、登録なしに匿名のサンドボックスと鍵を用意できる（出典: https://docs.stripe.com/sandboxes.md、見た日 2026-11-11）。
- Sessions 2026 では、Claimable Sandboxes API を提供中と発表した。AI のパートナーが Stripe を組みこむためのものだ。本番の鍵の自動交換はプレビューだ（出典: https://stripe.com/blog/everything-we-announced-at-sessions-2026、見た日 2026-11-11）。
- 推測: 自然言語で組んだ採用の流程は、まずサンドボックスで架空の応募者を流して試す。確かめてから本番に出す。

### Stripe Projects

- ホスティング、データベース、認証などの外部サービスを、CLI で用意して管理する。60 以上の提供者がある。認証情報は暗号化して保存し、`.env` に同期する（出典: https://docs.stripe.com/projects.md、見た日 2026-11-11）。
- 提供者は Stripe と共同で設計した手順に従う。用意、プランの選択、更新、認証情報の受け渡しをそろえている（出典: https://docs.stripe.com/projects.md、見た日 2026-11-11）。
- エージェントも人と同じ CLI を使う。「決定論的で監査できる道」を通ると書いている。エージェント向けの決まりとして「環境変数の値は見せず、名前だけ見せる」とある（出典: https://docs.stripe.com/projects.md、見た日 2026-11-11）。
- 有料プランの支払いは SPT にして提供者に渡す。元の支払い手段は共有しない。提供者ごとに支出の上限を決められる（出典: https://docs.stripe.com/projects.md、見た日 2026-11-11）。
- 推測: 求人媒体や人材紹介会社を「提供者」とみなす形に使える。企業の bot が、共通の手順で媒体への掲載を用意し、予算の上限を守り、認証情報を受け渡す。

### Dashboard assistant

- ダッシュボードで自然言語でアカウントを操作できる。「35 ドルの商品を作って」と頼めば、assistant が作り、人が確かめる。複数の手順もまとめてこなす（出典: https://docs.stripe.com/assistant.md、見た日 2026-11-11）。
- 2025-05 に「自然言語でダッシュボードの作業ができる」と発表した（出典: https://stripe.com/blog/top-product-updates-sessions-2025、見た日 2026-11-11）。
- Workflows を自然言語で作れるかは、見つからなかった。Workflows の文書はビジュアルビルダーとして説明している（出典: https://docs.stripe.com/workflows.md、見た日 2026-11-11）。

## 7. ノーコードの流程と拡張

### Stripe Workflows

- ダッシュボードのビジュアルビルダーで、コードを書かずに多段の処理を組む。起点は 3 種類ある。Stripe のイベント、決まった日時、ダッシュボードか API からの呼び出しだ（出典: https://docs.stripe.com/workflows.md、見た日 2026-11-11）。
- 条件で分岐でき、オブジェクトの一覧を回して同じ処理をかけられる。アプリが作ったカスタムアクションで外部とつながる（出典: https://docs.stripe.com/workflows.md、見た日 2026-11-11）。
- 組みこみの守りがある。無限ループの検出、自動の再試行、冪等、実行ごとの記録だ（出典: https://docs.stripe.com/workflows.md、見た日 2026-11-11）。
- Workflows は一般提供。ループ、カスタムアクション、Mailchimp と Slack のアクションはプレビュー（出典: https://stripe.com/blog/everything-we-announced-at-sessions-2026、見た日 2026-11-11）。
- keynote では「一度決めれば、誰が起こしても同じように動く」と説明している（出典: https://stripe.com/sessions/2026/developer-keynote、見た日 2026-11-11）。

### Custom Objects

- 配送や予約など、Stripe の標準のオブジェクトでは表せないデータを、独自の型として定義する。顧客や請求とつなげられる（出典: https://docs.stripe.com/custom-objects.md、見た日 2026-11-11）。
- 定義は TypeScript で書き、Stripe Apps にまとめる。上げると API ができる。変化はイベントになり、Workflows の起点にもなる（出典: https://docs.stripe.com/custom-objects.md、見た日 2026-11-11）。
- プライベートプレビューで、1 アカウントの中だけで使える（出典: https://docs.stripe.com/custom-objects.md、見た日 2026-11-11）。

### Stripe Apps

- アプリを社内だけで配るか、Marketplace に出せる。ダッシュボードの中に独自の画面を作れる（出典: https://docs.stripe.com/stripe-apps.md、見た日 2026-11-11）。
- Sessions 2026 で、フルページで複数タブのアプリをプレビューで出した（出典: https://stripe.com/blog/everything-we-announced-at-sessions-2026、見た日 2026-11-11）。

### このプロダクトへの使い方

- 推測: 「自然言語で採用の流程を設計する」は、自然言語から決まった流程の定義(起点、条件、手順)を作ることにする。実行はその定義で行う。Stripe の keynote の「誰が起こしても同じように動く」という性質を保てる。
- 推測: 企業ごとに違う項目(職種ごとの評価の観点、独自の書類など)は Custom Objects のように型として定義させる。複雑なカスタマイズの代わりになる。
- 推測: ATS や勤怠、給与のシステムとのつなぎは、カスタムアクションのような拡張の口にする。部品を独立に保てる。

## 8. Agentic commerce

### Agentic Commerce Protocol(ACP)

- Stripe と OpenAI が共同で作った開かれた規格だ。2025-09-29 に発表した（出典: https://stripe.com/newsroom/news/stripe-openai-instant-checkout、見た日 2026-11-11）。
- 「買い手、AI エージェント、事業者の間のプログラムによる取引の開かれた規格」で、Apache 2.0 で公開している（出典: https://www.agenticcommerce.dev/、見た日 2026-11-11）。
- 設計の原則として、事業者は売り手(merchant of record)のまま客との関係を持つ。どの決済代行とも組める（出典: https://stripe.com/blog/developing-an-open-standard-for-agentic-commerce、見た日 2026-11-11）。
- 事業者は注文を受けるか断るかを決められる。商品の見せ方や注文の処理も自分で決める（出典: https://stripe.com/newsroom/news/stripe-openai-instant-checkout、見た日 2026-11-11）。
- 推測: 企業の bot と求職者の bot の間の規格を作るなら、ACP の形が手本になる。企業は採否を決める主体のまま、どの求職者の bot ともやり取りできる。開かれた規格にすれば、大手の囲いこみと差をつけやすい。

### Shared Payment Token(SPT)

- エージェントが始める買い物で、売り手に、客の支払い手段への限られた権限を渡すトークンだ（出典: https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens.md?agent-seller=agent、見た日 2026-11-11）。
- エージェントは、相手の売り手、通貨、上限の金額、期限を決めて発行する。いつでも取り消せる（出典: https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens.md?agent-seller=agent、見た日 2026-11-11）。
- 状態は `active`、`requires_action`、`deactivated` の 3 つ。変化は Webhook で知らせる。`deactivated` は戻らない（出典: https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens.md?agent-seller=agent、見た日 2026-11-11）。
- 使える国は米国、カナダ、欧州の一部で、日本は入っていない（出典: https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens.md?agent-seller=agent、見た日 2026-11-11）。
- 推測: 求職者のアシスタントが企業に「見てよい範囲」を渡すときに使える。「A 社の B 職の選考だけ」「職務経歴と希望年収だけ」「30 日まで」と絞ったトークンにする。求職者はいつでも取り消せ、企業がいつ使ったかもイベントで分かる。

### Instant Checkout

- 2025-09-29 に、米国の ChatGPT の利用者が Etsy の店から買える形で始まった（出典: https://stripe.com/newsroom/news/stripe-openai-instant-checkout、見た日 2026-11-11）。
- 2026-03 に、OpenAI が ChatGPT の中での買い物を縮小したと報じられた。OpenAI の広報は「Instant Checkout はアプリに移る」と述べたという(報道)（出典: https://www.shopifreaks.com/openai-scales-back-its-integrated-commerce-plans/、見た日 2026-11-11）。
- 今の状態を、OpenAI の一次情報で確かめることはできなかった。OpenAI の開発者向けページは ACP の連携の手順を案内している。Instant Checkout には触れていない（出典: https://developers.openai.com/commerce、見た日 2026-11-11）。
- 推測: 汎用アシスタントの中で最後まで済ませる形は、まだ定着していないかもしれない。hiring-os は、汎用アシスタントに頼らない専用の求職者アシスタントと、開かれた規格の両方を持つほうが安全だ。

### Agentic Commerce Suite と関連の発表

- Sessions 2026 では次を発表した（出典: https://stripe.com/blog/everything-we-announced-at-sessions-2026、見た日 2026-11-11）。
  - Agentic Commerce Suite: 提供中。商品の一覧を上げ、エージェントの利用をダッシュボードで管理する。
  - プラットフォーム向けの版: プレビュー。
  - Machine Payments Protocol: 提供中。
  - Google との Universal Commerce Protocol: 近く提供。
- 投稿の日付は 2026-04-29 で、新しい製品と機能は 288 個（会社の発表）（出典: https://stripe.com/blog/everything-we-announced-at-sessions-2026、見た日 2026-11-11）。

### Link Agent Wallet

- エージェントが、利用者の承認を得て支払う。利用者が共有を選んだ口座の金融データも読める（出典: https://docs.stripe.com/agentic-commerce/agents/link-agent-wallet.md、見た日 2026-11-11）。
- 認証は、利用者 1 人ごとの OAuth のアクセストークンで行う。Stripe の API キーは使えない（出典: https://docs.stripe.com/agentic-commerce/agents/link-agent-wallet.md、見た日 2026-11-11）。
- 支払いは米国とカナダ、金融データは米国の利用者だけが対象だ（出典: https://docs.stripe.com/agentic-commerce/agents/link-agent-wallet.md、見た日 2026-11-11）。
- 推測: 求職者のアシスタントの権限は、Stripe の鍵ではなく、求職者 1 人ごとの OAuth で渡す形が合う。企業の権限とは別の系統にする。

### サービスの予約(面接の日程の手本)

- 予約できるサービスを持つ事業者向けに、エージェントが空きを探し、予約し、支払う流れを示している（出典: https://docs.stripe.com/agentic-commerce/sellers/use-cases/booking.md、見た日 2026-11-11）。
- 操作ごとに別の道具にするよう勧めている。`search_availability`、`create_booking`、`complete_booking`、`modify_booking`、`cancel_booking` だ（出典: https://docs.stripe.com/agentic-commerce/sellers/use-cases/booking.md、見た日 2026-11-11）。
- 予約の一生を通じて、変わらない ID を使う。枠が埋まったら `409` と `slot_unavailable` を返し、エージェントが別の枠を探せるようにする（出典: https://docs.stripe.com/agentic-commerce/sellers/use-cases/booking.md、見た日 2026-11-11）。
- 冪等キーを受け、記録を 24 時間以上残すよう勧めている（出典: https://docs.stripe.com/agentic-commerce/sellers/use-cases/booking.md、見た日 2026-11-11）。
- Stripe は決まった API の形を求めていない。業界の規格があればそれに従うよう書いている（出典: https://docs.stripe.com/agentic-commerce/sellers/use-cases/booking.md、見た日 2026-11-11）。
- 推測: 面接の日程の調整は、この形をほぼそのまま写せる。企業の bot が空き枠を出し、求職者の bot が選んで確定する。採用の流程で最初に A2A にしやすい部品だ。

### エージェント同士の取引(Sessions 2026 のセッション)

- 「Preparing for agent-to-agent commerce」で、Stripe と AWS の担当者が話した。取引は「その場の行為」から「前もって決めた方針」に変わりつつあると述べた（出典: https://stripe.com/au/sessions/2026/preparing-for-agent-to、見た日 2026-11-11）。
- 買い手のエージェントは、利用者が決めた予算と方針の中で動く。上限を超えれば人に戻す。すべての操作は記録し、監査できるようにする（出典: https://stripe.com/au/sessions/2026/preparing-for-agent-to、見た日 2026-11-11）。
- 売り手のエージェントは、来たエージェントを認証し、価格の決まりと在庫を確かめてから支払いを受ける（出典: https://stripe.com/au/sessions/2026/preparing-for-agent-to、見た日 2026-11-11）。
- 中心の主張は「エージェントは考え、支払いはコードがする」だ。デモは試作で、本番ではないと断っている（出典: https://stripe.com/au/sessions/2026/preparing-for-agent-to、見た日 2026-11-11）。
- 推測: 企業の bot と求職者の bot のやり取りも「方針の中で動き、外れたら人に戻す」形にする。たとえば「年収の下限を下回る提示は人に戻す」「面接の候補日は自動で受ける」のように決める。

## 9. Stripe の年次の手紙(2025 年版)

- 2026-02-24 に公開した。2025 年の取扱高は 1.9 兆ドルで、前年から 34% 増えた（会社の発表）（出典: https://stripe.com/newsroom/news/stripe-2025-update、見た日 2026-11-11）。
- 「エージェントコマースの成功は、初期のインターネットのように、一律の相互運用性にかかっている」と書いている（出典: https://stripe.com/newsroom/news/stripe-2025-update、見た日 2026-11-11）。
- 手紙は、エージェントコマースを 5 段階に分けた。業界は「1 段階目と 2 段階目の境目にいる」と書いたという(報道)（出典: https://www.paymentsdive.com/news/stripes-slower-view-of-agentic-commerce/813056/、見た日 2026-11-11）。
- 5 段階目は、エージェントが利用者の必要と予算を知り、指示なしで動く段階だという(報道)（出典: https://www.paymentsdive.com/news/stripes-slower-view-of-agentic-commerce/813056/、見た日 2026-11-11）。
- 推測: 採用でも、いきなり全自動を目指さず、段階を分けて出すほうがよい。たとえば「書類の入力の代行」「条件の説明で探す」「継続して探す」「権限を渡して任せる」「先回りして動く」の順だ。

## このプロダクトへの示唆

- 推測: 採用の流程を、Stripe の製品のように独立した部品に分ける。各部品は単独でも、他社の ATS や媒体と組んでも使えるようにする。
- 推測: 「自然言語で設計する」は、自然言語から決まった流程の定義を作ることにする。実行はその定義で行い、まずサンドボックスで試す。Stripe の Workflows と keynote の考え方に合う。
- 推測: 企業の bot には、資源ごとに読み書きを分けた鍵を渡す。bot には印をつけ、不採用の通知や内定などは承認ルールで止める。担当が 1 人の会社でも二者承認が成り立つ。
- 推測: 求職者のアシスタントには、SPT のように「相手、範囲、期限」を絞ったトークンでデータの権限を渡させる。取り消せて、使われたらイベントで分かる形にする。これが汎用アシスタントとの違いの核になる。
- 推測: A2A の最初の部品は面接の日程にする。Stripe の予約の手引き(空きの検索、確定、構造化したエラー、冪等キー)をほぼそのまま使える。
- 推測: A2A の規格は ACP のように開いて公開する。日付の版と固定で、相手が変わっても壊れないようにする。
- 推測: エージェントに読めるドキュメント、MCP サーバー、スキルを最初から用意する。Stripe はドキュメントのアクセスの 40% 近くがエージェントだと述べている（会社の発表）。
- 推測: Instant Checkout の縮小の報道から考えると、汎用アシスタントの中で完結させる形だけに頼るのは危うい。
- 推測: SPT と Link Agent Wallet は日本で使えない。hiring-os が日本で支払いを扱うなら、この部品は直接は使えない。採用の多くは支払いを伴わないので、使うのは設計の考え方が中心になる。

## 見つからなかったこと

- 2026-10-26 の Stripe の agentic design のセミナーの公開資料。Stripe のイベントのページ(stripe.events)は 403 で開けなかった。Stripe Tour Tokyo の公式ページは 404 だった。
- Stripe Tour Tokyo 2026(2026-09-30)の講演の動画や資料。開催の案内(sbbit)だけ確かめた。
- 年次の手紙の本文の 5 段階の名前。stripe.com/annual-updates/2025 を開いたが、取れた本文にエージェントコマースの節がなかった。5 段階の中身は報道でしか確かめていない。
- Instant Checkout の 2026-11 時点の状態を示す OpenAI の一次情報。
- Workflows を自然言語で作る機能。Dashboard assistant が Workflows を作れるかも分からなかった。
- 承認ルールとエージェント用の鍵の、今の提供の段階。ドキュメントに段階の表示がなかった。Sessions 2026 の発表では「Agent guardrails」はプレビューだった。
- Agent Toolkit が対応していたフレームワークの一覧。リポジトリには廃止の告知だけがあった。
