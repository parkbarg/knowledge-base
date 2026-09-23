## vue.jsとは
- ユーザーインターフェースを簡単に作るためのjavascriptフレームワーク
- ユーザーインターフェース：見た目・クリック
- javascript：ブラウザ上で実行できる
- シングルページアプリケーション(サーバー側で何度もUIを返すのではなく、ブラウザ上でいろいろな画面を構築する)
- 
## vueはこうして始める
- 単一ファイルコンポーネント
- Vite
  - vue -> js変換処理を自動で行ってくれる
  - jsの実行環境としてnodejsが必要
- npm create vue@latest
  - 他に設定ファイルが必要だがやってくれる
  - create-vueをインストールしている
- npm install
  - packagejsonの依存関係がインストールされる
  - distは製品でviteが最適化処理を行ってくれる
  - .vscode/packagejsonはインストールするといい拡張機能
  - 右クリックやctlSで特定のフォーマットにできる
  - editorconfigは拡張機能がないと動かない。
  - eslint.config.jsでrecommendで厳しくできる
- create app
  - インターフェースを作って表示はしていない
  - 引数にコンポーネント(vueファイル)を渡せる
- import App from './App.vue'
  - デフォルトインポート文で持ってくる
- mount
  - css セレクターで指定する
- vueファイルとは
  - script, template, style
- script内をtemplateで表示したいとき
  - scriptの中はトップレベルじゃないと参照不可
  - {{}}を使う
  - 変数は${{}}
- クリックされた時の処理
  - <butten @click>
- リアクティブティ
  - refオブジェクトで実現
    - jsonみたいなデータ構造となっている
    - 値はオブジェクトを参照する必要がある
    - テンプレートではrefオブジェクトかどうかを自動で判断
      - 入れ子だと参照できない事がある
      - 処理は入れない
  - reactiveオブジェクト
    - 元々オブジェクトのものをリアクティブにする

## vue.jsの基礎
- ディレクティブ
  - テンプレートから値を参照
  - v-html
    - 文字列
    - ユーザーからの情報を入れない(XSS)
  - v-bind
    - 属性値はv-bindでscriptから参照する
    - :だけで省略できる
    - 複数指定可能
  - v-on
    - @で省略可能
    - イベントとハンドラー
      - インラインハンドラー、メソッドハンドラーなど
    - [Dom events](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Events)
    - イベント情報の詳細なものを見れる
      - インライン:$, メソッド:関数内引数
    - 引数を入れたいときは関数でハンドラーを指定する
    - イベント修飾子（stop, eventetc）
    - キー修飾子
    - []を使って引数にscriptのデータを指定する
  - v-model
    - userが入れた値を受け取ることができる
- computed ref オブジェクト
  - 複雑な式をまとめたい
  - リアクティブエフェクト
    - 値の変化を監視して変更を実行する
    - 中でリアクティブオブジェクトを指定している場合でも追うことが可能
    - templateでもある。再レンダリング
      - computed（推奨）使わなくてもいい
      - 一応関数呼び出しもできる
  - 読み取り専用
  - 副作用は気を付ける（関数の外のデータを変更するようなものはダメ）
  - 最適化
    - 必要ないときは関数を実行しない
    - 変更を検知したら関数を再実行する
- watchEffect
  - 引数に関数を指定する
  - 非同期処理や副作用も入れられる
  - 監視させるためにはデータを読み取らせる必要がある
    - 同期の中で行う
- watch
  - 引数に監視対象と関数を入れる
    - refやリアクティブオブジェクトを入れる
      - リアクティブオブジェクトは更新すると実行されるので注意
    - 第一引数に関数を入れるとwatcheffectと同じ
  - 関数にnewValue, oldValueをおける
  - リアクティブオブジェクトの値を監視したい場合は関数で書く
- v-html
  - class
    - 配列やオブジェクト、辞書の指定が可能である
  - style
    - 配列やオブジェクト、辞書の指定が可能である
    - ケバブケースをキャメルケースにできる
      - vuejsはキャメルケース

## 条件付きレンダリングとリストレンダリング
- v-if
  - v-if, v-else-if, v-elseは一緒に書かないとだめ
  - 複数の出したいときは囲む(div or template)
  - pタグが消える
- v-show
  - pタグが残る
    - 高頻度な時はこちらを使った方が効率が良い。
- v-for
  - リストレンダリングしたいとき
  - key属性
    - ずれが生じないようにする
    - vueは効率的なため表示が変になる
  - インデックスの取得
    - indexを指定する
  - 分割代入
    - {}で指定する
  - 新しいタグを作りたくないときはtemplateを使用する
  - v-ifとv-forを同時に使用したいときはずらす必要がある
  - オブジェクトを表示する
    - num in numsのような形

## コンポーネントはこう使う
- コンポーネントツリー
- 繋げる方法
  - 親で子をimportしてタグ指定する
  - 複数使用可能
- コンポーネントの命名規則
  - パスカルケース or ケバブケース
  - App以外は二単語以上
- グローバル登録
  - mainjsの中のapp.componentで指定する
  - vueファイルにないので保守性が低い
    - あまり使うべきではない
- componentsフォルダでまとめることが多い
- @がソースコードのディレクトリ
- コンポーネント内の属性の継承
  - idは親が優先
  - class, styleは合算される
  - ディレクティブによって違いがある
    - 物によって違う
    - タグが複数の場合
      - $attrsで継承可能
- styleタグの継承
  - データは使えないが他のコンポーネントから使える
  - コンポーネントだけで使えるstyle
    - scoped
    - 一番外側はついてしまう
  - global
    - assetsにcssを書きmainjsにインポートする場合もある
- コンポーネントごとに識別子をふっている
- vue devtools便利だよ

## 親子間のコンポーネントでデータを受け渡す方法
- 親からの子へ渡す場合(Props)
  -  definePropsを使用する
  -  オブジェクトにあるのでアクセス可能である
  -  readonly
  -  属性の継承は行われない
  -  分割代入が可能は独自でリアクティブ性を維持してくれる
     -  本当は変更を検知できないがvuejsがいい感じにやってくれる(props.foo)
  -  オブジェクトで値のバリデーションができる
     -  defaultがオブジェクトか配列のときは関数でしていする　
  -  命名規則
     -  子；キャメルケース
     -  親：ケバブケース
- 子からの親へ渡す場合
  - イベントで$emitの指定
    - データを受けるときはイベントハンドラーでもメソッドハンドラーでも可能
    - defineEmitsを定義する
    - 命名規則
      - 子：キャメルケース
      - 親：ケバブケース

## vuejsの内部構造はこうなっている
- DOM(Document Object Model)
  - ブラウザがHTMLをレンダリングするもの
  - ツリー上のデータ構造
  - jsがDOMを操作している
  - Cとかで書かれている
- vuejsが作る仮想的なDOM
  - jsのオブジェクトで作られる
  - 初期のレンダリングのみ行われる(mount)
    - 次回以降は差分だけDOMに反映する(patch)
  - 仮想DOMはDOMより軽い
- onMountedとonUnmounted, onUpdated, onbefore系
  - コンポーネントのライフサイクル、ライフサイクルフック
  - 非同期処理はできない
- DOMの更新は非同期的に行われる
  - nextTick
    - DOM更新後の処理(Mount系でもできる)
    - awaitでも記述可能
- DOM自体にアクセスする
  - useTemplateReff
## コンポーネントの高度な機能はこう書く
- slot(親から子へ)
  - タグごと渡すことができる
  - 柔軟なコンポーネントの作成
  - データの受け渡しはできない
  - フォールバックコンテンツ
    - slotでの指定
  - v-slot(#)
    - name属性となる
    - ないのはdefaultとなる
  - スロットプロップス
    - 子から親へ
- 動的コンポーネント
  - 動的にコンポーネントを変えたいとき
  - component isで指定する
- shallowRef
  - オブジェクトの中はリアクティブにしない
  - パフォーマンスがいい
- keepalive
  - マウントアンマウントをしてもデータが残るようにする
  - include, exclude, max
  - onActivated, onDeactivated
    - コンポーネントの削除の検知など
- teleport
  - 挿入できる
  - 外側に置くのがいいとされている
  - モーダルとかに使えるらしい
- 遅延読みこみ
  - defineAsyncComponent
  - 使用するときに読み込む
  - 遅延コンポーネント（非同期コンポーネント）

## vuejsで簡単にフォームを作れる(v-model)
- 複数行(textarea)
- チェックボックス(checkbox)
  - 真偽値が入る
  - true-valueなど
  - value + 配列
    - 複数候補
- ラジオボタン
  - valueを使用する
- selectタグ
  - タイトルvalueとdisable
  - 配列で複数
  - multiple
- 修飾子
  - lazy
  - trim
  - number
- defineModel
  - 子のデータを親へ
  - フォームのときだけ
  - 修飾子を引き継ぐ
    - get,setで処理を入れる
## composableを使って処理の部分を再利用する方法
- composition API
- スクリプト内を再利用したい
  - jsに書いてexportを書く
- 非同期にできない
- 組み合わせることを可能
- ベストプラクティス
  - useから始める
  - 普通の値にレフオブジェクトが入っても使えるようにする
    - tovalue
- VueUse
  - OSS的なやつ
  - Darkモード

## Vue Router
- createRouter
- app.use
  - プロジェクト全体に影響を及ぼすものを指定する
  - 引数の部分をプラグインという
- routerフォルダで分割
- 設定
  - routes
  - history
    - createWebHistory
      - ブラウザのヒストリーAPI
  - views
    - routerで使うコンポーネント
  - RouterViewの指定
    - toの指定もできる  
  - URLの指定とURLごとに毎回リロードを防ぐ
    - RouterLink
- :to
  - オブジェクトを渡したいとき
- プログラムからURLを移動したい
  - useRouter
  - push
    - 履歴が残る
  - replace
    - 履歴が残らない
  - $routerでもできる
- routeに名前を付ける
  - nameを設定する
  - オブジェクトの設定
- パスがどんな値でも同じコンポーネントを表示する方法
  - pathに:を入れてできる(パラメータ)
  - paramsにしてそれぞれ指定する
  - 条件指定が可能
    - ルールや正規表現が可能
    - +, ? , *
- routeオブジェクトでURLのパラメータの値を取得する方法
  - $route
  - useRoute
  - パラメータを変更してもマウントされるわけじゃない
- 設定していないURLにアクセスした場合
  - (.*)*となる
  - 詳細度の高いものからアクセスされる
- リダイレクトとエイリアス
  - redirectを設定する
  - aliasを設定する
- 設定の情報をpropsとして取得する方法
  - props
- ネストされたRouterView
  - childrenを設定する
- 複数のRouterを同じ階層に入れる
  - components
  - name属性の指定
- Transitionコンポーネント
  - アニメーション
- スクロールのふるまい
  - scrollBehaviorを設定する
  - 引数にいろいろ指定できるよ

## 世界中に自分のアプリを公開する方法
- npm run build
  - distの作成
- 静的ホスティングサービス
  - vite
    - cloud flare pages
## Question
- なぜこれがうまくいかない
  ```
  <script setup>
  const props = defineProps(['foo'])
  const chore = props.foo
  </script>
  <template>
    <p>count: {{ foo }}</p>
    <p>count: {{ chore }}</p>
  </template>

  ```
  その時点の値を参照しているだけ。分割代入すれば戻せる、definepropsの特殊な例である。computed、toRefなどでもできる。
- リアクティブな値であることとそれを自動で再実行するかは違う
  ```
  <script setup>
  import { ref } from 'vue'
  const count1 = ref(0)
  console.log(count1)
  </script>
  <template>
    <p>{{ count1 }}</p>
    <button @click="count1++">count1: +1</button>
  </template>

  ```
  自動で再実行するようにする
- ref は「リアクティブな箱そのもの」を渡せるが、props の foo は「箱の中の値」なので getter () => foo が必要。
  ```
  <script setup>
  import { watch } from 'vue'

  const { foo } = defineProps(['foo'])
  watch(
    () => foo,
    () => {
      console.log('watch')
    },
  )
  console.log(foo)
  </script>
  <template>
    <p>count: {{ foo }}</p>
  </template>

  ```
