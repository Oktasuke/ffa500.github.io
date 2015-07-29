---
layout: post
title: OnsenUIを使ってTabBarアプリを実現する
---

## ゴール
TabBar構成のUIを理解&つくる

## テンプレート
* tabbarを実現したサンプルコードは以下にあります。（「あるものは使え、ないものは作れ」です）
 * [tabbar-template(GitHub)](https://github.com/ffa500/tabbar-template)

## ソース解説
### モジュールを関連付ける
ng-appというAngularJSのディレクティブを利用して、アプリケーションのルートを指定します。
ngAppディレクティブがhtml要素上に無ければ、 ドキュメントはコンパイルされないので注意。
下記は`ng-app="{angular.Module}"`というディレクティブを利用しています。引数には読み込むモジュールを宣言します。


```html
<html lang="en" ng-app="simpleTabApp" ng-csp>

```

### モジュールの定義
* ポイント
 * `angular.module('simpleTabApp', ['onsen']);`でsimpleTabAppというモジュールを作成し、第二引数でonsenモジュールが必要であることを宣言します。
 * `angular.module('simpleTabApp').controller(...)`では宣言したsimpleTabAppというモジュールにAppControllerを登録します。

```javascript
    <script>
        angular.module('simpleTabApp', ['onsen']);

        angular.module('simpleTabApp').controller('AppController', function ($scope) {
            //ここに独自のイベントとかを追記します
        });
    </script>
```

* moduleメソッドについて
 * angular.module(name [,requires] [,config])
   * name： モジュール名（string）
   * requires： 依存するモジュール（Array<string>）
   * config： モジュールの構成情報を設定する関数（Function*1）

### タブバーの設定
* ポイント
 * タブバーは`<ons-tabbar>`と`<ons-tab>`をつかって生成します。
 * `active="true"`を宣言するとそこがデフォルトの表示タブになります。
 * `page=worldClock.html`でタブがアクティブになった際のテンプレートを指定します。


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

ちなみに上記がレンダリングされると以下になる。この処理が気になる場合はonsenui.jsをみてみると書いてあるので見てみてもいいかもしれない。


```html
<ons-tabbar class="ng-scope">
	<div class="ons-tab-bar__content tab-bar__content">
		<ons-navigator class="ng-scope">
		<ons-page class="ng-scope page">
			<ons-toolbar class="navigation-bar" style="position: absolute; z-index: 10000; left: 0px; right: 0px; top: 0px;">
				<div class="left navigation-bar__left">&nbsp;</div>
				<div class="center navigation-bar__title navigation-bar__center">世界時計</div>
				<div class="right navigation-bar__right">&nbsp;</div>
			</ons-toolbar>
				<div class="page__background"></div>
				<div class="page__content ons-page-inner" no-status-bar-fill="">
					<ons-list style="margin: -1px 0" class="list ons-list-inner">
                     	<!-- ngRepeat: i in [1] -->
                     	<ons-list-item modifier="chevron" class="item ng-scope list__item ons-list-item-inner list__item--chevron" ng-repeat="i in [1]" ng-click="showDetail()">
                        	<ons-row class="row ons-row-inner">
                            	<ons-col width="60px" class="col ons-col-inner" style="-webkit-box-flex: 0; flex: 0 0 60px; max-width: 60px;">
                                	<div class="item-thum"></div>
                            	</ons-col>
                            	<ons-col class="col ons-col-inner">
                            	    <header>
                                    	<span class="item-title">東京</span>
                                	</header>
                                	<h2 class="item-desc">16:00</h2>
                            	</ons-col>
                        	</ons-row>
                    	</ons-list-item><!-- end ngRepeat: i in [1] -->
                	</ons-list>
				</div>
			</ons-page>
		</ons-navigator>
	</div>

	<div ng-hide="hideTabs" class="tab-bar ons-tab-bar__footer  ons-tabbar-inner">
        <ons-tab active="true" page="worldClock.html" class="ng-scope tab-bar__item ng-isolate-scope active">
        	<input type="radio" name="tab-bar-1438183452276" style="display: none">
			<button class="tab-bar__button tab-bar-inner  " ng-click="tryToChange()">
            	<div class="tab ng-scope">
                	<ons-icon icon="ion-ios-world-outline" class="tab-icon ons-icon ons-icon--ion ion-ios-world-outline fa-lg"></ons-icon>
                	<div class="tab-label">世界時計</div>
            	</div>
        	</button>
		</ons-tab>
        <ons-tab page="alarm.html" class="ng-scope tab-bar__item ng-isolate-scope">
        	<input type="radio" name="tab-bar-1438183452276" style="display: none">
			<button class="tab-bar__button tab-bar-inner  " ng-click="tryToChange()">
            	<div class="tab ng-scope">
            	    <ons-icon icon="ion-ios-alarm-outline" class="tab-icon ons-icon ons-icon--ion ion-ios-alarm-outline fa-lg"></ons-icon>
        	        <div class="tab-label">アラーム</div>
    	        </div>
	        </button>
		</ons-tab>

        <ons-tab page="stopWatch.html" class="ng-scope tab-bar__item ng-isolate-scope">
        	<input type="radio" name="tab-bar-1438183452276" style="display: none">
			<button class="tab-bar__button tab-bar-inner  " ng-click="tryToChange()">
            	<div class="tab ng-scope">
                	<ons-icon icon="ion-ios-stopwatch-outline" class="tab-icon ons-icon ons-icon--ion ion-ios-stopwatch-outline fa-lg"></ons-icon>
                	<div class="tab-label">ストップウォッチ</div>
            	</div>
        	</button>
		</ons-tab>

        <ons-tab page="timer.html" class="ng-scope tab-bar__item ng-isolate-scope">
        	<input type="radio" name="tab-bar-1438183452276" style="display: none">
			<button class="tab-bar__button tab-bar-inner  " ng-click="tryToChange()">
            	<div class="tab ng-scope">
            		<ons-icon icon="ion-ios-timer-outline" class="tab-icon ons-icon ons-icon--ion ion-ios-timer-outline fa-lg"></ons-icon>
        	    	<div class="tab-label">タイマー</div>
            	</div>
        	</button>
		</ons-tab>
	</div>
</ons-tabbar>
```

### タブのテンプレート宣言
* ポイント
 * タブのテンプレートは`<ons-template>`をつかって宣言します。このときのid属性に指定した値がタブバー作成時に記載した`<ons-tabbar>`のpage属性に指定した値にすることで指定したタブで表示するテンプレートになります
 * ナビゲーションバーを使いたい場合は各タブで表示するテンプレートで宣言してあげます。


```html
    <!-- 世界時計タブ内の画面を定義しているテンプレートです -->
    <ons-template id="worldClock.html">
        <ons-navigator>
            <ons-page>
                <ons-toolbar>
                    <div class="center">世界時計</div>
                    <div class="right"></div>
                </ons-toolbar>
                <ons-list style="margin: -1px 0">
                     <ons-list-item modifier="chevron" class="item">
                        <ons-row>
                            <ons-col width="60px">
                                <div class="item-thum"></div>
                            </ons-col>
                            <ons-col>
                                <header>
                                    <span class="item-title">東京</span>
                                </header>
                                <h2 class="item-desc">16:00</h2>
                            </ons-col>
                        </ons-row>
                    </ons-list-item>
                </ons-list>
            </ons-page>
        </ons-navigator>
    </ons-template>
```


## チーム開発のためにやりたいこと
以下のようにタブバーのコンテンツを外だししてチーム開発しやすい構成にしたかったが、これをやると初回にDOMロードされなかった。
今後改修する予定。

```html
    <link rel="import" href="worldClock.html">
    <link rel="import" href="alarm.html">
    <link rel="import" href="stopWatch.html">
    <link rel="import" href="timer.html">
```


## 参考
[http://ja.onsen.io/reference/css.html#tab-bar](http://ja.onsen.io/reference/css.html#tab-bar)

