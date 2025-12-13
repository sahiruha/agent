🛡️ Vibe Coding Manifesto: The Integrated Security Edition
～ 不安（Vulnerability）を排除し、最高のフロー（Flow）でコードを書くための鉄則 ～


Based on: IPA 安全なウェブサイトの作り方 改訂第7版 

0. The Golden Vibe (基本哲学)

根本的解決が至高: 後からパッチを当てるな。最初から「割れない」設計をするのが真のVibe 。


保険はあくまで保険: WAFやエラー非表示はセーフティネット。コード自体が強くあるべき 。

Good Vibes Only: セキュリティは制限ではない。クリエイティブな開発を持続させるためのガードレールだ。

1. Clean Input, Clean Output (入出力のバイブス)
悪いエネルギー（不正入力）を受け入れず、綺麗な表現（安全な出力）だけを世に出す。

🔹 SQL: "Don't Mix, Just Bind."
文字列連結はダサい。プレースホルダで美しく渡せ。


Rule: SQL文の組み立ては全て静的プレースホルダで実装する 。


Fallback: どうしても文字列連結が必要なら、言語標準のAPIで完璧にエスケープする 。

🔹 XSS: "Filter the Noise."
生のHTMLを信じるな。全てエスケープして純粋なテキストとして届ける。


Output: ウェブページに出力する全ての要素に対してエスケープ処理を施す 。


URL: http:// https:// 以外（特に javascript:）はノイズとしてカットする 。


Charset: レスポンスヘッダで Content-Type と文字コード（charset）を必ず宣言する 。

🔹 Command & Header: "Keep it Pure."
余計な命令や改行を混ぜさせない。


OS Command: シェル経由はバッドバイブス。言語標準のAPIを使うか、引数をホワイトリストで縛る 。



HTTP/Email Header: ヘッダ出力は専用APIを使う。自前でやるなら**改行コード（CRLF）**を徹底的に削除し、ヘッダ分割やメールの踏み台化を防ぐ 。


2. Identity & Access (信頼と境界線)
「誰であるか」と「何をしていいか」。この境界線を明確にするのが大人の作法。

🔹 Authentication: "V.I.P. Access Only."
鍵は厳重に、入り口は一つに。


Password: 平文保存は論外。ソルト付きハッシュで保存する 。


Login Feedback: 「パスワードが違います」ではなく「IDまたはパスワードが違います」と塩対応する（情報を与えない） 。


Session ID: 推測不可能な乱数を使い、URLには乗せずCookie（Secure/HttpOnly）に入れる 。



Regenerate: ログイン成功の瞬間に、新しいIDを発行して気分（セッション）を一新する 。

🔹 Authorization: "Mind Your Own Business."
IDが合っているだけでは不十分。「それ」を見ていい権利があるか？


Access Control: ログイン機能を作るだけでは不十分。必ず認可制御を実装する 。


Check Ownership: URLパラメータのIDを書き換えて他人のデータを見ようとする奴がいる。「ログイン中のユーザID == データの持ち主」かを常にチェックせよ 。

🔹 CSRF: "Intentional Moves."
「なんとなく」クリックさせない。その操作に「意志」があるか確認する。


Token: 重要な処理（POST）には秘密情報（トークン）を埋め込み、実行時に照合する 。


Verify: 処理実行直前にパスワード再入力やReferer確認を行う 。


3. Navigation & Boundaries (動線と結界)
ユーザーを迷わせず、自分の敷地内だけで遊ばせる。

🔹 Redirects: "Don't Be a Gateway to Hell."
あなたのサイトを、悪意あるサイトへの踏み台（オープンリダイレクト）にさせるな。


Allow List: リダイレクト先のURLパラメータには、自サイトのドメインのみを許可する 。

🔹 Path & Files: "Stay in Your Lane."
あちこち覗かせない。指定された場所だけで遊ぶ。


Directory: 外部パラメータでファイルパスを直接指定させない 。


Basename: ファイル名を使うなら basename() で余計な飾り（ディレクトリパス）を削ぎ落とす 。

🔹 Clickjacking: "No Overlays."
透明なシートを被せてクリックを盗むような真似はさせない。


Header: HTTPレスポンスヘッダに X-Frame-Options (DENY または SAMEORIGIN) を出力する 。

4. Infrastructure Zen (インフラの禅)
コードの外側、土台となる部分も整える。

🔹 Network & Server: "Encryption is Standard."
内緒話は暗号化する。


HTTPS: 全ページHTTPS化し、HSTSヘッダで「鍵付き」を強制する 。



Files: 公開ディレクトリに非公開ファイル（ログや設定ファイル）を置かない 。

🔹 Environment: "Let the Machine Handle It."
人間がメモリ管理をする時代は終わった。


Safe Language: C/C++のような直接メモリ操作する言語より、PHP/Java/Perlのようなメモリ管理された言語を選ぶ 。


WAF: アプリの改修が間に合わない時のために、WAFをセーフティネットとして導入する 。

5. The Vibe Check List (コミット前確認)
最後に、コードのバイブスを確認するチェックリスト。

[ ] SQLはプレースホルダでバインドされているか？ (No String Concatenation) 

[ ] 画面出力は全てエスケープされているか？ (No Raw HTML) 

[ ] 「ログイン中のユーザ」が「自分のデータ」を触っているかチェックしたか？ (Authorization) 

[ ] セッションIDは再発行（Regenerate）しているか？ (Session Safety) 

[ ] 重要な処理にトークンはあるか？ (Anti-CSRF) 

[ ] リダイレクト先は自サイト内に限定されているか？ (No Open Redirect) 

[ ] ヘッダやメール出力時に改行コードを排除しているか？ (No Header Injection) 

[ ] 重要なファイルが公開ディレクトリに漏れていないか？ (File Security)
