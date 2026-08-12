Authenticationは本人確認（ログイン済みユーザーなど)、Authorizationは権限確認（アクセス権限）
### RFC 7519 [[JSON Web Token(JWT)]]
	ユーザー情報や権限などの情報を、安全にやり取りするための文字列形式。以下の情報を
	```
	{  
		"user_id": 123,  
		"name": "taro",  
		"role": "admin",  
		"exp": 1710000000  
	}
	```
	などを次のような形式で送る。
	```
		header.payload.signature
	```
	|部分|役割|
	|---|---|
	|Header|署名方式などの情報|
	|Payload|ユーザーID、有効期限、権限などの情報|
	|Signature|改ざんされていないことを確認するための署名|
	- Claimsは上のJSONデータのことを指す
	- JWS
		- 署名付きJWT
	- JWE
		- 暗号かされたJWT
	- 基本JWSを使用し、Base64でデコードすれば見れるが署名があるから改ざんがバレる
	- RFC 7519, RFC8725（安全に使うための注意点）, RFC7797
-------------------------------------------------------------
### RFC 6749The [[OAuth]] 2.0 Authorization Framework
	あるアプリが、ユーザーのパスワードを直接預からずに、別サービスのデータへ限定的にアクセスするための仕組み。
	たとえば、あなたが「写真印刷アプリ」にGoogleフォトの写真を使わせたいとします。
	昔ながらのやり方だと、写真印刷アプリにGoogleアカウントのID・パスワードを渡す必要がありました。でもそれは危険です。RFC 6749でも、第三者アプリがユーザーの認証情報、典型的にはパスワードを保存しなければならない問題があるがこれを以下のようにぬける
	```
		写真印刷アプリ
		  ↓
		Googleの認可画面に移動
		  ↓
		ユーザーがGoogle側でログイン
		  ↓
		「写真へのアクセスを許可しますか？」と聞かれる
		  ↓
		許可すると、写真印刷アプリに access token が渡される
		  ↓
		写真印刷アプリはその token を使って写真APIにアクセスする
	```
	このとき、写真印刷アプリは、あなたのGoogleパスワードを知らないです。代わりにaccess tokenを使います。
	このようにauthorization layerを用意し、を導入し、clientとresource ownerの役割を分離すると説明されています。
	- JWTとの関係
		- JWTをaccess tokenとして使わなくてもよい
	|役割|意味|例|
	|---|---|---|
	|Resource Owner|リソースの持ち主|あなた|
	|Client|アクセスしたいアプリ|写真印刷アプリ、家計簿アプリ|
	|Authorization Server|トークンを発行するサーバー|Googleの認可サーバー|
	|Resource Server|データを持っているサーバー|Google Photos API|
	- access token
		- この範囲ならアクセスしてよいという許可証
	- refresh token
		- 期限が切れたときに使う。Authorization Serverに保存する
	- Authorization Code Flow
		1. ユーザーを認可サーバーにリダイレクトする
		2. ユーザーがログインして許可する
		3. 認可サーバーが authorization code をアプリに返す
		4. アプリが authorization code を token endpoint に送る
		5. access token / refresh token を受け取る
		6. access token を使ってAuthorization: Bearer <token>の形でAPIにアクセスする
	OAuthはAccess Tokenで主に認可を行います。認証に使うならOpenID ConnectのID Tokenを使います。
------------------------------------------------------
### [[HTTP]] Basic Authentication
	Webサーバーにアクセスするときに、ブラウザ標準のログイン画面でユーザー名とパスワードを送る認証方式。
	webアプリ側で作るのではなく、ブラウザからダイアログがでるやつである
	1.最初にブラウザがサーバーへアクセスする
	```
	GET /secret-page HTTP/1.1  
	Host: example.com
	```
	2.サーバーが「認証が必要です」と返す
	Basic認証が必要です。
	```
	401 Unauthorized  
	WWW-Authenticate: Basic realm="user_pages"
	```
	3.ブラウザがログインポップアップを出す。
	WWW-Authenticate: Basicをブラウザがみてポップアップをだす。
	```
	ユーザー名とパスワードを入力してください
	```
	4.ユーザー名とパスワードをBase64にして送る
		Baseはエンコードなのでバレる
	5.サーバーが検証する