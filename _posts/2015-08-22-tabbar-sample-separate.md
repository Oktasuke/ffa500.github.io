---
layout: post
title: チーム開発がしやすいTabBar構成
---

## ゴール
tabbarのテンプレートを別ファイルに分けてチーム開発しやすくする

## テンプレート
* サンプルコードは以下にあります。
    * [tabbar-template-separate(GitHub)](https://github.com/ffa500/tabbar-template-separate)

## タブバーの宣言ポイント
* index.htmlにtabbarを宣言する際に、ons-tabの属性`page`を利用してViewのURLを記述する。

```html
    <!-- タブバーの宣言 -->
    <ons-tabbar>
        <ons-tab active="true" page="worldClock.html">
            <div class="tab">
                <ons-icon icon="ion-ios-world-outline" class="tab-icon"></ons-icon>
                <div class="tab-label">世界時計</div>
            </div>
        </ons-tab>
        <ons-tab page="alarm.html">
            <div class="tab">
                <ons-icon icon="ion-ios-alarm-outline" class="tab-icon"></ons-icon>
                <div class="tab-label">アラーム</div>
            </div>
        </ons-tab>
        <ons-tab page="stopWatch.html">
            <div class="tab">
                <ons-icon icon="ion-ios-stopwatch-outline" class="tab-icon"></ons-icon>
                <div class="tab-label">ストップウォッチ</div>
            </div>
        </ons-tab>
        <ons-tab page="timer.html">
            <div class="tab">
                <ons-icon icon="ion-ios-timer-outline" class="tab-icon"></ons-icon>
                <div class="tab-label">タイマー</div>
            </div>
        </ons-tab>
    </ons-tabbar>
```

## タブがアクティブになった際のViewの宣言
* ons-tabの属性`page`に指定したファイル名と同じものをwww/配下に配置する。
* `<ons-template>`を使う必要はない。`<ons-template>`は同一ファイルにまとめたい場合にidにファイル名を記載することでViewに仮想URLを付与することができるもの。

## 参考
[ons-tab](http://ja.onsen.io/reference/ons-tab.html)
[ons-template](http://ja.onsen.io/reference/ons-template.html)
