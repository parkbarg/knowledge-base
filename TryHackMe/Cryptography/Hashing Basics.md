- Hash Functions
	ハッシュ関数から要約値（ハッシュ値・ダイジェスト）。ハッシュ関数は暗号化と異なり出力から入力に戻ることは不可能である。ハッシュ値本来はバイト列だが16進数となっている。ハッシュ衝突というものがある。鳩ノ巣効果である。MD5についての衝突(https://www.mscs.dal.ca/~selinger/md5collision/?utm_source=chatgpt.com)。SHA-1についての衝突(https://csrc.nist.gov/news/2017/research-results-on-sha-1-collisions?utm_source=chatgpt.com)。同時衝突は確認されていない。
- Insecure Password Storage for Authentication
	認証用パスワードは、元のパスワードを取り出せる形で保存してはいけない。平文保存、暗号化、MD5/SHA-1のような弱いハッシュは危険。安全にはsalt付きのパスワードハッシュ関数を使う必要がある。rockyou.txtのパスワードリスト。パスワードマネージャーは戻す必要があるから暗号化する必要がある。認証用パスワードは元に戻す必要なし。
- Using Hashing for Secure Password Storage
	ハッシュ値を保存する。レインボーテーブルとはハッシュ値と平文を対応付けたルックアップテーブル。CrackStationやHashes.comなどはsaltなしのレインボーテーブルに向いている。ハッシュをクラックするよりこういうのを使用した方が効率的である。bycyptとscryptはsaltを自動で使う。
	- レインボーテーブルの対策
		saltはユーザーごとのランダムでユニークな値にする。saltは秘密にする必要ない
- Recognising Password Hashes
	hashIDは自動ハッシュ認識ツールである。大体のツールはプレフィックスを持つハッシュの場合、ツールは信頼できる。文脈で判断することが大事である。例えば古いwebアプリではMD5が使われているなどである。
	- Linuxのパスワードハッシュ
			Linuxではパスワードハッシュは/etc/shadoにありrootしか読めない。各フィールドは：で分かれていている。それで各項目が表しているものをみれば簡単に分かる
	- Windowsのパスワードハッシュ
			NTLMを使用している。MD５に似ているため文脈が大事である。基本的にSAM（Security Accounts Manager）に保存される。mimikatzはWindowsの認証情報を扱う有名なツールである。LM hashやNThashが歴史的にあった。
	Hashcat Example Hashesのページをみて見比べることが大事
- Password Cracking
	パスワードハッシュは復号できないので候補パスワードを大量に試すしかない。ハッシュクラックの流れとして対象ハッシュがあり、パスワードを大量にハッシュ化して対象ハッシュと一致したら元のパスワードが分かったという流れである。saltを加えて試す。rockyou.txtをハッシュし、必要に応じてsaltを加えて、HashcatやJohn the Ripperを行う。
	- Cracking Passwords with GPUs
		同じような計算を大量並列を行うのが得意。bcryptはパスワード保存用に作られたハッシュ方式。速すぎてクラックされやすい（MD5, SHA-1, NTLM）、遅く設計されていてクラックされにくい（bcrypt, scrypt, Argon2）。
	- Cracking on VMs
		HashcatはGPUを使うことが多いのでVM場だとホストPCのGPUを使えないので可能ならホストOS上で動かした方がいい。John the RipperではCPUで動かしやすくVMでも簡単に使える。
	- Time to Crack Some Hashes
		hashcat -m <hash_type> -a <attack_mode> hashfile wordlist　Hashcatの基本構文である。
	- Questions
		- ＄２a＄はbcryptです。`$6$` なので **sha512crypt**
- Hashing for Integrity Checking
	普通のハッシュは「データが変わっていないか」を確認するために使える。HMACはそれに秘密鍵を加えて、「改ざんされていない」だけでなく「正しい相手が作った」ことも確認できる仕組みです。
	- Integrity Checking
		head Fedora-Workstation-40-1.14-x86_64-CHECKSUM。ハッシュ値と比べるコマンド。公式ハッシュ値が改ざんされている可能性があるので署名の確認が大事である。重複ファイルの検出にも使える。
	- HMAC（Keyed-Hash Message Authentication Code）
		秘密鍵付きハッシュ認証コード。秘密鍵は共有しているとする。メッセージを送る->HMACを計算する->hmacを送る->HMACを秘密鍵Kで計算する。
- Conclusion
	- Hashing
		入力データから固定長のハッシュ値を作る処理。元に戻せない
	- Encoding
		データの表現形式を変換すること。ASCII、UTF-8、Base64。エンコードは暗号化されているは言えない。元に戻せる
	- Encryption
		データの機密性を守るために、鍵を使って読めない形に変換すること。元に戻せる
- Action point
	-a 0ばかり使わない。