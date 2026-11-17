# エージェントどうしのやり取り、権限の渡し方、エージェントの決済の約束

## 結論

- エージェントどうしをつなぐ約束は A2A に集まりつつある。A2A は 2026-03 に v1.0.0 を出し、IBM の ACP も A2A に統合された。ただし採用の分野の語彙(求人、応募、候補者の同意)は A2A にない。
- 権限を渡す部品は IETF でそろっている。scope、RFC 8693(委任)、RFC 9396(細かい権限)、GNAP。一方、エージェント専用の OAuth の仕組みは、WG の正式文書としてはまだない。個人の草案と、課題を並べた草案が出ている段階。
- 「求職に関係するデータだけを渡す」は、RFC 9396 の authorization_details と、VC の選択的開示を組み合わせると表せそう。ただし採用向けの型の定義は見つからなかった。
- 決済の約束(Agentic Commerce Protocol、AP2、Visa、Mastercard)は採用では直接使わない。ただし「利用者が事前に署名した条件の範囲で代理させ、その証拠を残す」という型(AP2 の mandate、Mastercard の Verifiable Intent)は、応募の代行にそのまま当てはまる。
- 監査の記録は、EU AI 法で採用の AI が高リスクに入るため避けられない。EU の高リスクの義務は延期され、Annex III の分は 2027-12-02 から適用になった。

## 一覧表

提供の段階は、仕様の場合「安定版として公開」を「一般提供」、版が 0.x やベータ表記のものを「ベータ(公開)」として扱った。「採用での使いどころ」と「足りない点」の列は、本文の事実をもとにしたこの調べものの見立てで、推測を含む。

| 名前 | 出した組織 | 版と日付 | 提供の段階 | 採用での使いどころ | 足りない点 | 出典 | 見た日 |
|---|---|---|---|---|---|---|---|
| A2A | Google が作成。Linux Foundation、のち Agentic AI Foundation(AAIF) | v1.0.1(GitHub の公開 2026-05-28、変更履歴の日付 2026-05-26) | 一般提供 | 企業 bot と求職者 bot の発見(Agent Card)と、タスクの受け渡し | 採用の語彙がない。認証情報の範囲や失効は仕様の外 | https://github.com/a2aproject/A2A/releases | 2026-11-11 |
| MCP(認可) | Anthropic が作成。2025-12 に AAIF へ寄贈 | 2026-07-28 版 | 一般提供(現行版) | bot が ATS や人事のデータにつなぐ時の OAuth | エージェントどうしの約束ではない。scope の名前はサーバーごと | https://modelcontextprotocol.io/specification/versioning | 2026-11-11 |
| ACP(Agent Communication Protocol) | IBM(BeeAI) | 2025-08 に A2A に統合 | 終了(A2A へ移行) | 単体では使わない | - | https://github.com/i-am-bee/acp | 2026-11-11 |
| Agentic Commerce Protocol | OpenAI と Stripe | 2026-04-17 版 | ベータ(公開) | 直接は使わない。有料サービスの購入なら使える | 採用の取引の型はない | https://github.com/agentic-commerce-protocol/agentic-commerce-protocol | 2026-11-11 |
| AP2 | Google。2026-04 に FIDO Alliance への寄贈を発表 | v0.2(2026-04-28) | ベータ(公開) | 「事前に決めた条件で代理する」型の手本 | 決済に特化 | https://blog.google/products-and-platforms/platforms/google-pay/agent-payments-protocol-fido-alliance/ | 2026-11-11 |
| Visa Intelligent Commerce / Trusted Agent Protocol | Visa | TAP は 2025-10 公開。VIC は米国で本番の取引(2026-04 時点) | 一般提供(参加は審査制) | 直接は使わない。エージェントの署名の確かめ方は参考になる | 採用の取引の型はない | https://usa.visa.com/about-visa/newsroom/press-releases.releaseId.22341.html | 2026-11-11 |
| Mastercard Agent Pay | Mastercard | 2026 に複数の地域で本番の取引(会社の発表) | 一般提供(認定したエージェントのみ) | 同上 | 同上 | https://developer.mastercard.com/merchant-cloud/documentation/tutorials-and-guides/agentic-commerce-guide/21/ | 2026-11-11 |
| OAuth 2.0 の scope | IETF | RFC 6749(2012-10) | 一般提供 | 「求人を読む」「応募を書く」の粗い権限 | 粗すぎて、項目単位の制限ができない | https://www.rfc-editor.org/rfc/rfc6749.html | 2026-11-11 |
| RFC 8693 トークン交換 | IETF | 2020-01 | 一般提供 | 求職者 bot が「本人の代わり」であることをトークンに残す(act) | 各段で絞った権限を証明できない | https://www.rfc-editor.org/rfc/rfc8693.html | 2026-11-11 |
| RFC 9396 RAR | IETF | 2023-05 | 一般提供 | 「職歴と資格だけ、この求人に、読みだけ」を表す | 採用向けの type の定義がない | https://www.rfc-editor.org/rfc/rfc9396.html | 2026-11-11 |
| GNAP | IETF | RFC 9635(2024-10) | 一般提供(標準として) | 鍵に結びつけた権限の交渉と継続 | 採用での利用例は見つからなかった | https://www.rfc-editor.org/rfc/rfc9635.html | 2026-11-11 |
| W3C VC 2.0 | W3C | 勧告(2025-05-15) | 一般提供 | 資格や職歴を、発行元に問い合わせずに確かめる | 国内の発行元の状況は調べていない | https://www.w3.org/TR/vc-data-model-2.0/ | 2026-11-11 |
| Open Badges 3.0 | 1EdTech | Final Release(文書版 1.4.5) | 一般提供 | 資格と技能の証明 | 職歴そのものの型ではない | https://www.imsglobal.org/spec/ob/v3p0 | 2026-11-11 |
| schema.org JobPosting | schema.org | V30.1(2026-09-16) | 一般提供 | 企業 bot が求人を機械で読める形で出す | 応募の受け付けの約束ではない | https://schema.org/JobPosting | 2026-11-11 |

## 1. エージェントどうしの約束

### A2A(Agent2Agent)

- 出した組織: Google が 2025-04-09 に発表した（出典: https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/、見た日 2026-11-11）。
- 移管: Linux Foundation が 2025-06-23 に A2A のプロジェクトを始めた。100 社超が支持と発表した(会社の発表)（出典: https://linuxfoundation.org/press/linux-foundation-launches-the-agent2agent-protocol-project-to-enable-secure-intelligent-communication-between-ai-agents、見た日 2026-11-11）。
- さらに 2026-08-17 に、Linux Foundation の下の Agentic AI Foundation(AAIF)の hosted project になった。支持は 150 組織超(会社の発表)。AAIF は MCP を道具とつなぐ層、A2A をエージェントどうしの層と位置づけている（出典: https://aaif.io/blog/a2a-joins-aaif、見た日 2026-11-11）。
- 版と日付: v1.0.0 が 2026-03-12。v1.0.1 は GitHub の公開が 2026-05-28 で、変更履歴の見出しの日付は 2026-05-26（出典: https://github.com/a2aproject/A2A/releases、見た日 2026-11-11）。
- 提供の段階: 一般提供(v1.0 の安定版の仕様と SDK)（出典: https://github.com/a2aproject/A2A/releases、見た日 2026-11-11）。

仕組みの要点（出典: https://a2a-protocol.org/latest/specification/、見た日 2026-11-11）:

- Agent Card: エージェントの名前、能力、技能(skills)、つなぐ先、認証の方式を書いた JSON。`https://{server_domain}/.well-known/agent-card.json` で取れる。
- 署名: Agent Card の署名は任意。JWS(RFC 7515)と JSON の正規化(RFC 8785)を使う。
- 認証の方式: API キー、HTTP 認証、OAuth 2.0、OpenID Connect、相互 TLS を宣言できる。
- 拡張した Agent Card: 認証した相手にだけ詳しい Card を見せられる。
- タスク: `id`、`contextId`、状態、成果物(artifacts)、履歴を持つ。状態は submitted、working、input-required、auth-required、completed、failed、canceled、rejected など。
- auth-required: エージェントが相手に「認可が要る」と返す状態。認証情報は原則として別経路(out-of-band)で渡す。連鎖の各エージェントに認証情報が見えないように、とも書いている。
- 仕様が決めないこと: auth-required で得た認証情報の範囲、有効期間、失効は決めていない。
- 監査と個人データ(13.4 節): 認証の失敗や認可の拒否を記録する。機微な操作は監査の記録を残す。利用者がデータの削除を求められるようにする。ログに個人データを残すのは最小にする。
- 拡張: `A2A-Extensions` ヘッダーで拡張を指定できる。AP2 はこの拡張の形で A2A に乗る。

採用での使いどころ:

- 企業 bot が Agent Card で「求人の照会」「面接の日程調整」などの技能を公開する。求職者 bot はそれを見つけてタスクを送る。
- input-required と auth-required で、「本人の確認が要る」「追加の書類が要る」を途中で返せる。
- 推測: 応募のやり取りは時間がかかる。タスクの状態と通知(push、購読)の仕組みは、選考の進み具合の連絡に合う。

足りない点:

- 採用の語彙(求人、応募、候補者の同意、選考の結果)は仕様にない。拡張で決める必要がある。
- Agent Card は自己申告で、署名は任意。企業 bot が本物の企業のものかを確かめる仕組みは仕様の外。
- 求職者のデータのどの項目を見せてよいか、という同意の範囲を表す型はない。

### ACP(Agent Communication Protocol、IBM)

- 出した組織: IBM Research(BeeAI のための約束)。
- 今の状態: IBM の研究ページに「ACP is now part of A2A under the Linux Foundation」と出ている。移行の手引きへのリンクがある（出典: https://research.ibm.com/projects/agent-communication-protocol、見た日 2026-11-11）。
- GitHub のリポジトリは 2025-08-27 にアーカイブされ、読み取り専用になった（出典: https://github.com/i-am-bee/acp、見た日 2026-11-11）。
- AAIF は、ACP が 2025-08 に A2A に統合されたと書いている（出典: https://aaif.io/blog/a2a-joins-aaif、見た日 2026-11-11）。
- 提供の段階: 終了(A2A へ移行)。新しく採用する理由はない。
- 名前の注意: 「ACP」は OpenAI と Stripe の Agentic Commerce Protocol と同じ略称。この文書では「Agentic Commerce Protocol」と略さずに書く。

### MCP の認可

- 出した組織: Anthropic が作った。Linux Foundation は 2025-12-09 に AAIF の設立を発表し、MCP は Anthropic が寄贈した（出典: https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation、見た日 2026-11-11）。
- 版: 現行版は 2026-07-28。版は「後方互換でない変更をした最後の日付」で表す（出典: https://modelcontextprotocol.io/specification/versioning、見た日 2026-11-11）。
- 提供の段階: 一般提供(Current)。

版ごとの認可の変化:

| 版 | 認可の主な変更 | 出典 | 見た日 |
|---|---|---|---|
| 2025-06-18 | MCP サーバーを OAuth の resource server と位置づけた。Protected Resource Metadata で認可サーバーを探す。クライアントに RFC 8707(Resource Indicators)を必須にした | https://modelcontextprotocol.io/specification/2025-06-18/changelog | 2026-11-11 |
| 2025-11-25 | OpenID Connect Discovery に対応。`WWW-Authenticate` で scope を段階的に求める(SEP-835)。Client ID Metadata Documents を推奨の登録方法にした。URL 型の elicitation、試験的な tasks を追加 | https://modelcontextprotocol.io/specification/2025-11-25/changelog | 2026-11-11 |
| 2026-07-28 | 動的クライアント登録(RFC 7591)を非推奨にした。RFC 9207 の `iss` の確かめを入れた。クライアントの認証情報を認可サーバーごとに分けることを必須にした。tasks は拡張に移した。OpenTelemetry の trace context の受け渡しを文書化した | https://modelcontextprotocol.io/specification/2026-07-28/changelog | 2026-11-11 |

2026-07-28 版の認可の要点（出典: https://modelcontextprotocol.io/specification/latest/basic/authorization、見た日 2026-11-11）:

- 土台は OAuth 2.1 の草案(draft-ietf-oauth-v2-1-13)。認可そのものは任意。
- MCP サーバーは RFC 9728 の Protected Resource Metadata を必ず出す。
- クライアントは `resource` パラメータで、トークンを使う MCP サーバーを必ず指定する。サーバーは自分宛てのトークンだけを受ける。ほかのトークンを素通しすることは禁止。
- scope が足りないと、サーバーは 403 と `insufficient_scope` と必要な scope を返す。クライアントは scope を足して認可をやり直す(step-up)。
- 最小権限: `scopes_supported` は基本の機能に要る最小の scope とし、追加は step-up で求める。
- 拡張として Enterprise-Managed Authorization と OAuth Client Credentials がある。どちらも Stable で 2026-07-28 の版がある（出典: https://github.com/modelcontextprotocol/ext-auth、見た日 2026-11-11）。

OAuth 2.1 そのものはまだ RFC になっていない。最新は draft-ietf-oauth-v2-1-17(2026-10-31)。IESG への提出の目標は 2026-12（出典: https://datatracker.ietf.org/doc/draft-ietf-oauth-v2-1/、見た日 2026-11-11）。

採用での使いどころ:

- 企業の bot が、自社の ATS や人事のデータに MCP でつなぐ。scope の step-up で、普段は見ない項目を必要な時だけ開ける。
- 求職者 bot が、求職者の書類の置き場に MCP でつなぐ。

足りない点:

- MCP は道具とデータにつなぐ約束で、企業 bot と求職者 bot の間の約束ではない。
- scope の名前と意味はサーバーごとに決める。「職歴は見てよいが年齢は見ない」のような項目単位の制限は、仕様では決まっていない。

## 2. 権限を渡す形(OAuth の系統)

### OAuth 2.0 の scope

- RFC 6749(2012-10)。scope は、認可サーバーが決める文字列を空白で区切って並べたもの。サーバーは求められた scope を一部だけ認めてもよい。その場合は認めた scope を返す（出典: https://www.rfc-editor.org/rfc/rfc6749.html、見た日 2026-11-11）。
- 採用での使いどころ: 「求人を読む」「応募を出す」「面接の日程を書く」のような粗い権限。
- 足りない点: scope は二択で中身が見えない。金額の上限、期間、条件を表せない。この点は IETF の草案も課題として挙げている（出典: https://www.ietf.org/archive/id/draft-chen-oauth-agent-authz-use-cases-05.html、見た日 2026-11-11）。

### 例: Gmail の scope(2 回目のレビューの後に足した)

求職者のメールから応募のメールだけを読めるかを確かめた。

- Gmail の scope は、データの種類と読み書きの強さで分かれる。送信元や検索の条件で絞る scope はない（出典: https://developers.google.com/workspace/gmail/api/auth/scopes、見た日 2026-11-11）。
- `gmail.metadata` は、ラベルとヘッダーを読めるが、本文は読めない。この scope も restricted だ（出典: 同上、見た日 2026-11-11）。
- メッセージの一覧の `q`(Gmail の検索窓と同じ書き方の条件)は、`gmail.metadata` では使えない（出典: https://developers.google.com/workspace/gmail/api/reference/rest/v1/users.messages/list、見た日 2026-11-11）。
- 本文を読むには `gmail.readonly` などが要る。これらは restricted で、Google の restricted scope の審査が要る。restricted のデータをサーバーに保存するか送るなら、セキュリティの評価にも通る必要がある（出典: https://developers.google.com/workspace/gmail/api/auth/scopes、見た日 2026-11-11）。
- 狭い scope は、アドオンの `gmail.addons.current.message.readonly` などだ。本人がアドオンの中で操作している間だけ、そのメッセージを読める（出典: 同上、見た日 2026-11-11）。
- 推測: 「応募のメールだけを読む」は鍵では表せない。鍵の上ではメールボックス全体の読み取りになり、絞るのは受け取った側のコードだ。鍵で絞るには、本人が転送の設定で応募のメールだけを別の宛先に送るか、アドオンの形で本人が開いたメールだけを読む形になる。

### RFC 8693 トークン交換(委任)

- 2020-01 公開、Standards Track（出典: https://www.rfc-editor.org/rfc/rfc8693.html、見た日 2026-11-11）。
- 委任となりすましを分けている。委任では、A は自分の身元を保ったまま B の代わりに動く。
- `act` クレームで「今動いている者」を示す。入れ子にすると、過去の代理の連鎖も残せる。`may_act` で「誰が代理してよいか」を示せる。
- 採用での使いどころ: 求職者 bot が求職者の代わりに応募する時、トークンに「本人は求職者、動いたのは bot」と残せる。企業側は、bot が出した応募と本人が出した応募を区別できる。
- 足りない点: `act` は「誰が動いたか」を示すが、各段でどこまで権限を絞ったかは証明しない（出典: https://www.ietf.org/archive/id/draft-chen-oauth-agent-authz-use-cases-05.html、見た日 2026-11-11）。

### Rich Authorization Requests(RFC 9396)

- 2023-05 公開、Standards Track（出典: https://www.rfc-editor.org/rfc/rfc9396.html、見た日 2026-11-11）。
- `authorization_details` という JSON の配列で権限を求める。各要素は `type`(必須)と、`locations`、`actions`、`datatypes`、`identifier`、`privileges` を持てる。
- scope は粗い権限、`authorization_details` は細かい権限(例: 特定の相手への特定の金額)に使う。両方を同時に使える。認可サーバーは両方を合わせて利用者に同意を求める。
- 採用での使いどころ: 例えば type を「応募の提出」とし、`datatypes` に職歴と資格だけ、`locations` に応募先の企業 bot、`actions` に読みだけ、と書ける。
- 推測: 「求職に関係するデータだけを見せる」を同意の画面で示すには、今ある標準の中でこれが一番近い。
- 足りない点: 採用向けの `type` の定義は見つからなかった。自前で決める必要がある。

### GNAP(RFC 9635)

- 2024-10 公開、Standards Track（出典: https://www.rfc-editor.org/rfc/rfc9635.html、見た日 2026-11-11）。
- クライアントは grant endpoint に JSON で求める。`access` の配列で権限を書く。複数のトークンを一度に求められる。
- クライアントは公開鍵で身元を示す。トークンは原則その鍵に結びつく(bearer にしない)。
- 承認を待つ間は「継続」の仕組みで、あとから権限を足す、トークンを回す、取り消す、ができる。
- 採用での使いどころ: 推測: 長く続く選考で、権限を足したり取り消したりする流れに合う。
- 足りない点: 採用や汎用アシスタントで GNAP を使った例は見つからなかった。

### IETF のエージェント向けの草案

OAuth WG が正式に扱う文書(WG 文書)には、名前に「agent」を含むものはない。エージェント向けは個人の草案が中心（出典: https://datatracker.ietf.org/wg/oauth/documents/、見た日 2026-11-11）。

| 文書 | 状態 | 日付 | 内容 | 出典 | 見た日 |
|---|---|---|---|---|---|
| draft-ietf-oauth-identity-chaining-17 | WG 文書。RFC Editor の待ち行列 | 2026-07-19 | 別の信頼の範囲(別の会社の認可サーバー)へ、RFC 8693 と JWT grant で身元と権限をつなぐ。境界ごとに権限を絞れる | https://datatracker.ietf.org/doc/draft-ietf-oauth-identity-chaining/ | 2026-11-11 |
| draft-ietf-oauth-transaction-tokens-11 | WG 文書。WG の合意済み、提出の準備中 | 2026-07-30 | 1 つの信頼の範囲の中で、呼び出しの連鎖に身元と文脈を運ぶ短命の JWT | https://datatracker.ietf.org/doc/draft-ietf-oauth-transaction-tokens/ | 2026-11-11 |
| draft-oauth-ai-agents-on-behalf-of-user-02 | 個人の草案。期限切れ | 2025-08-25 | `requested_actor` と `actor_token` で、どの AI エージェントに委任するかを同意の時点から示す | https://datatracker.ietf.org/doc/draft-oauth-ai-agents-on-behalf-of-user/ | 2026-11-11 |
| draft-hardt-oauth-aauth-protocol-11 | 個人の草案 | 2026-09-25 | エージェントごとに鍵に結びついた識別子。全リクエストに HTTP Message Signatures。本人の側に立つ person server が同意を扱う | https://datatracker.ietf.org/doc/draft-hardt-oauth-aauth-protocol/ | 2026-11-11 |
| draft-chen-oauth-agent-authz-use-cases-05 | 個人の草案(Informational) | 2026-10-27 | エージェントの認可の課題を整理。委任の連鎖の証明、scope の粗さ、同意の文脈、行動の証拠、一括の取り消し、監査の ID がない、と指摘 | https://www.ietf.org/archive/id/draft-chen-oauth-agent-authz-use-cases-05.html | 2026-11-11 |

採用での使いどころ:

- identity chaining は、求職者側の認可サーバーと企業側の認可サーバーが別の会社でも、権限を絞ってつなぐ形に使える。WG 文書なので、近く RFC になる見込み(RFC Editor の待ち行列にある)。
- 推測: エージェント専用の仕組みは固まっていない。今つくるなら、RFC 8693、RFC 9396、identity chaining のような確定済みや確定間近の部品で組み、個人の草案に頼りすぎないほうが安全。

## 3. エージェントの決済と取引

採用では、求職者が対価を払う場面は少ない。それでも、この分野の「代理の範囲を前もって決め、証拠を残す」設計は参考になる。

### Agentic Commerce Protocol(OpenAI と Stripe)

- 出した組織: OpenAI と Stripe が共同で管理する。Apache 2.0（出典: https://www.agenticcommerce.dev/、見た日 2026-11-11）。
- 版と段階: 日付の版で、2025-09-29(初版)から 2026-04-17(カート、商品フィード、注文、認証、MCP)まで出ている。README は「beta」と書いている（出典: https://github.com/agentic-commerce-protocol/agentic-commerce-protocol、見た日 2026-11-11）。
- 中身: エージェントと売り手の間の購入手続き(checkout)と、決済の認証情報の安全な受け渡し。売り手は REST か MCP で出せる。最初に対応した決済の手段は Stripe の Shared Payment Token（出典: https://www.agenticcommerce.dev/、見た日 2026-11-11）。
- OpenAI 側の文書は、Agentic Checkout、Delegated Payment、商品フィードの 3 つの仕様に分けている（出典: https://developers.openai.com/commerce、見た日 2026-11-11）。
- Shared Payment Token: エージェントが売り手ごとに発行する。通貨、上限金額、有効期限を決められる。いつでも取り消せる。状態は active、requires_action、deactivated。API の版の名前は `2026-09-30.preview` で、利用規約は「Agent Services Preview」（出典: https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens.md?agent-seller=agent、見た日 2026-11-11）。
- 採用での使いどころ: 推測: 「相手ごと、上限つき、期限つき、取り消せる」というトークンの形は、求職者のデータを企業ごとに見せる権限にそのまま応用できる。

### AP2(Agent Payments Protocol、Google)

- 出した組織: Google。2025-09-17 に発表。60 組織超が参加(会社の発表)。A2A と MCP の拡張として使える（出典: https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol、見た日 2026-11-11）。
- 2025 年の発表時の考え方: Intent Mandate(利用者の指示と条件)と Cart Mandate(承認したカートの中身と金額)を、署名つきの記録として残す。intent から cart、payment への連鎖を「否認できない監査の記録」と呼んでいる。
- 版と段階: 2026-04-28 に v0.2 を出し、FIDO Alliance へ寄贈すると発表した。v0.2 は、本人がその場にいない(Human Not Present)購入に対応した。Mastercard と共同で作った Verifiable Intent も寄贈の対象（出典: https://blog.google/products-and-platforms/platforms/google-pay/agent-payments-protocol-fido-alliance/、見た日 2026-11-11）。
- 今の公式サイトの言い方: mandate を Checkout Mandate と Payment Mandate の 2 種類とし、それぞれ「開いた段階(条件)」と「閉じた段階(特定の取引の承認)」を持つ。標準化は FIDO の作業部会で続ける（出典: https://ap2-protocol.org/、見た日 2026-11-11）。
- 採用での使いどころ: 推測: 「職種、勤務地、年収の下限を満たす求人なら応募してよい」という条件を求職者が前もって署名し、bot はその範囲でだけ応募する。応募のたびに、どの条件で応募したかの証拠が残る。この形は Intent Mandate と同じ構造。
- 足りない点: 決済に特化しており、応募や個人データの開示の型はない。

### Visa Intelligent Commerce と Trusted Agent Protocol

- Visa Intelligent Commerce(VIC): エージェントが Visa の認証情報で利用者の代わりに買い物をするための仕組み。トークン化、認証(passkey、段階的な本人確認)、購入の指示(暗号化した payload)からなる。本番には認定と Visa の承認が要る（出典: https://developer.visa.com/capabilities/visa-intelligent-commerce、見た日 2026-11-11）。
- 段階: 2026-04-29 の発表で、米国では多くのエージェントと提携先に展開し、本番の取引が起きていると書いた(会社の発表)（出典: https://usa.visa.com/about-visa/newsroom/press-releases.releaseId.22341.html、見た日 2026-11-11）。
- Trusted Agent Protocol(TAP): 2025-10-17 発表。Cloudflare と作った。エージェントごとの暗号の署名で、売り手が「承認されたエージェント」と悪い bot を見分ける。HTTP Message Signature を土台にし、IETF の Web Bot Auth にそろえた。発表時点で Visa Developer Center と GitHub で使えた（出典: https://www.visa.com/en-ua/newsroom/visa-trusted-agent-protocol、見た日 2026-11-11）。
- 採用での使いどころ: 推測: 企業 bot が「この求職者 bot は登録された正規のものか」を確かめる時、TAP と同じく HTTP の署名と公開鍵の目録で確かめる形が使える。

### Mastercard Agent Pay

- 中身: エージェントは生のカード番号を扱わず、エージェント用のトークンを使う。トークンは売り手、金額、期間で絞れる。認定されたエージェントは Web Bot Auth(RFC 9421)で署名したリクエストを送り、売り手は Mastercard の鍵の目録で確かめる（出典: https://developer.mastercard.com/merchant-cloud/documentation/tutorials-and-guides/agentic-commerce-guide/21/、見た日 2026-11-11）。
- Verifiable Intent: 2026-03 に Google と共同で公開した。利用者の身元、エージェントへの指示、取引の結果を結びつけた、改ざんしにくい記録。相手ごとに必要なデータだけを渡す（出典: 同上）。仕様は v0.1 の草案で、SD-JWT を重ねた形（出典: https://github.com/agent-intent/verifiable-intent/、見た日 2026-11-11）。
- 段階: タイ、中南米などで本番の取引を済ませた、と開発者向けの文書にある(会社の発表)（出典: https://developer.mastercard.com/merchant-cloud/documentation/tutorials-and-guides/agentic-commerce-guide/21/、見た日 2026-11-11）。オーストラリアでは 2026-01 に初の取引を発表し、提携先は「初期の管理された試行」と呼んだ（出典: https://newsroom.mastercard.com/news/ap/en/newsroom/press-releases/en/2026/mastercard-accelerates-ai-powered-commerce-with-australia-s-first-authenticated-agentic-transactions-using-agent-pay/、見た日 2026-11-11）。
- 2026-09-30 には、取引がエージェントによるものかの確率を出すスコアを米国で試験中と発表した（出典: https://investor.mastercard.com/investor-news/investor-news-details/2026/Mastercard-Advances-Agentic-Commerce-With-New-Trust-and-Intelligence-Services/default.aspx、見た日 2026-11-11）。
- 採用での使いどころ: 推測: Verifiable Intent の「選択的に開示しつつ、本人の指示とエージェントの行動を結ぶ」形は、応募の代行の証拠にそのまま応用できる。

## 4. 職歴と資格の証明

### W3C Verifiable Credentials 2.0

- W3C 勧告、2025-05-15（出典: https://www.w3.org/TR/vc-data-model-2.0/、見た日 2026-11-11）。
- 役割: 発行者(issuer)、持ち主(holder)、確かめる者(verifier)。持ち主は複数の証明をまとめて提示(verifiable presentation)できる。
- 選択的開示: 持ち主が見せる情報を細かく選べることを、仕様は用語として定義している。
- 有効期間は `validFrom` と `validUntil`、失効の確認は `status` で表す。
- 採用での使いどころ: 求職者 bot が資格や学歴の証明を提示し、企業 bot が発行元に問い合わせずに確かめる。年齢や住所など、選考に要らない項目は出さない。

### Open Badges 3.0、CLR、LER-RS

- Open Badges 3.0: 1EdTech の仕様。Final Release(文書版 1.4.5)。Open Badges の証明は W3C VC 2.0 の VC でもある。「この達成をした」と「この技能がある」の 2 つの型を持つ。複数をまとめたものが CLR(Comprehensive Learner Record)（出典: https://www.imsglobal.org/spec/ob/v3p0、見た日 2026-11-11）。
- LER-RS(Learning and Employment Record Resume Standard): 1EdTech と HR Open Standards が 2024-01-23 に発表した履歴書の標準。Open Badges 3.0、CLR 2.0、HR Open の履歴書の標準を組み合わせた（出典: https://www.1edtech.org/1edtech-article/1edtech-and-hr-open-improve-learning-to-employment-with-updated-standard/410921、見た日 2026-11-11）。
- 採用での使いどころ: 推測: 求職者の職歴を LER-RS の形で持ち、資格を Open Badges で添えると、企業 bot が機械で確かめられる。
- 足りない点: 前職の会社が職歴を VC で発行する仕組みの普及の状況は、見つからなかった。

## 5. 求人の構造化データ

### schema.org JobPosting と Google の求人の構造化データ

- schema.org の JobPosting は V30.1(2026-09-16)。`title`、`datePosted`、`validThrough`、`hiringOrganization`、`jobLocation`、`baseSalary`、`employmentType`、`directApply`、`qualifications`、`skills`、`experienceRequirements`、`educationRequirements`、`jobLocationType` などを持つ（出典: https://schema.org/JobPosting、見た日 2026-11-11）。
- Google の求人の構造化データは、`datePosted`、`description`、`hiringOrganization`、`jobLocation`、`title` を必須とする。求人の URL は sitemap より Indexing API で知らせるよう勧めている（出典: https://developers.google.com/search/docs/appearance/structured-data/job-posting、見た日 2026-11-11）。
- 採用での使いどころ: 企業 bot が出す求人の型の土台にできる。求職者 bot は、汎用の検索とも同じ型で読める。
- 足りない点: 求人を「出す」型であり、応募を受け付けるやり取りの約束ではない。`directApply` は「その URL から直接応募できるか」の真偽だけ。

### HR Open Standards

- HR Open Standards のサイトは、Trusted Career Profile(TCP)の正式公開、JEDx Open API(Final)、Skills Proficiency Data API(公開前)を載せている。版や日付は書いていない（出典: https://www.hropenstandards.org/、見た日 2026-11-11）。
- AI やエージェントに向けた仕事は、サイトの上では見つからなかった。

## 6. 監査の記録の考え方

各約束の監査の考え方:

| 出どころ | 監査についての考え方 | 出典 | 見た日 |
|---|---|---|---|
| A2A 13.4 節 | 認証の失敗、認可の拒否、怪しい要求を記録する。機微な操作は監査の記録を残す。ログの個人データは最小にする | https://a2a-protocol.org/latest/specification/ | 2026-11-11 |
| AP2(2025 年の発表) | intent、cart、payment の署名つき mandate の連鎖を「否認できない監査の記録」とする | https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol | 2026-11-11 |
| RFC 8693 | `act` の入れ子で代理の連鎖を残す | https://www.rfc-editor.org/rfc/rfc8693.html | 2026-11-11 |
| Transaction Tokens 草案 | 呼び出しの連鎖に、身元と文脈を短命の署名つきトークンで運ぶ | https://datatracker.ietf.org/doc/draft-ietf-oauth-transaction-tokens/ | 2026-11-11 |
| MCP 2026-07-28 | OpenTelemetry の trace context を `_meta` で受け渡す決まりを文書化した | https://modelcontextprotocol.io/specification/2026-07-28/changelog | 2026-11-11 |
| IETF の課題の草案 | 段をまたぐ監査の ID、エージェントを別の主体として記録する方法、承認と行動を結ぶ否認できない記録が、どれも標準にない | https://www.ietf.org/archive/id/draft-chen-oauth-agent-authz-use-cases-05.html | 2026-11-11 |

法令の面:

- EU AI 法の Annex III の 4(a) は、採用と選考に使う AI、つまり応募の分析と絞り込み、候補者の評価を高リスクに入れている（出典: https://artificialintelligenceact.eu/annex/3/、見た日 2026-11-11）。このサイトは条文の転載で、EU の公式のサイトではない。
- 第 12 条は、高リスクの AI に、使っている間ずっと出来事を自動で記録できることを求める。目的は、リスクの発見、市販後の監視、利用者による監視（出典: https://artificialintelligenceact.eu/article/12/、見た日 2026-11-11）。記録の最低項目の一覧は Annex III の 1(a)(生体認証)向けで、採用向けではない。
- 適用の日: Digital Omnibus on AI により、Annex III の高リスクの義務(第 3 章 1〜3 節)は 2027-12-02 から適用になった。もとは 2026-08-02（出典: https://data.consilium.europa.eu/doc/document/PE-30-2026-INIT/en/pdf、見た日 2026-11-11）。この規則は Regulation (EU) 2026/1744 で、2026-07-08 採択、2026-07-24 に官報に載った（出典: https://www.niassembly.gov.uk/assembly-business/committees/2022-2027/windsor-framework-democratic-scrutiny-committee/eu-acts/published-eu-acts/regeu20261744/、見た日 2026-11-11）。

推測: 採用の bot の監査の記録には、少なくとも次が要る。

- 誰の代わりに、どの bot が動いたか(RFC 8693 の `act` に当たるもの)
- どの同意(どの項目を、どの企業に、いつまで)にもとづいたか
- 相手の bot の身元をどう確かめたか(Agent Card の署名、HTTP の署名)
- どのデータを渡し、どの判断をしたか
- 人が確かめた場合は、その人と時刻

## 7. 採用の分野で A2A を使う例

- Google の A2A の発表(2025-04-09)は、例として「ソフトウェアエンジニアの採用」を挙げた。採用担当者のエージェントが専門のエージェントと組んで候補者を探し、面接の日程を組み、別のエージェントが経歴の確認をする（出典: https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/、見た日 2026-11-11）。
- この例は、企業の中で企業のエージェントどうしが組む話。企業 bot と求職者 bot が直接やり取りする、公開された実装の例は見つからなかった。

## このプロダクトへの示唆

- 企業 bot と求職者 bot の間の土台は A2A を使う。発見は Agent Card、やり取りはタスク、本人の確認は auth-required で表せる。
- 推測: 採用の語彙(求人、応募、同意、選考の結果)は、A2A の拡張として自分たちで定義することになる。その時、求人は schema.org JobPosting、職歴は LER-RS、資格は Open Badges 3.0 の型を借りると、ほかとつなぎやすい。
- 推測: 求職者の「求職に関係するデータだけを見せる」は、RFC 9396 の `authorization_details` で項目と相手と操作を書き、VC の選択的開示で中身を出す、の 2 段で表せる。採用向けの `type` の定義はまだどこにもないので、ここに先行する余地がある。
- 推測: 応募の代行は、AP2 の mandate や Mastercard の Verifiable Intent と同じ形にできる。「この条件なら応募してよい」を求職者が前もって署名し、bot はその範囲でだけ動き、応募ごとに証拠を残す。
- 推測: 企業側の bot が人事のデータに入る時は、MCP の認可(RFC 8707 の宛先の固定、scope の step-up)と、identity chaining による会社をまたいだ権限の絞り込みが使える。
- 推測: 監査の記録は最初から設計に入れる。EU で売るなら、2027-12-02 から採用の AI に記録の義務がかかる。エージェントの監査の ID は IETF でも標準がないので、自前で決める必要がある。
- 推測: 決済の約束そのもの(Agentic Commerce Protocol、Visa、Mastercard)は、求人広告の購入や有料の選考サービスを bot が買う場面まで要らない。

## 見つからなかったこと

- 企業 bot と求職者 bot が A2A で直接やり取りする、公開された実装や発表。
- A2A、MCP、RFC 9396 の、採用向けの拡張や `type` の定義。
- HR Open Standards の、AI やエージェントに向けた仕事。Trusted Career Profile の版と日付。
- 前職の会社が職歴を VC で発行する仕組みの、普及の状況(国内も海外も)。
- GNAP を採用や汎用アシスタントで使った例。
- Mastercard の newsroom のいくつかのページ(Verifiable Intent の記事、ビジョンの記事、中南米の発表)は 403 で開けなかった。代わりに開発者向けの文書と investor の発表で確かめた。
- Visa の Trusted Agent Protocol が 2026 年に一般提供の扱いになったかの公式の発表は見つからなかった。
- EUR-Lex の Regulation (EU) 2026/1744 の本文のページは中身を取れなかった。適用の日は、理事会の文書 PE-CONS 30/26 の本文で確かめた。
- EU AI 法の Annex III と第 12 条は、EU の公式のサイトでは開けなかった。条文の転載サイトで確かめた。
