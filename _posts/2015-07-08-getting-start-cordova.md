---
layout: layout_posts
title: Cordovaでのアプリ開発を始める
---

## Cordovaとは

[Apache Cordova](https://cordova.apache.org/)より

> Apache Cordova is a set of device APIs that allow a mobile app developer to access native device function such as the camera or accelerometer from JavaScript. Combined with a UI framework such as jQuery Mobile or Dojo Mobile or Sencha Touch, this allows a smartphone app to be developed with just HTML, CSS, and JavaScript.

## Getting Started with Android

[Getting Started with Android](http://cordova.apache.org/docs/en/2.3.0/guide_getting-started_android_index.md.html)でお勉強

## ツールの準備

MacでセットアップしたのでWindowsだとどうなるか不明。。。

### Android Studioをインストール

- Android SDK
- ADT Plugin

### Cordovaをインストール

- CLIツールのインストール
 - Node.jsをインストール
 - (なければ)Gitのインストール

```
$ node -v
v0.10.31
$ git --version
git version 2.2.1
$ npm install -g cordova
```

権限がなくてエラーになるので、所有者を変更

```
sudo chown -R $(whoami) /usr/local
```

バージョン確認

```
$ cordova -v
5.1.1
```

### Androidまわりのパス設定

以下のフォルダへのパスを、.bash_profileで追加

- Android SDK platform-tools
- Android SDK tools

Android SDKのインストール場所/sdk以下にある

### プロジェクトの新規作成

プロジェクトを作成するディレクトリに移動してコマンド実行

```
$ cordova create location_demo com.nifty.cloud.mb.locationdemo LocationDemo
```

platformとしてAndroidを追加して結果を確認

```
$ cd location_demo/
$ cordova platform add android
$ cordova platform ls
Installed platforms: android 4.0.2
Available platforms: amazon-fireos, blackberry10, browser, firefoxos, ios
```

フォルダの中身を確認

```
$ ls
config.xml hooks      platforms  plugins    www
```

Monacaでプロジェクトエクスポートしたときに似てる
(CordovaベースのMonacaなんだからそりゃそうだ

### エミュレーターで実行

```
$ cordova emulate android
```

### 実機でデバッグ

- Android Studioでプロジェクトを開く
 - Import Project
 - /path to cordova project/platforms/androidを指定
- デバッグ用の実機をUSB接続してプロジェクトをRunさせる
