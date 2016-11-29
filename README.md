# 【Monaca × mBaaS】<br>Webコンテンツをスマホアプリ化をしよう！

![Webコンテンツのスマホアプリ化イメージ](/readme-img/Webコンテンツのスマホアプリ化イメージ.png)

## はじめに
### 概要
Monacaとニフティクラウド mobile backendを使うことで、**既存のWebコンテンツも簡単にスマホアプリ化することが可能** です。ここではその手順を解説します。

### 今回体験する内容
#### ブログコンテンツのスマホアプリ化
既存のスマホ対応済みブログをスマホアプリ化します。
* ブログのRSSからアプリの記事リストを構築します
* 記事本体はWebViewでブログ本体へ遷移させます
* ブログのお気に入り登録機能を追加します
 * お気に入り情報をクラウドに保存します
* アプリ側は「Monaca」を、バックエンド側は「mBaaS」を使用して簡単に実装します

![Webコンテンツのスマホアプリ化イメージ](/readme-img/Webコンテンツのスマホアプリ化イメージ.png)

### Monacaって何？
* __もなか 【[Monaca](https://ja.monaca.io/)】__ HTML5/JavaScript/CSS3でスマホアプリが開発できる開発環境。開発スタイル／コーディング環境は選択可能。

![Monacaとは？](/readme-img/Monacaとは.png)

### ニフティクラウド mobile backend って何？
* __にふてぃくらうど-もばいる-ばっくえんど 【[ニフティクラウド mobile backend](http://mb.cloud.nifty.com/about.htm)】__ スマートフォンアプリに必要なバックエンド機能が開発不要で利用できるクラウドサービス。 クラウド上に用意された機能をAPIで呼び出すだけで利用できます。また、APIを簡単に使うためのSDKを用意しています（ iOS / Android / Monaca / Unity ）。mobile Backend as a Service の頭文字を取って、通称 **mBaaS** 呼ばれます。

![mBaaSとは？](/readme-img/mBaaSとは.png)

### Monaca と mBaaS でサーバー連携アプリは簡単に実現可能に
この２つを組み合わせると、高度なアプリも簡単スピーディーに開発できます
![Monaca×mBaaS](/readme-img/Monaca×mBaaS.png)

#### アプリ側：Monaca のすごいところ
* 無料で使える！
* iOS / Android 同時に開発可能！
* いつでもどこでも、ブラウザで開発OK！
* **mBaaSのSDK導入** がクリックだけで簡単に！

#### サーバー側：mBaaS のすごいところ
* 無料で使える！**バックエンドの開発・運用は一切不要**！
* データの保存はたった **３行** で実装可能！
* **プッシュ通知** も簡単実装！
* **コントロールパネル** からクラウドの状況をパッと確認できる！

## 準備
### 事前準備
下記登録を完了し、アカウントを作成しておいてください。
* [Monaca](https://ja.monaca.io/register/start.html)の利用登録（無料）
* [ニフティクラウド mobile backend (mBaaS)](http://mb.cloud.nifty.com/signup.htm)の利用登録（無料）

### 動作環境準備
* PC
 * Chrome 最新版
* 端末 ( iPhone / Android )
 * [Monacaデバッガー](https://ja.monaca.io/debugger.html) 最新版

## ハンズオン
### 手順
1. Monacaの準備
1. 動作確認① MonacaでRSSリーダーを体験
1. mBaaSの準備
1. お気に入り機能をオンライン化する
1. 動作確認② クラウド連携したRSSリーダーを体験

### 1. Monaca準備
* Monacaにログインをします

![Monaca準備1](/readme-img/Monaca準備1.png)
https://ja.monaca.io/

* プロジェクトをインポートします
 * 今回は「アプリとサーバーの連携以外の処理」に関しては実装したプロジェクトを用意しました。アプリとサーバー間の連携部分のコーディングを体験していただけます。
* 「Import Project」をクリックすると、「プロジェクトのインポート」画面が表示されます
* 「プロジェクト名」を入力します　例）__Webコンテンツのスマホアプリ化__
* 「インポート方法」では、「URLを指定してインポート」を選択し、次のURLを入力します
 * `https://github.com/natsumo/MonacaRssReaderApp/archive/master.zip`

![Monaca準備2](/readme-img/Monaca準備2.png)

* プロジェクトが作成さてたら、「開く」をクリックします
* プロジェクトが開かれます

![Monaca準備3](/readme-img/Monaca準備3.png)

* これでMonacaの準備は完了です

### 2. 動作確認① MonacaでRSSリーダーを体験
![動作確認①-1](/readme-img/動作確認①-1.png)

* 何も変更せずにMonacaデバッガーで動かしてみましょう
* mBaaSのブログ（mBaaS活用術）が表示されます

![動作確認①-2](/readme-img/動作確認①-2.png)

* 星のマークをタップするとお気に入りの ON/OFF ができます
 * 処理は`www/js/favorite-offline.js`ファイルに記述されています
* お気に入りの情報はスマホのローカルストレージに保存されています
 * したがって、「お気に入り」情報は、自分にしか見れません。また、機種変更したら見れなくなってしまいます。

![動作確認①-3](/readme-img/動作確認①-3.png)

#### ローカルストレージからクラウドへ！
mBaaSを導入しましょう！
* 自分のお気に入り情報をサーバーに上げて、共有する
* 他の人がどれくらいお気に入り登録しているかどうか

![完成イメージ1](/readme-img/完成イメージ1.png)

### 3. mBaaS準備
* mBaaS にログインします

![mBaaS準備1](/readme-img/mBaaS準備1.png)
http://mb.cloud.nifty.com/

* 新しいアプリを作成します
* アプリ名は「`RSSReader`」と入力し、「新規作成」をクリックします

![mBaaS準備2-1](/readme-img/mBaaS準備2-1.png)

* mBaaSを既に使用したことがある場合は、画面上方のメニューバーにある「+新しいアプリ」をクリックすると同じ画面が表示されます

![mBaaS準備2-2](/readme-img/mBaaS準備2-2.png)

* アプリが作成されるとAPIキー（２種類）が発行されます
 * APIキーは後で使用します。
* ここでは使用しないので、「OK」で閉じます

![mBaaS準備3](/readme-img/mBaaS準備3.png)

* ダッシュボードが表示されます

![mBaaS準備4](/readme-img/mBaaS準備4.png)

* これでmBaaSの準備は完了です

### 4. お気に入り機能をオンライン化する
完成イメージ
![完成イメージ2](/readme-img/完成イメージ2.png)

#### 作業手順
1. SDKの導入
2. SDKの初期化
3. 読み込むJavaScriptファイルの変更
 * 今回はコーディング実装済みのものを用意しています
4. コード解説

#### 1. SDKの導入
* Monacaを開きます
* 上部メニューバーから「設定」＞「JS/CSSコンポーネントの追加と削除...」をクリックします

![SDK導入1](/readme-img/SDK導入1.png)

* 「インストールしたコンポーネント」の右のテキストフィールドに「`ncmb`」と入力し、「検索」をクリックします

![SDK導入2](/readme-img/SDK導入2.png)

* 「ncmbインストールされていません。」とひょうじされるので、　「追加」をクリックします
* SDKのバージョンはそのまま（最新版を指定）で、「インストールの開始」をクリックします
* 「ローダーの設定」で「`components/ncmb/ncmb.min.js`」のチェックボックスにチェックを入れて「OK」をクリックします

![SDK導入3](/readme-img/SDK導入3.png)

* 下記のように表示されればOKです！

![SDK導入4](/readme-img/SDK導入4.png)

#### 2. SDKの初期化
* `www/index.html`を開きます

![Monaca_index](/readme-img/Monaca_index.png)

* 「APIキーの設定」にmBaaSでアプリ作成時に発行されたAPIキーを設定します

![code_API](/readme-img/code_API.png)

* mBaaS のダッシュボードから、APIキー（アプリケーションキーとクライアントキー）をコピーして、それぞれ`YOUR_NCMB_APPLICATION_KEY`と`YOUR_NCMB_CLIENT_KEY`に貼り付けます

![SDKの初期化](/readme-img/SDKの初期化.png)

* このとき、ダブルクォーテーション「`"`」は消さないように注意しましょう

#### 3. 読み込むJavaScriptファイルの変更
* 同じく`www/index.html`を編集します

現在の状態は、ローカルストレージに保存する処理を実装した「`www/js/favorite-offline.js`」を読み込んでいます。これをmBaaSに保存する処理を実装した「`www/js/favorite-online.js`」に読み込み先を変更する必要があります。

* 12行目のコードを下図のように編集します

![code_offline_to_online](/readme-img/code_offline_to_online.png)

* 必ず保存をしましょう
 * メニューバーの「保存」をクリックします
 * Windowsの場合は、「Ctrl + S」でも保存できます
 * Macの場合は、「Command + S」でも保存できます

今回のセミナーでは実装が完了したものを使用しますので、作業は以上です。コードについては動作確認後に見ていきます。

#### 4. コード解説
実装内容を確認していきます

* Monacaを開いて、`www/js/favorite-online.js`ファイルを開きます

![Monaca_online](/readme-img/Monaca_online.png)

##### (1) SDKの初期化
mBaaSのSDKを使う場合は必ず行う処理です
![code_1](/readme-img/code_1.png)

##### (2) 保存先クラスの定義
☆をタップするとお気に入り登録ができます。そのデータの保存先クラス`favorite`をここで定義しています
![code_2](/readme-img/code_2.png)

##### (3) 保存するオブジェクトの生成
![code_3](/readme-img/code_3.png)

##### (4) お気に入り登録（保存）
(3)で生成したオブジェクトに`.set(key, value)`で値を設定します。ここでは誰が(who)、どの記事を(where)を保存したかを記録するため、自分（端末）の`uuid`（ユニークユーザーID）と登録したい記事の`URL`を設定します。ドットチェーンで書くことができます。`.save()`で保存します。処理が成功した場合`.then`、失敗した場合`.catch`の処理が実行されます。
![code_4](/readme-img/code_4.png)

##### (5) お気に入り登録解除（検索/削除）
☆をもう一度タップするとお気に入り登録を解除することができます。該当のデータを検索し、削除を行います。`equalTo(key, value)`で自分（端末）の`uuid`（ユニークユーザーID）と削除したい記事の`URL`に一致するデータを、`fetch()`で検索します。
検索に成功した場合(then)に、`delete()`で削除を行っています。
![code_5](/readme-img/code_5.png)

##### (6) お気に入り登録人数表示（検索）
各記事の登録人数を数えるには、`equalTo(key, value)`で`URL`のみを指定し、`.count()`で数えて、`.fetchAll()`で全件検索を行います。
![code_6](/readme-img/code_6.png)

##### (7) ☆に色をつける（検索）
自分自身がお気に入り登録した記事には☆に色を付けます。
自分（端末）の`uuid`（ユニークユーザーID）と記事の`URL`のセットに合致するデータを`count()`で数えて、`fetchAll()`で全件検索します。その値が`0`より大きい場合に☆に色を付けています。

![code_7](/readme-img/code_7.png)

### 5. 動作確認②
* 再びMonacaデバッガーを起動し、MonacaとmBaaSの連携を確認しましょう

![動作確認②-1](/readme-img/動作確認②-1.png)

* ☆をタップしたら、mBaaSのダッシュボードを確認しましょう

#### mBaaSのダッシュボードを確認
* 下図のように情報が保存されます
 * １つのお気に入り登録に対して、１つのデータが保存されます。したがって、☆の数が増えると、mBaaSに保存されたデータも増えます。

![動作確認②-2](/readme-img/動作確認②-2.png)

* 個人（端末）を表す`uuid`と記事の`URL`が登録されていることが確認できます

#### mBaaSのダッシュボードからデータを編集
現在は、ユーザーが１人しかいないので、画面の数字は「1」までしか増えません。ダッシュボードからデータを編集して、「ダミーユーザー」のデータを作ってみましょう。

* 任意のデータの「`uuid`」を１つ選択し、編集します
 * 適当な文字列に置き換えてください。

![dummy_uuid](/readme-img/dummy_uuid.png)

* デバッガーを見てみましょう
 * 違うユーザーがお気に入り登録した状態なので、☆の色が消えます。

![dummy_debugger](/readme-img/dummy_debugger.png)

## まとめ
* 既存Webコンテンツのスマホアプリ化を体験いしました
* サーバー連携したアプリは Monaca × mBaaS で簡単に実現可能であることがわかった
* mBaaS の「データストア」機能について知ることができた

## おわりに
いかがでしたでしょうか？こんなに使いやすくて便利なmBaaSをもっと活用してみたい方へ、mBaaSの各機能をすぐに試すことができるサンプルアプリを多数ご用意しています。Monacaにサンプルプロジェクトをインポートして、簡単な操作をするだけで直ぐにお試しいただけます！ぜひご活用ください。

* [mobile backend を体験しよう！](https://github.com/NIFTYCloud-mbaas/monaca_data_registration)
 * 使用機能 / データストア
* [アプリにログイン機能をつけよう！](https://github.com/NIFTYCloud-mbaas/monaca_login_template)
 * 使用機能 / 会員管理
* [アプリにプッシュ通知を組み込もう！](https://github.com/NIFTYCloud-mbaas/MonacaPushApp)
 * 使用機能 / プッシュ通知
* [地図アプリを作ろう！](https://github.com/NIFTYCloud-mbaas/MonacaMapApp)
 * 使用機能 / データストア,位置情報検索
* [and more...](http://mb.cloud.nifty.com/doc/current/tutorial/tutorial_monaca.html)
