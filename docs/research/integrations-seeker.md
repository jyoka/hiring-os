# 求職者の側: スマホのアプリが自動で集められるもの(2026-11 時点)

## 結論

- iOS のアプリは、ほかのアプリの中身、通知、メール、SMS、画面を読めない。読めるのは、本人が許可した予定、連絡先、写真、位置と、本人が共有の口や選ぶ画面(ピッカー)で渡したものだけだ。iOS 27 の App Intents も、自分のアプリの中身を Siri に「出す」向きで、Siri が持つ個人の文脈を読む API は見つからなかった。
- Android は iOS より広い。本人が設定で許可すれば、通知アクセス(NotificationListenerService)で全アプリの通知を読める。既定のアシスタントに選ばれれば、呼ばれた時の画面の文字と画面写真を受け取れる。ただし Play の方針が強く縛る。SMS は既定の SMS かアシスタントのアプリに、通話履歴は既定の電話かアシスタントのアプリに限る。AccessibilityService で「自律で計画して動く」使い方は禁止だ。
- 他社のアプリの機能をエージェントから呼ぶ口(Android の AppFunctions、iOS の App Intents)は、OS の側の Gemini や Siri だけが呼べる。第三者のエージェントのアプリが他社の AppFunctions を呼ぶには特権の権限が要り、システムのアシスタントにしか与えないと Google は書いている。
- メールは OS からは読めず、各社の API か IMAP でつなぐ。Gmail は本文を広く読む scope(`gmail.readonly` など)が restricted で、審査が要る。アドオンの中で開いたメッセージだけを読む scope は sensitive だ。restricted のデータをサーバーに保存するか送るなら、12 か月ごとのセキュリティ評価(CASA)も要る。Outlook は Mail.Read を個人の Microsoft アカウントでも本人の同意だけで使える。iCloud メールは公開の API が見つからず、IMAP とアプリ用パスワードになる。
- 求人サイトの応募の記録を本人が自分で書き出せる機能は、LinkedIn だけ確かめられた。Indeed は申請の書式で約 1 か月かかる。国内の大手は、自分で書き出す機能が見つからず、個人情報保護法の開示請求(第 33 条)が道になる。第 33 条は電磁的記録での開示を本人が選べるが、形式は事業者が決められる。
- 汎用アシスタントのアプリのうち、端末の個人データを最も広く集めるのは Gemini(Android)だった。Play の Data safety に連絡先、予定、SMS、メール、入っているアプリの一覧を(任意として)載せている。ChatGPT と Claude のスマホのアプリは、主に本人が入力したものと、許可した予定や位置などに限られる。
- 推測: 「求職の金庫」の「求職のデータだけ」は、OS の許可の単位では表せない。通知アクセスは全アプリ、Gmail の scope はメールボックス全体になる。端末の中で求職のものだけを選び、それ以外は端末の外に出さない設計にすれば、ストアの表示の「収集」に当たる範囲を減らせる。Gmail のセキュリティ評価の条件(サーバーに保存か送信)も避けられる可能性がある。

## 比べる表

| データの種類 | iOS | Android | ストアの審査 | 出典 | 見た日 |
|---|---|---|---|---|---|
| ほかのアプリの中身 | 読めない。アプリは自分の領域の外を読み書きできない | 読めない。例外は既定のアシスタントが呼ばれた時の画面と、AccessibilityService。他社の AppFunctions を呼ぶのは特権 | Apple 2.5.2 で禁止。Play は入っているアプリの一覧も個人の機微なデータとして扱う | https://developer.apple.com/app-store/review/guidelines/ 、https://developer.android.com/ai/appfunctions | 2026-11-18 |
| 通知 | 読めない(公開の API は見つからなかった)。BLE の周辺機器向けの ANCS はある | 本人が通知アクセスを許可すれば、全アプリの通知を読める。Android 15 から、信頼されないアプリには OTP を伏せる | Play に専用の方針は見つからなかった。ユーザーデータの方針の開示と同意が要る | https://developer.android.com/about/versions/15/behavior-changes-all | 2026-11-18 |
| メール | 標準のメールを読む API はない(MailKit は macOS だけ)。Gmail API、Microsoft Graph、IMAP でつなぐ | 同じ。端末の Gmail を読む口はなく、API か IMAP | Gmail の本文を広く読む scope は restricted で審査。サーバーに保存か送信ならセキュリティ評価 | https://developer.apple.com/documentation/mailkit 、https://developers.google.com/workspace/gmail/api/auth/scopes | 2026-11-18 |
| SMS | 読めない。迷惑 SMS の振り分けの拡張だけ。知らない送信者に限り、ネットに直接出られない | READ_SMS などはある。Android 17 から OTP 入りの SMS は多くのアプリに 3 時間遅れで届く | Play は既定の SMS かアシスタントに限る。例外の一覧に求職の用途はない | https://developer.apple.com/documentation/identitylookup/sms-and-mms-message-filtering 、https://support.google.com/googleplay/android-developer/answer/9888170?hl=en | 2026-11-18 |
| 予定 | 本人の許可で読める(全部を読む許可)。書くだけの許可もある | READ_CALENDAR で読める | Apple 5.1.1(iii) 必要なものだけ | https://developer.apple.com/documentation/eventkit/accessing-the-event-store 、https://developer.android.com/identity/providers/calendar-provider | 2026-11-18 |
| 連絡先 | 全部か、本人が選んだ一部(iOS 18 から) | READ_CONTACTS か、Android 17 の連絡先ピッカー | Play は 2027-01-27 から、広い読み取りが要らないアプリにピッカーを求める | https://developer.apple.com/documentation/contactsui/contactaccessbutton 、https://support.google.com/googleplay/android-developer/table/12921780?hl=en | 2026-11-18 |
| 写真 | 全部か、本人が選んだ一部。PHPicker は許可なしで選んだものだけ | フォトピッカー。READ_MEDIA_IMAGES は中心の機能に要る時だけ | Play は 2025-05-28 から写真と動画の方針を全面適用 | https://developer.apple.com/documentation/photokit/delivering-an-enhanced-privacy-experience-in-your-photos-app 、https://support.google.com/googleplay/android-developer/answer/14115180?hl=en | 2026-11-18 |
| 位置 | 使っている間か、常に | 位置のボタン(Android 17)で、その場だけの正確な位置 | Play は 2027-01-27 から、1 回きりの正確な位置にボタンを勧める | https://developer.apple.com/documentation/corelocation/requesting-authorization-to-use-location-services 、https://support.google.com/googleplay/android-developer/table/12921780?hl=en | 2026-11-18 |
| 共有の口 | Share extension。本人が共有を選んだ時だけ | ACTION_SEND の受け口。本人が共有を選んだ時だけ | 本人が始めた共有は、Play の「共有」の開示から外れる | https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/Share.html 、https://developer.android.com/training/sharing/receive | 2026-11-18 |
| ショートカット | App Intents で自分の機能と中身を Siri、Spotlight、ショートカットに出す。iOS 27 の Siri AI はベータ | App Actions(Google アシスタント)。AppFunctions は実験的で、Gemini とは開発者プレビューでつなぐ | Play は AppFunctions の方針を 2027-04-14 に施行 | https://developer.apple.com/apple-intelligence/ 、https://developer.android.com/ai/appfunctions | 2026-11-18 |
| 画面の読み取り | ほかのアプリの画面は読めない。ReplayKit の配信は本人が始めた時だけ | AccessibilityService、既定のアシスタントの Assist API。Gemini の画面の自動操作はベータ | Play は AccessibilityService での自律の操作を禁止。アシスタントは障害者向けの道具に当たらない | https://support.google.com/googleplay/android-developer/answer/10964491?hl=en 、https://developer.android.com/training/articles/assistant | 2026-11-18 |

## 1. iOS

### 今の版

- 公開の最新は iOS 27.2.1(2026-11-09)。iOS 27.3 はベータ 2(2026-11-16)だ(出典: https://developer.apple.com/news/releases/ 、見た日 2026-11-18)。
- iOS 27.0.1 は 2026-09-28 に出た。iOS 26 の最新は 26.6.2(2026-09-08)(出典: 同上、見た日 2026-11-18)。

### ほかのアプリの中身

- アプリは自分の領域の外を読み書きできない。App Review Guidelines 2.5.2 が定める(出典: https://developer.apple.com/app-store/review/guidelines/ 、見た日 2026-11-18)。
- 公開の API だけを使う決まりもある(2.5.1)(出典: 同上、見た日 2026-11-18)。
- iOS 27 の開発者向けの説明は、App Intents の entity schema を「自分のアプリの中身を Spotlight の意味の索引に足す」ものとしている(出典: https://developer.apple.com/apple-intelligence/ 、見た日 2026-11-18)。
- View Annotations API は、自分の画面の部品を entity に結び付け、Siri が画面の内容を扱えるようにする(出典: 同上、見た日 2026-11-18)。
- 第三者のアプリが Siri の個人の文脈やほかのアプリの索引を読む API は、見つからなかった。

### 通知

- ほかのアプリの通知を読む公開の API は、見つからなかった。
- Notification Service Extension は、自分のアプリに届くリモート通知を表示の前に書き換える口だ(出典: https://developer.apple.com/documentation/usernotifications/unnotificationserviceextension 、見た日 2026-11-18)。
- ANCS は、Bluetooth LE の周辺機器が iPhone の通知を読む仕組みだ。アプリではなく周辺機器の側の口だ(出典: https://developer.apple.com/library/archive/documentation/CoreBluetooth/Reference/AppleNotificationCenterServiceSpecification/Introduction/Introduction.html 、見た日 2026-11-18)。

### メール

- MailKit(メールのアプリを拡張する口)は macOS 12 以降だけで、iOS にはない(出典: https://developer.apple.com/documentation/mailkit 、見た日 2026-11-18)。
- iOS の標準のメールの中身を読む API は、見つからなかった。メールは各社の API か IMAP でつなぐ(4 節)。

### SMS

- 使えるのは Message Filter の拡張だけ。知らない送信者の SMS と MMS を、迷惑かどうか判定する(出典: https://developer.apple.com/documentation/identitylookup/sms-and-mms-message-filtering 、見た日 2026-11-18)。
- 連絡先にいる送信者のメッセージと iMessage には働かない(出典: 同上、見た日 2026-11-18)。
- 拡張は直接ネットに出られない。本体のアプリと共有する領域にも書き込めない(出典: 同上、見た日 2026-11-18)。

### 予定

- iOS 17 から、予定の許可は「書くだけ」と「全部」の 2 つ。読むだけの許可はない(出典: https://developer.apple.com/documentation/eventkit/accessing-the-event-store 、見た日 2026-11-18)。
- 書くだけの許可では、既存の予定は読めない。自分が作った予定も読めない(出典: 同上、見た日 2026-11-18)。
- EventKitUI の編集画面は別のプロセスで動く。許可なしで予定を作らせられる(出典: 同上、見た日 2026-11-18)。

### 連絡先

- iOS 18 から、本人は連絡先の全部か、選んだ一部だけをアプリに渡せる(出典: https://developer.apple.com/documentation/contacts/cnauthorizationstatus/limited 、見た日 2026-11-18)。
- ContactAccessButton で、アプリの検索の画面から連絡先を 1 件ずつ足してもらえる(出典: https://developer.apple.com/documentation/contactsui/contactaccessbutton 、見た日 2026-11-18)。

### 写真

- iOS 14 から、本人が選んだ写真だけを渡す「限られたライブラリ」がある(出典: https://developer.apple.com/documentation/photokit/delivering-an-enhanced-privacy-experience-in-your-photos-app 、見た日 2026-11-18)。
- PHPickerViewController は別のプロセスで動く。許可なしで、選んだ写真だけを受け取れる(出典: 同上、見た日 2026-11-18)。

### 位置

- 許可は「使っている間」と「常に」の 2 つ。「常に」は必要な時だけ求めるよう Apple は書いている(出典: https://developer.apple.com/documentation/corelocation/requesting-authorization-to-use-location-services 、見た日 2026-11-18)。

### 共有の口

- Share extension は、本人がほかのアプリの共有ボタンから選んだ時だけ動く(出典: https://developer.apple.com/library/archive/documentation/General/Conceptual/ExtensibilityPG/Share.html 、見た日 2026-11-18)。
- 推測: 求人のページ、応募の完了の画面の画面写真、メールの本文を、本人が 1 回ずつ渡す道になる。

### ショートカット(App Intents、Siri)

- App Intents は iOS 16 から。アプリの操作と中身を、Siri、Spotlight、ショートカット、アクションボタン、ウィジェットに出す(出典: https://developer.apple.com/documentation/appintents 、見た日 2026-11-18)。
- iOS 27 では、schema に合わせると、決まった言い回しなしで Siri AI から呼ばれる(出典: https://developer.apple.com/ios/ 、見た日 2026-11-18)。
- Siri AI は iOS 27 でベータ。EU の iOS では最初は出さない(出典: https://www.apple.com/apple-intelligence/ 、見た日 2026-11-18)。
- 言語は、本文は英語、脚注は英語、フランス語、日本語、韓国語、ポルトガル語、スペイン語と書く。ページの中で食い違う(出典: 同上、見た日 2026-11-18)。
- 日本では iOS 26.2 から、声で会話するアプリをサイドボタンで起動できる API が入った。スマホ新法(MSCA)への対応だ(会社の発表)(出典: https://www.apple.com/newsroom/2025/12/apple-announces-changes-to-ios-in-japan/ 、見た日 2026-11-18)。
- Foundation Models framework(iOS 26 から)で、端末の中のモデルを使える。iOS 27 では、決まった型に合う他社のモデルも同じ API で使える(出典: https://developer.apple.com/documentation/foundationmodels 、見た日 2026-11-18)。

### 画面の読み取り

- ほかのアプリの画面を読む公開の API は、見つからなかった。
- ReplayKit で画面を録画や配信できる。配信の拡張は、本人が配信の選ぶ画面で始めた時に動く(出典: https://developer.apple.com/documentation/replaykit/rpsystembroadcastpickerview 、見た日 2026-11-18)。
- 推測: ReplayKit で求人アプリの画面を集め続ける作りは、5.1.1 と 5.1.2 の審査で通る見込みが低い。

### バックグラウンドの実行

- BGAppRefreshTask は、小さな更新を裏で短く走らせる(出典: https://developer.apple.com/documentation/backgroundtasks/bgapprefreshtask 、見た日 2026-11-18)。
- iOS 26 で BGContinuedProcessingTask が入った。前面で始めた作業を裏で続け、進み具合を Live Activity で見せる。本人は止められる(出典: https://developer.apple.com/documentation/backgroundtasks/bgcontinuedprocessingtask 、見た日 2026-11-18)。
- 裏の動作は目的の用途(VoIP、音声、位置、作業の完了など)に限る(2.5.4)(出典: https://developer.apple.com/app-store/review/guidelines/ 、見た日 2026-11-18)。

## 2. Android

### 今の版

- Android 17 は 2026-06-16 に Pixel 向けに安定版が出た(報道)(出典: https://androidauthority.com/android-17-stable-rollout-features-3675016 、見た日 2026-11-18)。
- 公式のリリースノートで確かめられたのは、Beta 3 で API が固まったこと(2026-03)、Beta 4.1 が 2026-06-01 に出たことまで(出典: https://developer.android.com/about/versions/17/release-notes 、見た日 2026-11-18)。

### ほかのアプリの中身

- AppFunctions は、アプリの機能を端末の中の MCP のような「道具」として出す API。Android 16 以降。実験的なプレビューだ(出典: https://developer.android.com/ai/appfunctions 、見た日 2026-11-18)。
- Gemini から使わせるには、Connected Apps Platform の開発者プレビューに申し込む(出典: 同上、見た日 2026-11-18)。
- 自分のエージェントから他社の AppFunctions を呼ぶには `EXECUTE_APP_FUNCTIONS` が要る。これは特権の権限で、認められたシステムのアシスタントにだけ与える、と書いている(出典: 同上、見た日 2026-11-18)。
- 権限の一覧では、`EXECUTE_APP_FUNCTIONS` の保護の段階は normal で、実行の時に許可リストで確かめるとある。説明が 2 つのページで食い違う(出典: https://developer.android.com/reference/android/Manifest.permission 、見た日 2026-11-18)。

### 通知

- NotificationListenerService は、`BIND_NOTIFICATION_LISTENER_SERVICE` を宣言し、システムがつなぐ(出典: https://developer.android.com/reference/android/service/notification/NotificationListenerService 、見た日 2026-11-18)。
- 本人が設定で通知へのアクセスを許可する手順は、このページに書いていない。
- Android 15 から、信頼されないリスナーには、OTP を含む通知の中身を伏せる(出典: https://developer.android.com/about/versions/15/behavior-changes-all 、見た日 2026-11-18)。
- 推測: 求人アプリや LINE の通知から、応募の返事や面接の連絡を拾える。ただし許可は全アプリの通知になる。

### メール

- 端末の Gmail のアプリの中身を読む口は、見つからなかった。Gmail API か IMAP を使う(4 節)。

### SMS

- Android 17 から、WebOTP の形の SMS は、宛先でないアプリには 3 時間遅れで届く。全アプリが対象(出典: https://developer.android.com/about/versions/17/behavior-changes-all 、見た日 2026-11-18)。
- Android 17 を対象にしたアプリでは、普通の SMS の OTP も 3 時間遅れる。既定の SMS のアシスタントのアプリなどは除く(出典: https://developer.android.com/about/versions/17/behavior-changes-17 、見た日 2026-11-18)。

### 予定、連絡先、写真、位置

- 予定は READ_CALENDAR で読み、WRITE_CALENDAR で書く(出典: https://developer.android.com/identity/providers/calendar-provider 、見た日 2026-11-18)。
- Android 17 の連絡先ピッカーは、本人が選んだ連絡先の、求めた項目だけを一時的に読ませる。READ_CONTACTS の代わりになる(出典: https://developer.android.com/about/versions/17/features/contact-picker 、見た日 2026-11-18)。
- Android 17 を対象にしたアプリは、連絡先の data の表から、アカウント名などの列が見えなくなる(出典: https://developer.android.com/about/versions/17/behavior-changes-17 、見た日 2026-11-18)。
- フォトピッカーは、選んだ写真と動画だけをアプリに渡す(出典: https://developer.android.com/training/data-storage/shared/photo-picker 、見た日 2026-11-18)。
- Android 17 の位置のボタンは、押した時だけ正確な位置を渡す。ダイアログは出ない(出典: https://developer.android.com/about/versions/17/release-notes 、見た日 2026-11-18)。

### 共有の口

- `ACTION_SEND` と `ACTION_SEND_MULTIPLE` の受け口を宣言すると、共有の一覧に出る。本人が選ぶと開く(出典: https://developer.android.com/training/sharing/receive 、見た日 2026-11-18)。
- 画面写真を共有する時、ページの URL も一緒に渡せる(出典: 同上、見た日 2026-11-18)。
- Android 18 から、共有の時の URI の読み取り許可は自動で付かなくなる予定(出典: https://developer.android.com/about/versions/17/behavior-changes-all 、見た日 2026-11-18)。

### ショートカット(App Actions、Gemini との連携)

- App Actions は、Google アシスタントから声でアプリの機能を開く仕組み。組み込みの intent を `shortcuts.xml` で宣言する(出典: https://developer.android.com/develop/devices/assistant/overview 、見た日 2026-11-18)。
- このページに、廃止や Gemini への移行の記載はなかった。
- Gemini との連携は、AppFunctions と Connected Apps(開発者プレビュー)が道になる(出典: https://developer.android.com/ai/appfunctions 、見た日 2026-11-18)。

### 画面の読み取り

- 本人は既定のアシスタントのアプリを選べる。アシスタントは呼ばれた時に、画面の文字と部品の構造(AssistStructure)と画面写真を受け取る(出典: https://developer.android.com/training/articles/assistant 、見た日 2026-11-18)。
- 画面の文字と画面写真を渡すかは、本人が設定で決める。FLAG_SECURE の画面は渡らない(出典: 同上、見た日 2026-11-18)。
- 次の版の参照文書には、画面の中身を受け取るのに `READ_ASSIST_STRUCTURE_SCREEN_CONTENT` が要る、と注記がある(出典: https://developer.android.com/reference/android/Manifest.permission 、見た日 2026-11-18)。
- Android 17 を対象にしたアプリでは、Content Capture を止めるのに FLAG_SECURE を使う。端末の AI が画面を解析するためだ(出典: https://developer.android.com/about/versions/17/behavior-changes-17 、見た日 2026-11-18)。
- AccessibilityService は技術的には画面を読めるが、Play の方針が強く縛る(3 節)。

### バックグラウンドの実行

- Android 15 から、正しいライフサイクルの外で始めた通信は例外になる。裏の通信は WorkManager か前面サービスを使う(出典: https://developer.android.com/about/versions/15/behavior-changes-all 、見た日 2026-11-18)。
- Android 17 から、端末のメモリの量に応じたアプリのメモリの上限が入った(出典: https://developer.android.com/about/versions/17/behavior-changes-all 、見た日 2026-11-18)。
- Play は 2027-01-27 から、ジオフェンスを前面サービスの認める用途から外す(出典: https://support.google.com/googleplay/android-developer/table/12921780?hl=en 、見た日 2026-11-18)。

## 3. アプリストアの審査

### App Store(Apple)

- 5.1.1(ii): 集める前に同意が要る。有料の機能を同意の条件にしてはいけない。同意の取り消しを簡単にする(出典: https://developer.apple.com/app-store/review/guidelines/ 、見た日 2026-11-18)。
- 5.1.1(iii): 中心の機能に関係するデータだけを求める。写真や連絡先は、できればピッカーか共有シートを使う(出典: 同上、見た日 2026-11-18)。
- 5.1.1(v): ソーシャルネットワークの資格情報やトークンを、端末の外に保存してはいけない(出典: 同上、見た日 2026-11-18)。
- 5.1.1(viii): 本人から直接ではない所から個人情報を集めるアプリは認めない。公開のデータベースでも同じ(出典: 同上、見た日 2026-11-18)。
- 5.1.2(i): 個人データを第三者に渡す時は、渡す先を明示し、明確な許可を得る。第三者の AI も含むと明記している(出典: 同上、見た日 2026-11-18)。
- 5.1.2(ii)(iii): 別の目的に使い回すには再び同意が要る。集めたデータでこっそり利用者の像(プロフィール)を作ってはいけない(出典: 同上、見た日 2026-11-18)。
- 5.1.2(iv): 連絡先や写真の API から、自社用の連絡先のデータベースを作ってはいけない(出典: 同上、見た日 2026-11-18)。
- 5.2.2: 第三者のサービスの中身を使うなら、その利用規約で許されている必要がある(出典: 同上、見た日 2026-11-18)。
- App Privacy の表示: 「収集」は、すぐの処理に要る時間を超えて読める形で端末の外に送ることを指す。端末の中だけの処理は収集に当たらない(出典: https://developer.apple.com/app-store/app-privacy-details/ 、見た日 2026-11-18)。
- データの種類に「メールやテキストメッセージ」「連絡先」「写真や動画」などがある。組み込んだ SDK の収集も含めて表示する(出典: 同上、見た日 2026-11-18)。
- 改定の日付は、このページの取れた範囲には書いていなかった。

### Google Play

- SMS と通話履歴: SMS は既定の SMS かアシスタント、通話履歴は既定の電話かアシスタントのアプリとして登録されていることが条件。外れたらすぐ使うのをやめる(出典: https://support.google.com/googleplay/android-developer/answer/9888170?hl=en 、見た日 2026-11-18)。
- 例外の一覧には、バックアップ、端末の自動化、SMS での金融取引や家計管理などがある。求職やアシスタントの例外はない(出典: https://support.google.com/googleplay/android-developer/answer/9047303?hl=en 、見た日 2026-11-18)。
- AccessibilityService: 障害のある人が端末を使うための道具だけが「アクセシビリティの道具」に当たる。アシスタントや自動化の道具は当たらない(出典: https://support.google.com/googleplay/android-developer/answer/10964491?hl=en 、見た日 2026-11-18)。
- 自律で動作を始め、計画し、実行する使い方は禁止。人が決めた固定の手順の自動化は禁止していない(出典: 同上、見た日 2026-11-18)。
- この禁止の明確化は 2025-10 の更新で、2026-01-01 に施行された(報道と検索結果)。Play の施行日の表は 2026-08-26 以降の分しか載っておらず、一次情報で日付は確かめられなかった。
- アクセシビリティの道具でないアプリは、アプリの中で開示し、本人の積極的な同意を得て、申告の書式と動画を出す(出典: 同上、見た日 2026-11-18)。
- すべてのファイルへのアクセス: ファイル管理、バックアップ、ウイルス対策、端末内の検索などに限る。メディアのファイルを読む目的には使えない(出典: https://support.google.com/googleplay/android-developer/answer/10467955?hl=en 、見た日 2026-11-18)。
- NotificationListenerService だけを扱う Play の方針のページは、見つからなかった。ユーザーデータの方針の開示と同意が当たる。
- ユーザーデータの方針: 本人が予想しない収集(裏での収集など)は、アプリの中で開示し、積極的な同意を得てから始める(出典: https://support.google.com/googleplay/android-developer/answer/10144311?hl=en 、見た日 2026-11-18)。
- 入っているアプリの一覧も、個人の機微なデータとして扱う。第三者の AI を組み込む場合にも方針が当たる(出典: 同上、見た日 2026-11-18)。
- 写真と動画: READ_MEDIA_IMAGES などは、写真と動画の広い読み取りが中心の機能のアプリに限る。2025-05-28 から全面適用(出典: https://support.google.com/googleplay/android-developer/answer/14115180?hl=en 、見た日 2026-11-18)。
- これからの施行(出典: https://support.google.com/googleplay/android-developer/table/12921780?hl=en 、見た日 2026-11-18):
  - 2027-01-27: 広い連絡先の読み取りが要らないアプリは連絡先ピッカーを使う。正確な位置は位置のボタンを勧める。電話での本人確認は READ_CALL_LOG の用途から外れる。
  - 2027-04-14: AppFunctions の方針。AI エージェントを欺いたり操作したりすることを禁じる。
  - 2027-08-25: 連絡先の管理の権限は申告が要る。
- Data safety: 公開しているアプリはすべて書く。SDK の収集も含む。端末の中だけの処理と、本人が始めた共有は開示から外れる(出典: https://support.google.com/googleplay/android-developer/answer/10787469?hl=en 、見た日 2026-11-18)。

## 4. メールの API

### Gmail API

- 本文を読む `gmail.readonly`、全権の `https://mail.google.com/`、ヘッダーだけの `gmail.metadata` は、どれも restricted(出典: https://developers.google.com/workspace/gmail/api/auth/scopes 、見た日 2026-11-18)。
- restricted ではないのは、アドオンの中で本人が開いたメッセージだけを読む scope など(sensitive)(出典: 同上、見た日 2026-11-18)。
- `gmail.metadata` では、検索の条件 `q` を使えない(出典: https://developers.google.com/workspace/gmail/api/reference/rest/v1/users.messages/list 、見た日 2026-11-18)。
- restricted scope の審査は、公開のアプリに要る。少数の知り合いだけが使う個人の用途、テスト中、組織の中だけのアプリは除く(出典: https://developers.google.com/identity/protocols/oauth2/production-readiness/restricted-scope-verification 、見た日 2026-11-18)。
- restricted のデータをサーバーに保存するか送るなら、セキュリティ評価が要る。12 か月ごとに受け直す(出典: 同上、見た日 2026-11-18)。
- Google の今の説明は、評価の段階を AL1 と AL2 に分ける。AL2 になると、翌年以降も AL2 で評価する(出典: https://support.google.com/cloud/answer/13465431?hl=en 、見た日 2026-11-18)。
- 費用の一次情報(Google の価格表)は、見つからなかった。評価をする会社の 1 つ、Leviathan Security は、AL1 を 3,000〜6,000 ドルと載せている(会社の発表)(出典: https://www.leviathansecurity.com/programs/google-casa-cloud-application-security-assessment 、見た日 2026-11-18)。
- Gmail の scope で認める用途は、メールのクライアント、自動のバックアップ、生産性を上げるもの(生成 AI の要約を含む)、メールの情報で報告や監視をするもの(出典: https://developers.google.com/workspace/workspace-api-user-data-developer-policy 、見た日 2026-11-18)。
- 1 回きりか手動のメールの書き出しは認めない(出典: 同上、見た日 2026-11-18)。
- データを AI のモデルの学習に使うのは禁止。その本人だけの個人向けのモデルは除く(出典: 同上、見た日 2026-11-18)。

### Microsoft Outlook(Microsoft Graph)

- 委任の Mail.Read は、本人のメールボックスを読む。管理者の同意は要らない。個人の Microsoft アカウントでも同意できる(出典: https://learn.microsoft.com/en-us/graph/permissions-reference 、見た日 2026-11-18)。
- Mail.ReadBasic は、本文、プレビュー、添付を除いて読む。これも個人のアカウントで同意できる(出典: 同上、見た日 2026-11-18)。
- publisher verification は無料。Microsoft AI Cloud Partner Program の確認済みのアカウントが要る。職場か学校のアカウントで登録したアプリだけが対象(出典: https://learn.microsoft.com/en-us/entra/identity-platform/publisher-verification-overview 、見た日 2026-11-18)。
- 2020-11 から、テナントの設定によっては、確認のない複数テナントのアプリに利用者が同意できない(出典: 同上、見た日 2026-11-18)。
- 個人のアカウントの同意に publisher verification が要るかは、見つからなかった。

### iCloud メール

- 第三者のアプリ向けの iCloud メールの公開 API は、見つからなかった。
- IMAP は imap.mail.me.com(993 番)。パスワードはアプリ用パスワードを使う。POP は使えない(出典: https://support.apple.com/en-us/102525 、見た日 2026-11-18)。
- アプリ用パスワードは 2 ファクタ認証が条件で、最大 25 個。本体のパスワードを変えると全部無効になる(出典: https://support.apple.com/en-us/102654 、見た日 2026-11-18)。
- 同じページに「一部の対応アプリは Apple Account で認可できる」とあるが、仕組みの詳細は書いていなかった(出典: 同上、見た日 2026-11-18)。

### 国内のメール

- ドコモメールは IMAP に対応したアプリで使える。dアカウントの設定と、dアカウントとは別の IMAP 専用のパスワードが要る(出典: https://www.docomo.ne.jp/service/docomo_mail/other/ 、見た日 2026-11-18)。
- Yahoo!メールは、他社のメールソフトから IMAP で使える。LINEヤフーは「海外からのアクセス制限」を順に有効にし、IMAP がつながらなくなる場合がある(報道)(出典: https://scan.netsecurity.ne.jp/article/2025/08/19/53453.html 、見た日 2026-11-18)。Yahoo!メールの公式のヘルプは開いていない。
- au と ソフトバンクのメールは調べていない。

## 5. 求人サイトの応募の記録の持ち出し

### 書き出しの機能

| サービス | 本人が持ち出す方法 | 応募の記録 | 時間 | 出典 | 見た日 |
|---|---|---|---|---|---|
| LinkedIn | 設定から「データのダウンロード」 | 含む(応募した求人、日付、会社名、職名)。保存した求人、希望条件も | 項目を選ぶと数分、全部は 24 時間以内。72 時間ダウンロードできる | https://www.linkedin.com/help/linkedin/answer/a1339364 | 2026-11-18 |
| Indeed | 個人データの申請の書式 | Indeed に載った求人への応募だけ。他社のサイトでの応募は含まない | 約 1 か月 | https://www.indeed.com/help/job-seekers/articles/10652026126605-requesting-or-deleting-your-data | 2026-11-18 |
| リクルート(リクナビNEXT、タウンワークなど) | サービスの窓口に開示を申し出る。郵送の開示は返信用切手 1,000 円分 | ページにサービス名の記載なし | 記載なし | https://www.recruit.co.jp/privacy/settings/request/ | 2026-11-18 |
| マイナビ(マイナビ転職) | 個人情報保護の問い合わせの窓口 | 見つからなかった | 見つからなかった | https://www.mynavi.jp/privacy/ | 2026-11-18 |
| ディップ(バイトル) | 方針のページは 403 で開けなかった | 不明 | 不明 | https://www.dip-net.co.jp/privacy/ | 2026-11-18 |

- LinkedIn のファイルの形式は、ヘルプに書いていなかった。
- リクナビNEXT、マイナビ転職、タウンワーク、バイトルで、本人が応募の記録を自分で書き出す機能は見つからなかった。

### 日本: 個人情報保護法 第 33 条

- 本人は、保有個人データの開示を、電磁的記録の提供などの方法で求められる(第 33 条第 1 項)(出典: https://laws.e-gov.go.jp/api/1/lawdata/415AC0000000057 、見た日 2026-11-18)。
- 事業者は、本人が求めた方法で遅滞なく開示する。その方法に多額の費用がかかるなど難しい場合は、書面でよい(第 2 項)(出典: 同上、見た日 2026-11-18)。
- 第三者提供の記録にも準用する(第 5 項)(出典: 同上、見た日 2026-11-18)。
- ガイドラインは、電磁的記録の例として、CD-ROM の郵送、メールへの添付、会員用サイトからのダウンロードを挙げる(出典: https://www.ppc.go.jp/personalinfo/legal/guidelines_tsusoku/ 、見た日 2026-11-18)。
- ファイルの形式は事業者が決められる。読みやすく、他の事業者に移しやすい形式が望ましいとする(出典: 同上、見た日 2026-11-18)。
- 手数料は、実費を考えて合理的な範囲で決める(第 38 条第 2 項、ガイドライン 3-8-8)(出典: 同上、見た日 2026-11-18)。
- 推測: 日本には GDPR のような「機械で読める形式」の義務はない。開示で受け取れても、形式がそろう保証はない。

### EU: GDPR 第 20 条

- EUR-Lex は空のページが返り、開けなかった。個人情報保護委員会の仮日本語訳で確かめた。
- 本人は、自分が提供した個人データを、構造化され、一般に使われ、機械で読める形式で受け取れる(出典: https://www.ppc.go.jp/files/pdf/gdpr-provisions-ja.pdf 、見た日 2026-11-18)。
- 条件は、同意か契約にもとづく取扱いで、自動の手段で行うこと(出典: 同上、見た日 2026-11-18)。
- 技術的にできる場合は、管理者から管理者へ直接移させる権利もある(第 2 項)(出典: 同上、見た日 2026-11-18)。

### 米国カリフォルニア州: CCPA

- 事業者は、確認できた請求から 45 日以内に、無料で開示する。1 回だけ 45 日延ばせる(1798.130(a)(2)(A))(出典: https://cppa.ca.gov/regulations/pdf/cppa_act.pdf 、見た日 2026-11-18)。
- 開示は、別の事業者へ妨げなく移せる、すぐ使える形式で出す(出典: 同上、見た日 2026-11-18)。
- PDF の版は 2024-07-15 施行の改正(AB 3286)を反映したもの(出典: 同上、見た日 2026-11-18)。

## 6. 汎用アシスタントのスマホアプリが集めているもの

App Store の App Privacy と Play の Data safety は、開発者の申告で、Apple と Google は確かめていない。

| アプリ | iOS の App Privacy(本人に結び付くデータ) | Play の Data safety(集める) | 端末のデータとの連携 | 出典 | 見た日 |
|---|---|---|---|---|---|
| ChatGPT | 健康とフィットネス、位置(おおまか)、連絡先の情報、利用者の中身、検索の履歴、識別子、利用のデータ、診断 | 個人の情報、メッセージ(アプリ内、任意)、おおまかな位置、アプリの操作、利用者の中身(任意) | ヘルプは 403 で開けなかった | https://apps.apple.com/us/app/chatgpt/id6448311069 、https://play.google.com/store/apps/datasafety?id=com.openai.chatgpt&hl=en | 2026-11-18 |
| Claude | 購入、金融、位置(おおまか)、連絡先の情報、利用者の中身(写真や動画を含む)、識別子、利用のデータ、診断 | 端末の ID、写真(任意)、個人の情報、ファイル(任意)、アプリの操作、位置(正確は任意) | iOS で予定の読み書き、リマインダー、位置、地図、健康(ベータ、米国)。既存のメッセージとメールは読まない。連絡先には直接触れない | https://apps.apple.com/us/app/claude-by-anthropic/id6473753684 、https://support.claude.com/en/articles/11869619-using-claude-with-ios-apps | 2026-11-18 |
| Gemini | 健康、購入、位置、連絡先の情報、連絡先、利用者の中身、検索と閲覧の履歴、識別子、利用のデータ、機微な情報、診断、その他 | 連絡先、予定、閲覧の履歴、入っているアプリ、音声、健康、写真、位置、メール、SMS、ファイル(多くは任意) | Android で画面の文脈、電話やメッセージの Connected Apps、画面の自動操作(ベータ) | https://apps.apple.com/us/app/google-gemini/id6477489729 、https://play.google.com/store/apps/datasafety?id=com.google.android.apps.bard&hl=en | 2026-11-18 |
| Apple Intelligence / Siri | 該当なし(OS の機能) | 該当なし | 端末の中の個人の文脈(メール、メモ、写真)。App Intents でアプリを動かす | https://www.apple.com/apple-intelligence/ | 2026-11-18 |
| Microsoft Copilot | App Store のページは 404 で開けなかった | Play のページも 404 で開けなかった | 見つからなかった | - | 2026-11-18 |

### ChatGPT

- App Privacy の版は 1.2026.307。健康とフィットネスを、分析と個人向けの調整の目的に載せている(出典: https://apps.apple.com/us/app/chatgpt/id6448311069 、見た日 2026-11-18)。
- help.openai.com は 403 で開けず、端末の連携の公式の説明は確かめられなかった。

### Claude

- iOS の予定は、読むには許可が要る。書くのはシステムの画面で許可なしにできる(出典: https://support.claude.com/en/articles/11869619-using-claude-with-ios-apps 、見た日 2026-11-18)。
- メッセージとメールは下書きを作って渡すだけ。既存のメッセージとメールは読まないと明記している(出典: 同上、見た日 2026-11-18)。
- App Store の説明は、Google Drive、Gmail、Calendar をつなげると書く(出典: https://apps.apple.com/us/app/claude-by-anthropic/id6473753684 、見た日 2026-11-18)。

### Gemini

- Privacy Hub は、モバイルで連絡先、通話とメッセージの記録、入っているアプリ、画面の中身を扱うと書く(出典: https://support.google.com/gemini/answer/13594961?hl=en 、見た日 2026-11-18)。
- 位置は常に集める。既定は IP などからのおおまかな位置で、正確な位置は許可がある時だけ(出典: 同上、見た日 2026-11-18)。
- 画面の自動操作の間は画面写真を撮る。人による確認の対象にもなる(出典: 同上、見た日 2026-11-18)。
- 画面の自動操作はベータ。英語、日本語、韓国語。日本を含む 5 か国。Pixel 10 と 11、Galaxy S26 などに限る(出典: https://support.google.com/gemini/answer/16940971?hl=en 、見た日 2026-11-18)。
- 対象の作業は、配車、旅行の予約、チケット、売り買い、食事の注文など。求人の応募は挙がっていない(出典: 同上、見た日 2026-11-18)。
- 通知を Gemini が読む公式の説明は、見つからなかった。Pixel の通知の要約は Android System Intelligence の機能だと報じられている(報道)(出典: https://9to5google.com/2025/11/13/pixel-notification-summaries/ 、見た日 2026-11-18)。

### Apple Intelligence / Siri

- Siri AI は、受信箱の奥のメールや保存したメモを探せる(出典: https://www.apple.com/apple-intelligence/ 、見た日 2026-11-18)。
- 端末の中の処理と Private Cloud Compute を使う。Apple はデータを保存しないと書く(会社の発表)(出典: 同上、見た日 2026-11-18)。
- 第三者のアプリは App Intents で中身を「出す」側で、Siri の文脈を受け取る口は見つからなかった(1 節)。

### Microsoft Copilot

- App Store と Play のページは、どちらも 404 で開けなかった。端末のデータの扱いは確かめられなかった。

## このプロダクトへの示唆

### 自動で集められる道

事実:
- メール: 本人が一度つなげば、Gmail API、Microsoft Graph、IMAP で自動で読める。Gmail は restricted scope の審査が要る。
- 予定: iOS も Android も、本人の許可で読める。面接の日程を拾える。
- 通知(Android だけ): 本人が通知アクセスを許可すれば、求人アプリやメッセージのアプリの通知を読める。
- 画面(Android だけ): 既定のアシスタントに選ばれれば、本人が呼んだ時の画面を受け取れる。

推測:
- Android の版が、iOS の版よりかなり多くを集められる。先に作るなら Android が向く。
- Gmail は「端末の中だけで読み、求職のメールだけを残す」作りにすれば、セキュリティ評価の条件(サーバーへの保存か送信)に当たらない可能性がある。restricted scope の審査は残る。
- Gmail の認める用途のうち「メールの情報で報告や監視をする」「生産性を上げる」に、応募の管理が当たる可能性がある。審査で確かめる必要がある。

### 本人の手が要る道

事実:
- 共有の口: 求人のページ、応募の完了の画面写真、メールの本文を、本人が 1 回ずつ渡す。両 OS で使え、審査で開示の負担が小さい。
- ピッカー: 写真(画面写真)、連絡先は、選んだものだけを渡す。
- 求人サイトの記録: LinkedIn は本人が書き出せる。Indeed は申請で約 1 か月。国内の大手は開示請求(郵送を含む)になる。
- Siri や Gemini から呼ぶ: iOS は App Intents、Android は App Actions と AppFunctions(プレビュー)で、本人が声や文で呼ぶ。

推測:
- 「応募したら共有ボタンで送る」を、本人の習慣にできるかが肝になる。
- 開示請求の代行は、本人の身元の確認が郵送で要る社があり、自動にはできない。

### 作れない道

事実:
- iOS で、ほかのアプリの中身、通知、メール、SMS、画面を読む。
- Android で、既定の SMS かアシスタントでないのに SMS を読む(Play の方針)。
- Android で、AccessibilityService を使い、AI が自律で求人サイトを操作する(Play の方針)。
- 第三者のアプリから、他社の AppFunctions を呼ぶ(特権の権限)。

推測:
- 「求職のデータだけ」は OS の許可では絞れない。通知アクセスも Gmail の scope も全体を渡す。絞るのはアプリのコードになる。
- そのため、端末の中で振り分け、求職のもの以外は端末の外に出さない設計が要る。これは App Privacy と Data safety の「収集」の範囲を減らす点でも効く。
- 既定のアシスタントの座は、多くの人が Gemini のまま使うと見込まれる。求職だけのために替えてもらうのは難しい。

## 見つからなかったこと

- iOS で、第三者のアプリがほかのアプリの通知や Siri の個人の文脈を読む公開の API。
- Play で、NotificationListenerService だけを扱う方針のページ。
- Play の AccessibilityService の「自律の操作の禁止」の施行日の一次情報。施行日の表は 2026-08-26 以降の分だけだった。
- Android 17 の安定版の公開日の一次情報。報道で 2026-06-16 と確かめた。
- Gmail の CASA の費用の Google の一次情報。評価する会社の価格だけ確かめた。
- 個人の Microsoft アカウントの同意に、publisher verification が要るかどうか。
- iCloud メールの公開 API。アプリ用パスワードのページの「Apple Account で認可」の仕組み。
- リクナビNEXT、マイナビ転職、タウンワーク、バイトルの、応募の記録の書き出しの機能。マイナビとディップの開示請求の手順(ディップは 403)。
- LinkedIn の書き出しのファイルの形式。
- Microsoft Copilot の App Privacy と Data safety(両方 404)。
- ChatGPT のスマホのアプリの端末の連携の公式の説明(help.openai.com が 403)。
- Gemini が Android の通知を読む公式の説明。
- Android の Advanced Protection Mode が AccessibilityService を制限するかどうか。公式のページに記載はなかった。
- au、ソフトバンクのキャリアメールと、Yahoo!メールの公式のヘルプ。
- EUR-Lex の GDPR の本文(空のページ)。カリフォルニア州の議会のサイト(403)。
