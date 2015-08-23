---
layout: post
title:	簡単なタイマーアプリを作成する
---

## ゴール
* 入力値を元にカウントダウンする
* CordovaAPIを利用しサウンドを鳴らす

## サンプルプログラム
* [simple-timer(GitHub)](https://github.com/ffa500/simple-timer/tree/master/simple-timer)


## 画面の作成
今回はシンプルにsingleViewを作成し、UIはOnsenUIを用いる
1. index.htmlにナビゲーションバーを持つ画面を作成

## カウントダウン機能の実装
OnsenUIのテンプレートを入れるとAngularJSを用いるようになっているが期間も短いので使い慣れているjqueryで実装してます。(一部Angularが残ってます)

1. jqueryを導入
	* `www/lib/jquery/jquery.js`を配置
	* index.htmlでロードさせる
2. カウントダウン機能を実装する
	* `www/scripts/app.js`を作成し中に処理を記述する
	* index.htmlでロードさせる

## サウンドを鳴らす
[通知](http://cordova.apache.org/docs/ja/3.1.0/cordova_notification_notification.md.html)によるとサウンドを鳴らすにはCordovaのプラグインを入れる必要がある
1. プラグインを導入する

```sh
$ cordova plugin add org.apache.cordova.dialogs
```

2. ビープ音を再生する
beep音を鳴らす回数は`navigator.notification.beep(5);`のように記述すると指定できるのだが、途中で止めるAPIは用意されていないので、Intervalを利用して実装した。beepIntervalをグローバル変数として用意しておく必要がある。（フラグで制御する実装でもいいと思う）

```js
var playBeep = function(){
   navigator.notification.beep(1);//初回が鳴るまでスパンがあるのでまずは一回目を鳴らしてしまう。（暫定対処）
   beepInterval = setInterval(function(){
         navigator.notification.beep(1);
   },3000);
}
```

## サウンドを止める
ビープ音を再生した時に、[notification.alert](http://cordova.apache.org/docs/ja/3.1.0/cordova_notification_notification.md.html#notification.alert)を使ってalertViewを表示してOKを押した時にビープ音を停止させるようにする
* ビープ音を止める関数を用意する

```js
var stopBeep = function(){
   clearInterval(beepInterval);
}
```

* alertViewを表示する関数を準備
	* callback関数を準備できるのでalertViewのボタンが押された際に先に用意したビープ音を停止させる関数をセットしておく

```js
	var showAlert = function(){
  		navigator.notification.alert(
      	'',
      	stopBeep,
      	'タイマー終了'
   	);
}
```

## デザイン
あとでいじるかも。

## その他
ライブラリ使えばよかった。

