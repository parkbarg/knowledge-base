- Hydra Introduction
	- オンラインのログインに対して、パスワードを総当たりで試すツール
	- ありがちなパスワードを使用する
	- いろいろなプロトコルに対応
	- パスワード認証は、弱いパスワードを使うと機械的に突破される可能性がある
- Using Hydra
	- プロトコルやformによって型が変わる
	- ssh
		```
		hydra -l <username> -P <password_list> MACHINE_IP -t 4 ssh
		```
	- web form
		```
		hydra -l <username> -P <password_list> MACHINE_IP http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V
		```
	- 作成するのに情報が必要
		- ブラウザのDeveloper ToolsのNetworkタブ
		- Burp SuiteのProxy HTTP history
	- Mini CTF
		- Burp Suiteを試す