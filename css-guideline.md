# CSS Guideline
## はじめに
私が約3年コーディングを経験してきた中での最適解をまとめたものです。「わかりやすい、使いやすい」と思って作成しましたが、まだ発展途上です。
私は最近のモダンフロントエンドに沿うような、高いスキルを持ち合わせていません。
ただ今まで少しづつ積み重ねてきたフロントの知識をアウトプットしていくために、CSSのことについて残してみたいと思います。

## 影響を受けたCSS設計
「FLOCSS」https://github.com/hiloki/flocss

``
class名にはprefixをつけることで、「どこにスタイルが書かれているのか」や「それはどんな役割なのか」が非常にわかりやすく、とても気に入りました。
そして私は、prefixをもう少し視覚的にわかりやすくしたかったので、このFLOCCSを応用したものをプロジェクトに取り入れてみることにしました。
``
## ファイル構成・ディレクトリ構成

````
├── assets
│   └── dist..
│   └── src
│       ├── images
│       ├── index.html
│       ├── js
│       │   ├── accordion.js
│       │   ├── backfaceFixed.js
│       │   ├── drawer.js
│       │   ├── footer-fixed.js
│       │   ├── hover.js
│       │   ├── main.js
│       │   ├── noopener.js
│       │   ├── screen-animate.js
│       │   ├── scrollobserver.js
│       │   ├── slideshow.js
│       │   ├── smooth.js
│       │   ├── userAgent.js
│       │   ├── viewport.js
│       │   └── worbreak.js
│       ├── scss
│       │   ├── base
│       │   │   ├── _b-00_author.scss
│       │   │   ├── _b-01_reset.scss
│       │   │   ├── _b-02_base.scss
│       │   │   └── _index.scss
│       │   ├── global
│       │   │   ├── _index.scss
│       │   │   ├── mixin
│       │   │   │   └── _mixin.scss
│       │   │   └── variables
│       │   │       ├── _v-01_config.scss
│       │   │       ├── _v-02_function.scss
│       │   │       ├── _v-03_color.scss
│       │   │       └── _v-04_font.scss
│       │   ├── module
│       │   │   ├── _m-01_header.scss
│       │   │   ├── _m-02_gNav.scss
│       │   │   ├── _m-03_spNav.scss
│       │   │   ├── _m-04_main.scss
│       │   │   ├── _m-05_sidebar.scss
│       │   │   ├── _m-06_footerNav.scss
│       │   │   ├── _m-07_footer.scss
│       │   │   ├── layout
│       │   │   │   ├── _ly-01_grid.scss
│       │   │   │   └── _ly-02_wrapper.scss
│       │   │   └── wp-layout
│       │   ├── object
│       │   │   ├── component
│       │   │   │   ├── _accordion.scss
│       │   │   │   ├── _arrow.scss
│       │   │   │   ├── _badge.scss
│       │   │   │   ├── _breadcrumb.scss
│       │   │   │   ├── _button.scss
│       │   │   │   ├── _card.scss
│       │   │   │   ├── _follow.scss
│       │   │   │   ├── _headline.scss
│       │   │   │   ├── _hover.scss
│       │   │   │   ├── _input.scss
│       │   │   │   ├── _media.scss
│       │   │   │   ├── _noscript.scss
│       │   │   │   ├── _pagination.scss
│       │   │   │   ├── _paragraph.scss
│       │   │   │   ├── _search.scss
│       │   │   │   ├── _share.scss
│       │   │   │   ├── _tags.scss
│       │   │   │   └── _topScroll.scss
│       │   │   ├── project
│       │   │   │   ├── _infomation.scss
│       │   │   │   ├── _revealer.scss
│       │   │   │   ├── _solution.scss
│       │   │   │   └── _top.scss
│       │   │   ├── scope
│       │   │   └── theme
│       │   │       ├── _animate.scss
│       │   │       └── _border.scss
│       │   ├── plugin
│       │   ├── test
│       │   │   └── _test.scss
│       │   └── utility
│       │       └── _utility.scss
│       └── style.scss
└── gulpfile.js
````

### base
htmlタグ, bodyタグには、color, fontベースを設定。settingsフォルダ内のSCSSファイル（変数）と合わせて管理。

### reset
リセットCSSは、プロジェクト毎に一度チェックする。
基本的にresetで、色、サイズ、余白などのスタイルを当て無いこと。
ユーティリティクラスの量産を避け、!importantを用いる無理な調整などをしない為にもリセットCSSを確認することは重要な作業。
より強力なリセットが求められる場合は、HTML5 Doctor CSS Resetを使用する。

### variable

|variable      |                                                         |
|--------------|---------------------------------------------------------|
|mixin         |@media: メディアクエリ                                   |
|config        |コンテナサイズ、メディアクエリの数値、z-index, transition|
|color         |文字色、背景色                                           |
|font          |font-family, font-size(options)                          |
|function      |rem => pxへの変換などの関数を格納                        |

### module
ワイヤーフレームに定義されるような大きなブロックコンテナが該当する。この部分のみIDセレクタで指定する事が許容される。(header, header-nav, drawer sidebar, footer-nev, footerなど。) componentと組み合わせることで完成する。
moduleは独自のアセットとして用意していることがほとんどのため、スニペット登録、トレンドのデザインは抑えておくとベスト。

### module/lauout
接頭辞を “ly-” で統一。

### object
再利用可能なパーツを格納する

### object/component
多くのプロジェクトで横断的に利用できるような最小単位のモジュールが該当する。Bootstrapのcomponent-categoryを参照。
(button, breadcrumb, snsIcons, pagination, card...)

### object/Project
プロジェクト固有のビジュアルパターン (ユーザーインターフェース)に該当し、object/componentパーツ、その他の要素で構成される最大単位のモジュールを管理する。

### utility
HTML上でスタイルを付けるため専用のclassを管理するものとして用いられる。HTMLは本来、文書構造を記述するものであって、積極的なスタイルを付けるべきでは無いと考えている。(Tailwind CSS, Bootstrapを除く)
特定のブロック(div, article, figure)に機能を持たせたい場合や詳細度を下げて抽象的にタグを使いたい場合など、スコープ外に影響しないことを前提に活用したい。『セレクタ指定は極力避ける』

utilityを使用する範囲は限定した方がCSSの破綻を防ぐことができる。margin, padding, positionなどのボックスモデル(位置調節系)以外は、許容範囲とする。
簡潔でわかりやすいclass名が求められることを意識したい。

````css
    .u-content-area {
        padding: 60px 0;
    }
    .u-flex {
        display: flex;
    }
    .u-flex-wrap {
        flex-wrap: wrap;
    }
    .u-flex-bet {
        justify-content: space-between;
    }
    .u-flex-content-center {
        align-items: center;
    }
    .u-flex-justify-center {
        justify-content: center;
    }
    .u-flex-row {
        flex-direction: row;
    }
    .u-flex-column {
        flex-direction: column;
    }
    .u-flex-none {
        display: block !important;
    }
    .u-visual-hidden {
        clip: rect(0 0 0 0);
        clip-path: inset(50%); 
        height: 1px;
        margin: -1px;
        overflow: hidden;
        position: absolute;
        white-space: nowrap;
        width: 1px;
    }
    .u-under-line {
        border-bottom: 1px solid currentColor;
    }
    .u-uppercase {
        text-transform: uppercase;
    }
    .u-capitalize {
        text-transform: capitalize;
    }
    .u-brsp {
        display: none;
    }
    .u-brpc {
        display: inline-block;
    }
    @media screen and (max-width:767px) {
        .u-brsp {
            display: inline-block;
        }

        .u-brpc {
            display: none;
        }
    }
````

case: スクリーンリーダー対応用
```css
    .u-visual-hidden { 
        position: absolute;
        width: 1px;
        height: 1px;
        overflow: hidden;
        margin: -1px;
    }
```


## 名前空間
クラスの命名規則はBEMを使用しているため、接頭辞から次の要素名までは、アンダースコア(_)は使用せず、ハイフン(-)で繋ぐ。 

```md
    case:
    ├── module         | mod-  |  .mod-header
    ├── block          | bl-   |  .bl-wrapper
    ├── component      | c-    |  .c-btn
    ├── project        | p-    |  .p-btn
    ├── pageInPage     | a-    |  .a-top
    ├── utility        | u-    |  .u-flex
    ├── modal          | m-    |  .m-content
    ├── theme          | th-   |  .th-border
    ├── scope          | sc-   |  .sc-article-page
    ├── Javascript     | js-   |  .js-active
    └── *=state        | is-   |  .is-state
```

## フォーマット

### CSSプロパティを揃える
.csscomb.jsonを使用して揃える。
ABC順にフォーマット。

````json
{
    "remove-empty-rulesets": true,
    "always-semicolon": true,
    "color-case": "lower",
    "block-indent": "    ",
    "color-shorthand": false,
    "element-case": "lower",
    "eof-newline": false,
    "leading-zero": true,
    "quotes": "double",
    "sort-order-fallback": "abc",
    "sort-order": [],
    "space-before-colon": "",
    "space-after-colon": " ",
    "space-before-combinator": " ",
    "space-after-combinator": " ",
    "space-between-declarations": "\n",
    "space-before-opening-brace": " ",
    "space-after-opening-brace": "\n",
    "space-after-selector-delimiter": "\n",
    "space-before-selector-delimiter": "",
    "space-before-closing-brace": "\n",
    "strip-spaces": true,
    "tab-size": true,
    "vendor-prefix-align": true
}
````