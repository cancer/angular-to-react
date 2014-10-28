Yokohama.js (#yjs20140817)

## CSS Spriteを動的生成して快適ソシャゲ開発

---

## 自己紹介
![](https://avatars2.githubusercontent.com/u/730940?s=200)

宇野 陽太([@cancer6](https://twitter.com/cancer6))

株式会社モバイルファクトリーというところで<br>
フロントエンドエンジニアやってます

最近はBackbone / Marionette / AngularJS あたりを触ったり<br>
CSSの設計したりなど

---

## 生成の流れ
- Image Assets Generator(Photoshop) <!-- .element: class="fragment" data-fragment-index="1" -->
- フォルダに配置 <!-- .element: class="fragment" data-fragment-index="2" -->
- Compass (grunt-watch) <!-- .element: class="fragment" data-fragment-index="3" -->

---

## Image Assets Generator(Photoshop)

- [ファイル] → [生成]にチェックを入れておく <!-- .element: class="fragment" data-fragment-index="1" -->
- レイヤーにファイル名をつけておく <!-- .element: class="fragment" data-fragment-index="2" -->
- レイヤーが更新されると指定した名前で自動的に書き出し <!-- .element: class="fragment" data-fragment-index="3" -->
- ※ Photoshop CC以降 <!-- .element: class="fragment" data-fragment-index="4" -->

---

## フォルダに配置

- 職人が丹精込めて一つ一つ移動 <!-- .element: class="fragment" data-fragment-index="1" -->

---

## Compass (grunt-watch)

- CSSの生成と一緒にSpriteファイルも生成してくれる <!-- .element: class="fragment" data-fragment-index="1" -->
- 便利！ <!-- .element: class="fragment" data-fragment-index="2" -->

---

## CSS Sprite Helpers for Compass

http://compass-style.org/reference/compass/helpers/sprites/

---

## CSS Sprite Helpers(略)のいいところ

- 導入が楽 <!-- .element: class="fragment" data-fragment-index="1" -->
 - Compassが用意しているfunctionを使えばすぐ <!-- .element: class="fragment" data-fragment-index="2" -->
 - Sass(SCSS)ファイルに書いていくだけ <!-- .element: class="fragment" data-fragment-index="3" -->

---

## CSS Sprite Helpers(略)のよくないところ

- 謎い <!-- .element: class="fragment" data-fragment-index="1" -->
 - マッピング情報はRuby側で管理 <!-- .element: class="fragment" data-fragment-index="2" -->
 - functionで取得するのでキャッシュしておかないといけない <!-- .element: class="fragment" data-fragment-index="3" -->

--

## CSS Sprite Helpers(略)のよくないところ

- 遅い <!-- .element: class="fragment" data-fragment-index="1" -->
 - CSSの生成が遅くなる(画像の変更が無くても+数秒) <!-- .element: class="fragment" data-fragment-index="2" -->
 - Sass(SCSS)に変更があるたびに画像の差分をチェック <!-- .element: class="fragment" data-fragment-index="3" -->
 - (Spriteの生成が遅いわけではないです、たぶん) <!-- .element: class="fragment" data-fragment-index="4" -->

--

## CSS Sprite Helpers(略)のよくないところ

- 画像生成後にgrunt-watchが走らない <!-- .element: class="fragment" data-fragment-index="1" -->
 - 画像の最適化とかしてると地味につらい <!-- .element: class="fragment" data-fragment-index="2" -->

---

## grunt-spritesmith

https://github.com/Ensighten/grunt-spritesmith

---

## grunt-spritesmithのいいところ

- Compass...というかSassに非依存 <!-- .element: class="fragment" data-fragment-index="1" -->
 - LESSでもStylusでも使える <!-- .element: class="fragment" data-fragment-index="2" -->
- CSSの生成とCSS Spriteの生成を分離できる <!-- .element: class="fragment" data-fragment-index="3" -->
 - CompassはCSSの生成に集中 <!-- .element: class="fragment" data-fragment-index="4" -->
 - CSSの生成が早くなる <!-- .element: class="fragment" data-fragment-index="5" -->

--

## grunt-spritesmithのいいところ

- Compassみたいにブラックボックスじゃない <!-- .element: class="fragment" data-fragment-index="1" -->
 - マッピング情報はSass(SCSS)の変数化される <!-- .element: class="fragment" data-fragment-index="2" -->
 - 変数にアクセスするfunctionも一緒に書きだされる <!-- .element: class="fragment" data-fragment-index="3" -->

---

## grunt-spritesmithのよくないところ

- フォルダが分けられない <!-- .element: class="fragment" data-fragment-index="1" -->
 - 一つのフォルダを監視して一つのSpriteを生成する <!-- .element: class="fragment" data-fragment-index="2" -->
- CompassのI/Fと差異があるので、途中からの移行がつらい <!-- .element: class="fragment" data-fragment-index="3" -->
 - 規模が大きくなってくると全部差し替えとかやってられない <!-- .element: class="fragment" data-fragment-index="4" -->

---

## もう少し使いやすく...

- 複数のフォルダを監視するgruntTaskを作成 <!-- .element: class="fragment" data-fragment-index="1" -->
 - 対象のフォルダ以下にあるフォルダ名でSpriteファイルを生成 <!-- .element: class="fragment" data-fragment-index="2" -->
 - grunt-spritesmithが作るマッピング情報をJSONで保存 <!-- .element: class="fragment" data-fragment-index="3" -->
 - パースしてSass(SCSS)のMapに変換 <!-- .element: class="fragment" data-fragment-index="4" -->
- 既存のI/Fを再利用 <!-- .element: class="fragment" data-fragment-index="5" -->

---

## 今後やりたいこと
- Image Assets Generatorとgruntの連携 <!-- .element: class="fragment" data-fragment-index="1" -->
 - 職人のぬくもりを機械で置き換えたい <!-- .element: class="fragment" data-fragment-index="2" -->

---

### ご清聴ありがとうございました

