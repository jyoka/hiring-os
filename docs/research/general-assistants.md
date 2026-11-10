# 汎用アシスタントのエージェント機能と求職での使われ方

## 結論

- 主な汎用アシスタントは、どれも「ブラウザやクラウドの PC を操作する」「アプリをつなぐ」「記憶する」の 3 つを持つ。権限を決める単位は、アプリ(コネクタ)、ツール(操作)、サイトのどれかで、データの中身の種類で決める仕組みは見つからなかった。
- 確認の手順は各社とも似ている。送信、購入、フォーム送信、削除などは、人の承認を待つ。Gemini と Claude は、操作ごとに「常に許可 / 毎回聞く / 禁止」を選べる。
- 求職での使われ方は「求人サービスがアシスタントの中にアプリを出す」形が中心。Indeed は ChatGPT の中にアプリを出した(2026-02)。LinkedIn は企業向けの Hiring Pro を Claude からつないだ(2026-10)。応募の代行まで一般提供した汎用アシスタントは見つからなかった。
- 「求職に関係するデータだけを見せ、ほかは遮断する」は、今の権限の形では、そのままはできない。つなぐサービスを絞る、プロジェクトの記憶を分ける、など近いことはできる(詳しくは最後の節)。

## 調べた範囲と前提

- 見た日はすべて 2026-11-11。
- このターンの WebSearch は、ほかのエージェントと共有の上限(200 回)に達していた。そのため検索はできず、公式の URL を WebFetch で直接開いて確かめた。
- openai.com と help.openai.com は 403 で開けなかった。OpenAI の製品は、openai.com のニュースの RSS(題名、日付、短い説明)、developers.openai.com、chatgpt.com、提携先の発表で確かめた。RSS で確かめたことは、そう書いた。
- x.ai と help.x.com は 403、x.com は 402 で開けなかった。Grok は docs.x.ai で確かめた。

## 一覧

| 名前 | 対象 | 代わりに操作できること | 提供の段階 | 権限の決め方 | 記憶 | つなぐ口 | 求職での使われ方 | 出典 | 見た日 |
|---|---|---|---|---|---|---|---|---|---|
| ChatGPT(agent、ChatGPT Work、apps) | 個人と企業 | アプリ、ファイル、ブラウザをまたいだ作業。承認が要る所で止まる | ChatGPT Work: 一般提供(2026-07 発表)。Atlas: 廃止と RSS に記載 | アプリはツールごとに OAuth の範囲。書き込みは注記と確認 | 新しい記憶の仕組み「Dreaming」(2026-06) | Apps SDK(plugins、MCP の上に作る) | Indeed のアプリで求人を探せる。応募は Indeed 側 | https://chatgpt.com/features/agent/ ほか本文 | 2026-11-11 |
| Claude(Claude in Chrome、computer use、connectors、Duet) | 個人と企業 | Chrome でクリック、入力、フォーム入力。API でデスクトップ操作。Duet はクラウドの PC で作業 | Chrome: 有料プラン。computer use: 安定版。Duet: 研究プレビュー(米国) | コネクタはツールごとに「常に許可 / 承認が要る / 禁止」(管理者)。サイトの許可と禁止の一覧(管理者) | 話題ごとに保存。見る、直す、消すができる。プロジェクトごとに分けられる | MCP(コネクタ)、Agent Skills | LinkedIn の Hiring Pro(企業向け)。求職者向けの公式の機能は見つからなかった | https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities ほか本文 | 2026-11-11 |
| Gemini(タスク、Chrome auto browse、Personal Intelligence) | 個人 | 手元の Chrome かクラウドのブラウザで操作。Workspace のアプリの操作 | タスク: 有料プラン(EEA、英国などは除く)。Personal Intelligence: 米国でベータ(2026-01) | アプリの操作ごとに「常に許可 / 常に聞く」。ブラウザも同じ | 過去の会話の記憶。消すには会話を消す | Connected Apps(MCP、プレビュー)、独自の MCP(米国、英語) | 公式の求職の機能、求人アプリの連携は見つからなかった | https://support.google.com/gemini/answer/18766567?hl=en ほか本文 | 2026-11-11 |
| Grok(Grok Bot) | 個人とチーム | クラウドの PC(ブラウザ、ファイル、端末)で作業 | 2026-08 に提供開始と記載。ベータか一般提供かは不明 | 承認のカードで止まる。保存したログインを使う | 会話をまたいで好みやログインを保つ | コネクタ、MCP、API | 見つからなかった | https://docs.x.ai/grok-bot/overview | 2026-11-11 |
| Microsoft Copilot(Autopilot、Cowork) | 企業 | Microsoft 365 の中の長い作業。Autopilot は独自の ID で動く | Cowork: 一般提供(2026-06)。Autopilot: 限定プレビュー | Entra の ID、承認した資源だけ。Purview のラベルと DLP | Work IQ で文脈を積む | MCP(デスクトップ経由) | LinkedIn Hiring Pro は Copilot に「近く」 | https://www.microsoft.com/en-us/copilot/blog/2026/06/02/introducing-microsoft-scout-your-always-on-personal-agent/ ほか本文 | 2026-11-11 |
| Perplexity(Comet、ショッピング) | 個人 | ブラウザでの作業、メール、買い物 | Comet: Mac、Windows、iOS、Android | 見つからなかった | 保存した記憶と検索の履歴。答えの出典に記憶を出す | Agent API の managed connectors(プレビュー) | 見つからなかった | https://www.perplexity.ai/comet ほか本文 | 2026-11-11 |
| Apple(Siri AI) | 個人 | Messages、Reminders などのアプリでの操作 | ベータ(iOS 27 など)。日本語あり | 見つからなかった | 端末の上で個人の情報を扱うと記載 | App Intents | 見つからなかった | https://www.apple.com/apple-intelligence/ | 2026-11-11 |
| Meta(Muse) | 個人 | 買い物、予約、メールと予定の管理 | シンガポールで提供(2026-10)。日本は記載なし | 機密の操作の前に確認。パスワードと支払いの手段はエージェントから見えない | 詳しい記載なし | Gmail、Google Calendar、Instagram などのコネクタ | 見つからなかった | https://about.fb.com/news/2026/10/muse-is-now-available-in-singapore-the-worlds-first-personal-ai-agent-built-for-everyone/ | 2026-11-11 |
| LINEヤフー(Agent i) | 個人 | 領域ごとのエージェントでの相談、タスク(定期の情報集め) | 一般提供(2026-04)。一部の領域はベータ | 見つからなかった | 「メモリ機能」を 2026-06 までに入れる予定と発表 | LINE、Yahoo! JAPAN の各サービス | 公表された領域に求人はなかった | https://www.lycorp.co.jp/ja/news/release/020366/ | 2026-11-11 |

## ChatGPT(OpenAI)

### 対象と提供の段階

- 対象は個人と企業の両方。
- ChatGPT agent は 2025-07-17 に出た。調べもの、予約、スライド作りを、道具を使って進める(RSS で確認)（出典: https://openai.com/news/rss.xml 、見た日 2026-11-11）。
- Operator は 2025-01-23 に出た(RSS で確認)。推測: ChatGPT agent が Operator の後を継いだ。本文は開けなかった（出典: https://openai.com/news/rss.xml 、見た日 2026-11-11）。
- ChatGPT Atlas(ブラウザ)は 2025-10-21 に出た。RSS の説明には「Atlas has since been deprecated.」とある。廃止の日付は不明（出典: https://openai.com/news/rss.xml 、見た日 2026-11-11）。
- ChatGPT Work は 2026-07-09 に発表された。RSS では「アプリとファイルをまたいで動くエージェント」と説明している（出典: https://openai.com/news/rss.xml 、見た日 2026-11-11）。

### AI とエージェントでしていること

- ChatGPT Work は、目標を受け取り、定期の作業や見張りをする。アプリ、ファイル、ブラウザを使う（出典: https://chatgpt.com/features/agent/ 、見た日 2026-11-11）。
- 判断や承認が要る所で人に聞く。メールの下書きは送らずに残す（出典: https://chatgpt.com/features/agent/ 、見た日 2026-11-11）。
- Plan モードでは、手順の案を作り、人が承認してから作業を始める（出典: https://chatgpt.com/features/agent/ 、見た日 2026-11-11）。
- 開発者向けには、Agents API(2026-09-10 に公開ベータ)の computer use で、OpenAI のブラウザを操作できる。サイトへのアクセスの承認とログインは、使う側のアプリが受け持つ（出典: https://developers.openai.com/changelog 、見た日 2026-11-11）。

### 権限とデータの扱い

- アプリ(plugins)の認証は OAuth 2.1 の認可コードと PKCE。ツールごとに必要な範囲(scope)を宣言する（出典: https://developers.openai.com/apps-sdk/build/auth 、見た日 2026-11-11）。
- サーバーは、ツールを呼ぶたびに範囲を確かめる決まり（出典: https://developers.openai.com/apps-sdk/guides/security-privacy 、見た日 2026-11-11）。
- 書き込みの操作には `readOnlyHint: false` を付ける。取り消せない操作には `destructiveHint: true` を付ける。注記は安全の仕組みではないと明記している（出典: https://developers.openai.com/apps-sdk/app-submission-guidelines 、見た日 2026-11-11）。
- アプリは、会話の履歴の全部を求めてはいけない。要るデータだけを集める決まり（出典: https://developers.openai.com/apps-sdk/app-submission-guidelines 、見た日 2026-11-11）。
- 政府の ID、健康の情報、パスワードなどは、アプリが集めてはいけない（出典: https://developers.openai.com/apps-sdk/app-submission-guidelines 、見た日 2026-11-11）。

### 記憶

- 2026-06-04 に、新しい記憶の仕組み「Dreaming」を出した(RSS で確認)（出典: https://openai.com/news/rss.xml 、見た日 2026-11-11）。
- 記憶を見る、消す手順のヘルプは、403 で開けなかった。
- 「メモリとチャットを参照する」設定がオンだと、Yahoo!ショッピングのアプリが使えないことがある、と LINEヤフーが書いている（出典: https://www.lycorp.co.jp/ja/news/release/020386/ 、見た日 2026-11-11）。

### つなぐ口

- apps in ChatGPT と Apps SDK は 2025-10-06 に発表された(RSS で確認)（出典: https://openai.com/news/rss.xml 、見た日 2026-11-11）。
- 今の開発者向けの文書は「plugins」と呼ぶ。skills、MCP サーバー、画面を組み合わせ、ChatGPT のディレクトリに出す（出典: https://developers.openai.com/apps-sdk 、見た日 2026-11-11）。
- 日本では、Yahoo!ショッピングが 2026-05-21 にアプリを出した（出典: https://www.lycorp.co.jp/ja/news/release/020386/ 、見た日 2026-11-11）。

### 求職での使われ方

- Indeed は 2026-02-10 に ChatGPT の中のアプリを出した。Indeed のプロフィールをつなぐと、好みと資格に合う求人を出す（出典: https://www.indeed.com/news/releases/indeed-launches-app-in-chatgpt?co=US 、見た日 2026-11-11）。
- 応募は ChatGPT の中ではなく、Indeed のサイトとアプリが「主な場所」のまま（出典: https://www.indeed.com/news/releases/indeed-launches-app-in-chatgpt?co=US 、見た日 2026-11-11）。
- OpenAI は 2025-09-04 に「Jobs Platform」と認定(Certifications)を発表した(RSS で確認)。今の提供の段階は確かめられなかった（出典: https://openai.com/news/rss.xml 、見た日 2026-11-11）。
- 「ChatGPT Jobs」という名の機能は、見た範囲では見つからなかった。

## Claude(Anthropic)

### 対象と提供の段階

- Claude in Chrome は有料プラン(Pro、Max、Ultra、Team、Enterprise)で使える。全体がベータか一般提供かは、ヘルプに書いていない（出典: https://support.claude.com/en/articles/12012173-getting-started-with-claude-in-chrome 、見た日 2026-11-11）。
- API の computer use(`computer_toolset_20260801`)は、Claude API などで安定版(stable)（出典: https://platform.claude.com/docs/en/agents-and-tools/tool-use/computer-use-tool 、見た日 2026-11-11）。
- Claude Duet は、メッセージで仕事を頼むと、自分のクラウドの PC で動くエージェント。米国の Pro、Max、Ultra 向けの研究プレビューで、順番待ち（出典: https://claude.com/duet 、見た日 2026-11-11）。

### AI とエージェントでしていること

- Claude in Chrome は、ページを読み、クリック、入力、移動、フォームの入力をする（出典: https://support.claude.com/en/articles/12012173-getting-started-with-claude-in-chrome 、見た日 2026-11-11）。
- computer use は、画面の写真、マウス、キーボードの 17 の道具を持つ。実行する場所は、使う側が用意する（出典: https://platform.claude.com/docs/en/agents-and-tools/tool-use/computer-use-tool 、見た日 2026-11-11）。
- Duet は、メッセージの送信や支払いの前に聞く（出典: https://claude.com/duet 、見た日 2026-11-11）。

### 権限とデータの扱い

- コネクタは、つないだサービスの本人の権限を引き継ぐ（出典: https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities 、見た日 2026-11-11）。
- Team と Enterprise の管理者は、コネクタのツールごとに「Always allow / Needs approval / Blocked」を選べる。読み取りと書き込み・削除で分けて並ぶ。個人はこれを上書きできない（出典: https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities 、見た日 2026-11-11）。
- 「Claude の側で制限しても、元のシステムより広い権限にはならない。狭めるだけ」と書いている（出典: https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities 、見た日 2026-11-11）。
- Claude in Chrome は、初めは「自動で承認」のモード。承認が要る所では止まって聞く。管理者は、使ってよいサイトと禁止のサイトの一覧を決められる（出典: https://support.claude.com/en/articles/12012173-getting-started-with-claude-in-chrome 、見た日 2026-11-11）。
- computer use の文書は、権限を絞った仮想マシンを使う、ログイン情報を見せない、行けるドメインを絞る、を勧めている（出典: https://platform.claude.com/docs/en/agents-and-tools/tool-use/computer-use-tool 、見た日 2026-11-11）。

### 記憶

- 記憶は Free、Pro、Max、Ultra で初めからオン。話題ごとに保存し、設定から見る、直す、消すができる（出典: https://support.claude.com/en/articles/11817273-using-claude-s-chat-search-and-memory-to-build-on-previous-context 、見た日 2026-11-11）。
- プロジェクトごとに記憶を持つ。「Use account memory」を切ると、そのプロジェクトをほかから切り離せる（出典: https://support.claude.com/en/articles/11817273-using-claude-s-chat-search-and-memory-to-build-on-previous-context 、見た日 2026-11-11）。
- 健康や政治などの機微な話題は、初めは記憶しない（出典: https://support.claude.com/en/articles/11817273-using-claude-s-chat-search-and-memory-to-build-on-previous-context 、見た日 2026-11-11）。
- ほかのアシスタントとの記憶の出し入れ(試験的)もある（出典: https://support.claude.com/en/articles/11817273-using-claude-s-chat-search-and-memory-to-build-on-previous-context 、見た日 2026-11-11）。

### つなぐ口

- コネクタは remote MCP を使う。ディレクトリには 1,104 件が並んでいた（出典: https://claude.com/connectors 、見た日 2026-11-11）。
- Agent Skills は 2026-10-22 に Agentic AI Foundation(Linux Foundation の下)へ寄贈された。70 を超えるエージェントの基盤が取り入れた(会社の発表)（出典: https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation 、見た日 2026-11-11）。

### 求職での使われ方

- LinkedIn は 2026-10-21 に、中小企業向けの Hiring Pro を Claude から使えるようにした。Claude が求人の原稿を作り、人が直して承認すると LinkedIn に載る（出典: https://news.linkedin.com/2026/making-it-easier-for-small-businesses-to-hire-on-linkedin 、見た日 2026-11-11）。
- これは企業向け。Hiring Pro の求人だけが対象で、Recruiter や Hiring Assistant は含まない（出典: https://news.linkedin.com/2026/making-it-easier-for-small-businesses-to-hire-on-linkedin 、見た日 2026-11-11）。
- コネクタの一覧の見えた範囲(約 30 件)に、求職者向けの求人サービスはなかった。全 1,104 件は確かめていない（出典: https://claude.com/connectors 、見た日 2026-11-11）。

## Gemini(Google)

### 対象と提供の段階

- タスク(エージェント)は、Google AI Pro か Ultra、個人のアカウント、18 歳以上が条件。EEA、ナイジェリア、スイス、英国では使えない（出典: https://support.google.com/gemini/answer/16596215 、見た日 2026-11-11）。
- Personal Intelligence は 2026-01-14 に、米国の Pro と Ultra 向けにベータで出た（出典: https://blog.google/innovation-and-ai/products/gemini-app/personal-intelligence/ 、見た日 2026-11-11）。
- Project Mariner の今の状態は、DeepMind のページに記載がなく確かめられなかった（出典: https://deepmind.google/models/project-mariner/ 、見た日 2026-11-11）。

### AI とエージェントでしていること

- 手元の Chrome か、クラウドのブラウザでサイトを操作する。手元の Chrome では、本人がログインしているサイトすべてに入れる（出典: https://support.google.com/gemini/answer/16596215 、見た日 2026-11-11）。
- Workspace では、Calendar、Gmail、Docs、Drive、Keep、Sheets、Slides、Tasks を使う（出典: https://support.google.com/gemini/answer/16596215 、見た日 2026-11-11）。

### 権限とデータの扱い

- アプリの操作ごとに「Always allow」か「Always ask」を選ぶ。ブラウザの使用も同じ 2 つから選ぶ（出典: https://support.google.com/gemini/answer/18766567?hl=en 、見た日 2026-11-11）。
- 聞かれた時は「許可しない / 一度だけ / この会話だけ / 常に許可」から選ぶ（出典: https://support.google.com/gemini/answer/18766567?hl=en 、見た日 2026-11-11）。
- 送信、購入、フォームの送信、Google でのログインの前には確認する。「常に許可」でも、健康、金融、政府の ID などを渡す前には止まる（出典: https://support.google.com/gemini/answer/16596215 、見た日 2026-11-11）。
- アプリを切っても、Gemini の活動の記録からはデータが消えない（出典: https://support.google.com/gemini/answer/13594961 、見た日 2026-11-11）。
- 活動の記録をオフにした会話も 72 時間は残る。人が見た会話は最長 3 年残る（出典: https://support.google.com/gemini/answer/13594961 、見た日 2026-11-11）。

### 記憶

- 過去の会話から学ぶ記憶がある。覚えた事柄を消すには、それを含む会話をすべて消す（出典: https://support.google.com/gemini/answer/16598469 、見た日 2026-11-11）。
- つないだアプリから得た情報は、会話を消し、さらにアプリを切らないと使われ続けることがある（出典: https://support.google.com/gemini/answer/16598469 、見た日 2026-11-11）。
- Personal Intelligence は、Gmail、Photos、YouTube、検索のどれをつなぐかを本人が選ぶ。初めはオフ（出典: https://blog.google/innovation-and-ai/products/gemini-app/personal-intelligence/ 、見た日 2026-11-11）。

### つなぐ口

- Connected Apps Platform を 2026-10-28 にプレビューで発表した。クラウドの MCP サーバーか Android の MCP で、Gemini と検索に出せる（出典: https://blog.google/innovation-and-ai/technology/developers-tools/connected-apps-one-place/ 、見た日 2026-11-11）。
- 個人は、MCP サーバーの URL で独自のアプリをつなげる。米国、英語、個人のアカウントだけ（出典: https://support.google.com/gemini/answer/17209137 、見た日 2026-11-11）。

### 求職での使われ方

- タスクで使える Connected Apps の一覧(86 件)に、Indeed、LinkedIn、ZipRecruiter、Glassdoor、Workday はなかった（出典: https://support.google.com/gemini/table/17434654 、見た日 2026-11-11）。
- Gemini の公式の求職の機能は見つからなかった。

## Grok(xAI)

### 対象と提供の段階

- Grok Bot は 2026-08 に「now available」と release notes に書いた。ベータか一般提供か、料金は文書に書いていない（出典: https://docs.x.ai/docs/release-notes 、見た日 2026-11-11）。
- 文書では、Grok Bot は Cursor のアカウントでログインすると書いている（出典: https://docs.x.ai/grok-bot/get-started 、見た日 2026-11-11）。

### AI とエージェントでしていること

- クラウドの PC(ブラウザ、ファイル、端末)を持ち、コネクタのないサイトも操作する（出典: https://docs.x.ai/grok-bot/overview 、見た日 2026-11-11）。
- コネクタは Google Drive、Google Calendar、Gmail、Slack、Notion など。X はコネクタの一覧にない（出典: https://docs.x.ai/grok-bot/overview 、見た日 2026-11-11）。

### 権限とデータの扱い

- 承認が要る時は、承認のカードを出して待つ（出典: https://docs.x.ai/grok-bot/get-started 、見た日 2026-11-11）。
- ログインは、保存したログイン、パスワード管理のアプリ、入力の画面の順で使う。ログインの状態は Bot の PC に残る（出典: https://docs.x.ai/grok-bot/get-started 、見た日 2026-11-11）。
- 連携の取り消しの手順は、開いたページに書いていなかった。
- API では、remote MCP のツールを `allowed_tools` で絞れる（出典: https://docs.x.ai/docs/guides/tools/remote-mcp-tools 、見た日 2026-11-11）。

### 記憶

- 会話をまたいで、好み、ファイル、ログインを保つ（出典: https://docs.x.ai/grok-bot/overview 、見た日 2026-11-11）。

### 求職での使われ方

- 見つからなかった。X の求人の機能と Grok の関係は、x.com が開けず確かめられなかった。

## Microsoft Copilot

### 対象と提供の段階

- Copilot Cowork は 2026-06-16 に、Microsoft 365 Copilot の利用者に世界で一般提供になった（出典: https://www.microsoft.com/en-us/copilot/blog/2026/06/16/copilot-cowork-is-now-generally-available/ 、見た日 2026-11-11）。
- Microsoft Scout(今は Autopilot)は、Frontier の限定プレビュー（出典: https://www.microsoft.com/en-us/copilot/blog/2026/06/02/introducing-microsoft-scout-your-always-on-personal-agent/ 、見た日 2026-11-11）。
- 個人向けの Copilot の操作(Actions)、記憶、コネクタのページは、見つからなかった。

### 権限とデータの扱い

- Autopilot は、エージェントごとに Entra の ID を持つ。本人か組織が承認した資源にだけ入れる（出典: https://www.microsoft.com/en-us/copilot/blog/2026/06/02/introducing-microsoft-scout-your-always-on-personal-agent/ 、見た日 2026-11-11）。
- 送る前、書く前に、Purview の機微のラベルと DLP の規則を当てる。機微な操作には人の承認を求められる（出典: https://www.microsoft.com/en-us/copilot/blog/2026/06/02/introducing-microsoft-scout-your-always-on-personal-agent/ 、見た日 2026-11-11）。
- Cowork は初めはオフ。監査の記録、eDiscovery、機微のラベルの下で動く（出典: https://www.microsoft.com/en-us/copilot/blog/2026/06/16/copilot-cowork-is-now-generally-available/ 、見た日 2026-11-11）。

### 記憶とつなぐ口

- Autopilot は Work IQ で文脈を積む。デスクトップのアプリからブラウザと MCP サーバーに届く（出典: https://www.microsoft.com/en-us/copilot/blog/2026/06/02/introducing-microsoft-scout-your-always-on-personal-agent/ 、見た日 2026-11-11）。

### 求職での使われ方

- LinkedIn の Hiring Pro は、Claude では使えて、Copilot には「coming soon」（出典: https://news.linkedin.com/2026/making-it-easier-for-small-businesses-to-hire-on-linkedin 、見た日 2026-11-11）。
- 求職者向けに Copilot と LinkedIn をつなぐ公式の機能は、見つからなかった。

## Perplexity(Comet)

### 対象と提供の段階

- Comet は 2025-07-09 に Max の加入者向けに出た（出典: https://www.perplexity.ai/hub/blog/introducing-comet 、見た日 2026-11-11）。
- 今は Mac、Windows、iOS、Android で出ている（出典: https://www.perplexity.ai/comet 、見た日 2026-11-11）。

### AI とエージェントでしていること

- 受信箱の整理、食料品の注文、旅行の計画などを任せられる、と宣伝している（出典: https://www.perplexity.ai/comet 、見た日 2026-11-11）。
- 2025-11-25 に、PayPal で会話の中で買える買い物を出した。売り手が販売の当事者(merchant of record)のまま（出典: https://www.perplexity.ai/hub/blog/shopping-that-puts-you-first 、見た日 2026-11-11）。

### 権限とデータの扱い

- Comet は閲覧のデータ、サイトの許可、ダウンロードの記録を手元に保存する。Perplexity のアカウントと同期すると、履歴が記録される(設定による)（出典: https://www.perplexity.ai/hub/legal/comet-privacy-notice 、見た日 2026-11-11）。
- エージェントの操作の権限と確認の手順は、開いたページには書いていなかった。

### 記憶とつなぐ口

- 記憶は、保存した記憶と検索の履歴の 2 つ。答えに記憶を使うと、出典の欄に出て、そこから消せる（出典: https://www.perplexity.ai/hub/blog/ai-memory 、見た日 2026-11-11）。
- 消した記憶の記録を、最大 30 日残すことがある（出典: https://www.perplexity.ai/hub/blog/ai-memory 、見た日 2026-11-11）。
- 開発者向けの Agent API に managed connectors(GitHub、Slack、Google Drive など)がプレビューで入った（出典: https://www.perplexity.ai/hub/blog/agent-api-now-supports-reusable-agents 、見た日 2026-11-11）。

### 求職での使われ方

- 見つからなかった。

## Apple(Siri AI)

- 対象は個人。Siri AI は iOS 27 などでベータ。日本語を含む 6 言語で始める。EU では iOS などで当面使えない（出典: https://www.apple.com/apple-intelligence/ 、見た日 2026-11-11）。
- Messages、Music、Reminders などのアプリで操作する。開発者は App Intents でつなぐ（出典: https://www.apple.com/apple-intelligence/ 、見た日 2026-11-11）。
- 大きなモデルは Private Cloud Compute で動き、データは保存しないと書いている(会社の発表)（出典: https://www.apple.com/apple-intelligence/ 、見た日 2026-11-11）。
- 権限の決め方、記憶の見方、MCP への対応は、このページに書いていなかった。求職での使われ方は見つからなかった。

## Meta(Muse)

- 対象は個人。Muse は 2026-10-27 にシンガポールで出た。2026-09 に世界に向けて発表した、と書いている。日本の記載はない（出典: https://about.fb.com/news/2026/10/muse-is-now-available-in-singapore-the-worlds-first-personal-ai-agent-built-for-everyone/ 、見た日 2026-11-11）。
- 買い物の比較、予約、メールと予定の管理をする。コネクタは Gmail、Google Calendar、Instagram（出典: https://about.fb.com/news/2026/10/muse-is-now-available-in-singapore-the-worlds-first-personal-ai-agent-built-for-everyone/ 、見た日 2026-11-11）。
- メールの送信や購入の前に確認する。パスワードと支払いの手段はエージェントから見えず、「Muse Secure VM」に置く（出典: https://about.fb.com/news/2026/10/muse-is-now-available-in-singapore-the-worlds-first-personal-ai-agent-built-for-everyone/ 、見た日 2026-11-11）。
- 記憶の扱いと Facebook や Instagram のデータの使い方は、詳しく書いていない。求職での使われ方は見つからなかった。
- 以前の「Meta AI」アプリとの関係は、ページに書いていなかった。

## 国内: LINEヤフー(Agent i)

- 対象は個人。Agent i は 2026-04-20 に始まった。「LINE AI」と「Yahoo! JAPAN」の「AIアシスタント」を一つにした（出典: https://www.lycorp.co.jp/ja/news/release/020366/ 、見た日 2026-11-11）。
- 100 を超える自社のサービスのデータを使って提案する、と書いている。同意の取り方と設定は書いていない（出典: https://www.lycorp.co.jp/ja/news/release/020366/ 、見た日 2026-11-11）。
- 予約や購入を代わりにする機能を、2026-06 ごろから出す予定と書いた。「メモリ機能」も 2026-06 までに入れる予定と書いた（出典: https://www.lycorp.co.jp/ja/news/release/020366/ 、見た日 2026-11-11）。
- 2026-11-10 に単体のアプリ(iOS)を出した。領域ごとのエージェントは累計 40(ベータを含む)。生成 AI は Gemini Enterprise Agent Platform か OpenAI の API を使う（出典: https://www.lycorp.co.jp/ja/news/release/020972/ 、見た日 2026-11-11）。
- 公表された領域(ファイナンス、クルマ選び、おでかけ、お買い物、レシピ、推し活など)に、求人や仕事探しはなかった（出典: https://www.lycorp.co.jp/ja/news/release/020576/ 、見た日 2026-11-11）。
- 推測: LINEヤフーは「LINEバイト」「LINEスキマニ」を持つため、仕事探しの領域を足す余地はある。発表は見つからなかった。

## 求人サービスの側から見たアシスタントとの連携

| 名前 | 対象 | していること | 提供の段階 | 出典 | 見た日 |
|---|---|---|---|---|---|
| Indeed のアプリ(ChatGPT の中) | 求職者 | プロフィールをつなぎ、合う求人を出す。応募は Indeed で | 提供中(2026-02-10 発表)。国の範囲は記載なし | https://www.indeed.com/news/releases/indeed-launches-app-in-chatgpt?co=US | 2026-11-11 |
| Indeed Apply For Me | 求職者 | プロフィールから応募の中身を下書き。自動で出す型は止め、人が見てから出す型に絞った | 米国の一部で試験(2026-07 発表、2026-08 更新) | https://www.indeed.com/news/releases/indeed-tests-apply-for-me-job-search?co=US | 2026-11-11 |
| LinkedIn Hiring Pro(Claude の中) | 企業(中小) | 求人の原稿を作り、承認後に LinkedIn に載せ、候補者を絞る | Claude で提供中、Copilot は近く(2026-10-21 発表) | https://news.linkedin.com/2026/making-it-easier-for-small-businesses-to-hire-on-linkedin | 2026-11-11 |

- Indeed の Apply For Me は、汎用アシスタントではなく Indeed の中の機能。応募の代行は、求人サービスの中でも試験の段階で、自動の型は止めている（出典: https://www.indeed.com/news/releases/indeed-tests-apply-for-me-job-search?co=US 、見た日 2026-11-11）。

## 「求職に関係するデータだけを見せ、ほかは遮断する」はできるか

### 事実(各社の文書に書いてあること)

- 権限の単位は、アプリ(コネクタ)、ツール(操作)、サイトのどれか。
  - Claude: ツールごとに「常に許可 / 承認が要る / 禁止」。決めるのは Team と Enterprise の管理者（出典: https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities 、見た日 2026-11-11）。
  - Claude in Chrome: 使ってよいサイトと禁止のサイトの一覧。決めるのは管理者（出典: https://support.claude.com/en/articles/12012173-getting-started-with-claude-in-chrome 、見た日 2026-11-11）。
  - Gemini: アプリの操作ごとに「常に許可 / 常に聞く」（出典: https://support.google.com/gemini/answer/18766567?hl=en 、見た日 2026-11-11）。
  - ChatGPT のアプリ: ツールごとの OAuth の範囲（出典: https://developers.openai.com/apps-sdk/build/auth 、見た日 2026-11-11）。
  - xAI の API: `allowed_tools` でツールを絞る（出典: https://docs.x.ai/docs/guides/tools/remote-mcp-tools 、見た日 2026-11-11）。
- コネクタは、つないだサービスの本人の権限をそのまま引き継ぐ。Claude 側では狭めるだけ（出典: https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities 、見た日 2026-11-11）。
- Gemini が手元の Chrome を使うと、本人がログインしているサイトすべてに入れる（出典: https://support.google.com/gemini/answer/16596215 、見た日 2026-11-11）。
- 記憶を分ける仕組みはある。Claude はプロジェクトごとの記憶と、アカウントの記憶を切るスイッチを持つ（出典: https://support.claude.com/en/articles/11817273-using-claude-s-chat-search-and-memory-to-build-on-previous-context 、見た日 2026-11-11）。
- Gemini では、アプリを切っても、活動の記録に入ったデータは消えない（出典: https://support.google.com/gemini/answer/13594961 、見た日 2026-11-11）。
- Gemini は、健康、金融、政府の ID を渡す前に止まる。これは「種類」で止める数少ない例だが、守る方向の仕組みで、見せる範囲を決める仕組みではない（出典: https://support.google.com/gemini/answer/16596215 、見た日 2026-11-11）。
- 「データの中身の種類(例: 求職に関係するメールだけ)」で範囲を決める設定は、調べた 9 件のどれにも見つからなかった。

### 推測

- 推測: 「Gmail をつなぐ」と決めた時点で、検索のツールは全部のメールに届く。求職のメールだけに絞るには、つなぐ先のサービスの側で、範囲の狭い口を用意する必要がある。
- 推測: 近いことは今でもできる。求職専用のメールのアカウントやブラウザのプロフィールを作り、求人サービスのアプリだけをつなぎ、Claude のプロジェクトのように記憶を分ける。ただし本人がこれを組む手間が大きい。
- 推測: 汎用アシスタントの記憶は、会話の全体から作られる。求職の話をほかの話と分けて保つ保証は、プロジェクトなどで分けない限りない。
- 推測: 個人向けのプランでは、ツールごとの細かい設定を本人が持てないことがある(Claude は管理者だけ)。求職者が自分で境界を決める形は、まだ弱い。

## このプロダクトへの示唆

- 推測: 求職者向けの差は「データの種類で区切った境界」を初めから持つこと。汎用アシスタントの単位はアプリ、ツール、サイトで、求職という目的で区切っていない。
- 推測: 汎用アシスタントと戦うより、その中に出る形(MCP のコネクタ、ChatGPT の plugins、Gemini の Connected Apps)を持つ方が届きやすい。Indeed と LinkedIn はこの道を先に選んでいる。
- 推測: その時、このプロダクトの MCP サーバーが「求職に関係するデータだけ」を返す口になれる。範囲の狭いツールと OAuth の範囲を自分で設計できるため。
- 推測: 応募の代行は、各社とも「送る前に人が見る」に寄っている。Indeed も自動の応募を止めた。初めは下書きと承認の型で作るのが安全。
- 推測: 記憶を見る、直す、消す、は各社の標準になった。求職のデータも、見える、消せる、どこで使ったかが分かる、の 3 つを最低限にする。
- 推測: 国内では LINEヤフーの Agent i が、領域ごとのエージェントを増やしている。仕事探しの領域が足されると、国内の求職者の入口として強い相手になる。

## 見つからなかったこと

- OpenAI の公式のページ(openai.com、help.openai.com)は 403 で開けなかった。ChatGPT agent の確認の手順、記憶の見方と消し方、Atlas の廃止の日付は、本文で確かめられなかった。
- OpenAI の Jobs Platform(2025-09-04 発表)の、今の提供の段階。
- 「ChatGPT Jobs」という名の機能。
- Grok と X の求人の機能の関係。x.ai、help.x.com、x.com は開けなかった。
- 個人向けの Microsoft Copilot の操作(Actions)、記憶、コネクタのヘルプ。
- Perplexity Comet のエージェントの権限と確認の手順。
- Apple の Siri AI の権限の決め方と記憶の扱い。
- Meta の Muse の記憶の扱い。以前の Meta AI との関係。
- Project Mariner の今の状態。
- 汎用アシスタントが、応募の代行を一般提供した例。
- データの種類で見せる範囲を決める設定(どの汎用アシスタントにも)。
- このターンでは Web 検索の上限に達していたため、検索で新しい発表を広く探すことはできなかった。上の「見つからなかった」には、検索できていれば見つかったものが含まれる可能性がある。
