- Basic Terms
	PやNPに関する説明がよくわからない。
	- Where John Comes in
		John the Ripper、略してJohnは、さまざまなハッシュタイプに対して高速なブルートフォース攻撃を行うツール。Jumbo Johnは拡張版である。
- Setting Up Your System
- Cracking Basic Hashes
	Johnの基本構文は john options file path
	まずは wordlist を指定して自動判別で試せる.
	==john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt==  
	ただし自動判別は間違うことがある。その場合は hash-identifier などでハッシュ形式を推測する。形式が分かったら --format= を使って明示的に指定する。MD5のような標準ハッシュでは raw-md5 のように raw- を付ける場合がある。対応formatは john --list=formats で確認できる。--showで結果を確認できる。
- Cracking windows Authentication Hashes
	windowsで使われるハッシュはNTHash/NTLMである。windowsではローカルユーザー情報はSAMに保存される。ハッシュ化されたユーザーパスワードなどが格納されている。Windowsのハッシュを入手する方法としてSAMデータベースをdumpする、MImikatzのようなツールを使う。Active DirectoryのNTDS.ditから取得する。pass the hashとはNTLMハッシュそのもので認証できる場合がある攻撃である。
- Cracking /etc/shadow Hashes
	Linuxのパスワードハッシュは/etc/shadowにある。これはrootしか読めない。/etc/shadowだけでなく/etc/passwdも必要な理由はJohnがユーザー情報とパスワードハッシュを好むから。
	- Unshadow
		==unshadow path to passwd path to shadow==
		統合する。
- Single Crack Mode
	Single Crack mode は、ユーザー名やユーザー情報から「ありそうなパスワード候補」をJohnが自動生成して試すモードです。
	- Word Mangling
		単語をいじる、変形する。人はベースがあって人部分だけ変えがちJ0kerなど。
	- Mangling rules
		むやみに変形しているのではくルールに従って変形いている。
	- GECOS
		これはプレフィックスの5番目のフィールドでフルネーム、電話番号、部屋番号などが入ることがある。
	- --singleとして使う
	- ユーザー名をファイルに追加する。
- Custom Rules
	自分でパスワード候補の変形ルールを作る方法。
	- How to create Custom Rules
		/opt/john/john.confなどの設定ファイルに書き込む。「List.Rules:名前」で登録して--ruleを使用する。
	- mangling rule syntax
		なれるまでは既存のルールを使用するべき、john.confの既存のルールを見ればいい。
	- 現実のルールなどに沿ったものを作成できる
- Cracking Password Protected Zip Files
	ZIPファイルそのものをJohnに直接渡すのではなく、まず zip2john でJohnが読めるハッシュ形式に変換し、そのハッシュをJohnでクラックする。
	- 基本構文
		==zip2john options zip file > output file==
	- 
- Cracking Password-Protected RAR Archives
	RARファイルもzipのクラッキングと同様に行う。
	- 基本構文
		==rar2john rar file > output file==
- Cracking SSH keys with John
	秘密鍵のパスフレーズをクラッキングする。sshファイルもzipのクラッキングと同様に行う。
	- 基本構文
		ssh2john id_rsa private key file > output file
		python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt(find / -name "ssh2john.py" 2>/dev/null)
	- パスフレーズが分かった後
		chmod 600 id_rsa
		ssh -i id_rsa user@host
- Further Reading
	- https://www.openwall.com/john/