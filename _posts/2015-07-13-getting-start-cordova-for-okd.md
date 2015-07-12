---
layout: post
title: okawaさん記事を元にCordovaを準備する
---

## ゴール
Cordovaを理解しつつ開発環境を整える

## [Cordova](https://cordova.apache.org/)とは？
* 一言でまとめると
 * Apache Cordova is a platform for building native mobile applications using HTML, CSS and JavaScript

* About Apache Cordova™から要点を抜き出すと
 * web technologies are used, and they are hosted in the app itself locally
 * Cordova provides a set of uniform JavaScript libraries that can be invoked, with device-specific native backing code for those JavaScript libraries
* 歴史的には
 * AdobeのPhoneGapをOSS化したとか

## Cordovaの準備
1. AndroidStudioをインストール
  * https://developer.android.com/sdk/installing/index.html?pkg=studio
2. JVMのインスール
  * JVMがない場合、AndroidStudioを開いたときにインスールしてね！とメッセージが出るのでそこからインストールするのが早い。
3. ADT Pluginをインストール
  * AndroidStudioの初回起動で言われた通りに進めれば入る
4. node.jsをインストール
  * http://nodejs.jp/nodejs.org_ja/docs/v0.10/
5. 確認

  ```
  $ java -version
  java version "1.6.0_65"
  Java(TM) SE Runtime Environment (build 1.6.0_65-b14-466.1-11M4716)
  Java HotSpot(TM) 64-Bit Server VM (build 20.65-b04-466.1, mixed mode)  
  ```

  ```
  $ node -v
  v0.10.25
  ```

  ```
  $ git --version
  git version 2.3.2 (Apple Git-55)
  ```
7. パーミッション変更
```
sudo chown -R $(whoami) /usr/local
```

8. Cordovaのインストール
  * 以下コマンドを実行（git必要）
  ```
  $ sudo npm install -g cordova
  ```
シンボリックリンクまで貼ってくれますね。ありがたやー
  ```
  /usr/local/bin/cordova ->/usr/local/lib/node_modules/cordova/bin/cordova
  ```

9. 環境変数PATHを追加
AndroidSDKのtoolsとplatform-toolsにPATHを通す必要性があるので.bash_profileに追加。自分の場合はデフォルトで進めてたので以下PATHに通してます。
```
/Users/内緒/Library/Android/sdk/tools
/Users/内緒/Library/Android/sdk/platform-tools
```
以下をわすれずにー。
```
$ source ~/.bash_profile
```
確認は以下で
```
$ android -h

       Usage:
       android [global options] action [action options]
       Global options:
  -h --help       : Help on a specific command.
```
```
$ adb version
Android Debug Bridge version 1.0.32
```


## プロジェクトを作成する
1. git管理かのディレクトリで以下コマンドでcordovaプロジェクトを作成。
```
cordova create timer_demo  com.nifty.timer_demo TimerDemo -d
```
「timer_demoディレクトリを作りその配下にcom.nifty.timer_demoというアプリ識別子をもつTimerDemoという名前のアプリのプロジェクトを作成する」という感じ。

2. platformを追加する
  * android
  エミュレーターで確認完了
  ```
$ cordova platform add android
Adding android project...
Creating Cordova project for the Android platform:
	Path: platforms/android
	Package: com.nifty.timer_demo
	Name: TimerDemo
	Activity: MainActivity
	Android target: android-22
Copying template files...
  ```
  * ios
  ```
  $ cordova platform add ios
Adding ios project...
iOS project created with cordova-ios@3.8.0
Installing "cordova-plugin-whitelist" for ios
```

3. 実行してみる
* android
 ```
 $ cordova emulate android
 ```
* ios
```
$ cordova emulate ios
ios-sim was not found. Please download, build and install version 3.0.0 or greater from https://github.com/phonegap/ios-sim into your path. Or 'npm install -g ios-sim' using node.js: http://nodejs.org
Error: /Users/OKD/sandbox/ffa500.github.io/sandbox/timer_demo/platforms/ios/cordova/run: Command failed with exit code 2
```
エミュレーターがないよ！と言われるので言われた通りにインストールする。
せっかくnodeがあるので以下で。emulateを再実行すれば起動確認できる。
```
$ npm install -g ios-sim
```
エミュレーターで確認完了
