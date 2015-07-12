---
layout: post
title: Monacaを使ったチーム開発環境を構築する
---

## ゴール
Atom + Git + Monaca LocalKit + Monacaデバッガーで開発できる状態を整える

## Atomを準備
### Atomを利用するメリット
  * 軽い
  * ブラウザベースなのでHTML、JS、CSSの開発に最適
  * HTML＋CSSのライブプレビューができるのでMonacaでの開発と相性がいい
  * プラグインを入れなくても高機能

### 手順
1. [Atomエディタ](https://atom.io/)のインストール
2. プラグインパッケージの追加
 * Atom > Preferences を選択
 * SettingsのInstallを選択して以下のパッケージをインストール
    1. [file-icons](https://atom.io/packages/file-icons)
      * ファイルの横にファイルアイコンをつけてくれる
    2. [Term2](https://atom.io/packages/term2)
      * ターミナルをatomエディタ内で開いてくれる。gitを使うときに便利だが、日本語が入力できないことが難点。途中で使わなくなるかも
    3. [Script](https://atom.io/packages/script)
      * atom上でScriptを実行してくれる
    4. [highlight Tips](https://github.com/raccy/show-ideographic-space)
      * 全角スペースを◽︎で表示してくれる
    5. [project-manager](https://atom.io/packages/project-manager)
      * 開いているプロジェクトを保存して次回起動時に呼び出したりできる
    6. [Japanese Wrap](https://atom.io/packages/japanese-wrap)
      * ウィンドウのサイズによって日本語の折り返しなどをよしなにしてくれる
3. ライブプレビュー機能を強化する
 * atomではデフォルトでHTMLのライブプレビュー機能が利用できる(control + Shift + m)が、デフォルトだとHTML上で読み込んでいるCSSは読み込んでくれない
  * 以下のプラグインをインストールで解決
  * [atom-html-preview](https://atom.io/packages/atom-html-preview)


## MonacaデバッガーとMonaca LocalKitを準備
### 手順
1. [Monaca LocalKit](https://ja.monaca.io/localkit.html)をインストール
 * OSのバージョンによって開発者が不明となり開けないので
 環境設定＞セキュリティとプライバシー＞一般からダウンロードしたアプリケーションの実行を許可してあげる
 (体験版で30日しかフル機能を利用できないらしいが問題なさそう)
2. リモートIDEからプロジェクトをインポート
 *  Monaca LocalKitを開くとプロジェクト一覧には何も表示されていない状態なので、
   ``+　＞　インポート　＞　クラウドIDEからインポート``を選択しサンプルプロジェクトをインポートする
 * プロジェクトを選択し、作業ディレクトリを指定して「インポート」[^1]
3. 実機（Monaca デバッガー）とペアリングをする
 * iPnoneをPCと同じWifiに接続する
 * Monaca デバッガーを起動する
 * 「新しいコンピーターが見つかりました」のアラートビューが出るのでペアリングを選択
 * ペアリング完了
4. ファイル編集
  * インポートしたローカルのプロジェクトを好きなエディタで開いて編集
  * エディタ上で保存するとSyncしているMonaca デバッガーがリスタートされ即時実機に反映される

     !!!! ペアリングできないとき !!!!
     1. Monaca デバッガーのスタートメニューを起動
     2. メニュー　＞　ローカルコンピューターを選択
     3. 「コンピューターを手動追加する」を選択
     4. PCのローカルIPアドレス調べる
       ターミナルでifconfig en0 と打ってEthernet（en0）のinet(IPv４アドレス)を確認
       上記で確認したIPアドレスを入力
       portはMonaca LocalKitでMonaca LocalKit＞設定で待ち受けポートで入力されているポートを入力する
       Pairを選択してペアリング確認

## Gitを準備
1. [GitHub](https://github.com/)でリポジトリを作る
2. .git/configで設定を変更してローカルのディレクトリと同期する

## Monacaのプロジェクトを作成
1. MonacaLocalKitで`Command + n`でMonacaプロジェクト作成
2. 作業ディレクトリをGitの準備で作成したディレクトリにディレクトリを作成しそこを設定し、
テンプレートは`Onsen UI Master-Detail`にする（Git管理下のrootディレクトリだと作成できなかった）

## 参考
  * [GitHub 製エディタ Atom入門](http://qiita.com/k2works/items/1d25888fb3a05058e48f)
