+++
tags = ["css", "dev"]
categories = ["blog", "dev"]
description = "CSSだけでレスポンシブに正方形を維持する方法"
menu = ""
slug = "css-square"
title = "CSSだけでレスポンシブに正方形を維持する方法"
date = 2019-09-05T00:00:24+09:00
+++

# div要素のアスペクト比を固定したい(例えば正方形)
デザイン上、div要素のアスペクト比を1:1(正方形)などに固定したい、ということがある。
当たり前だが、以下のコードは動作しない。
```html
    <div style="width:100%; height:100%">hoge</div>
```
親要素が正方形でない限り当然、高さと幅はバラバラに評価されるため。

# どうするの？
padding-topや-bottomの評価は、widthを基準に行われることを使う。ちょっとトリッキーだが…

```html
    <div class="parent">
        <div class="child">hoge</div>
    </div>
```
```css
    .parent {
        position: relative;
        overflow: hidden;
        width: 100%;
    }
    .parent:before {
        content: "";
        display: block;
        padding-top: 100%;
    }
    .child {
        position: absolute;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
    }
```

なお、親がposition:relative;なのも重要で、これがついてないと、子の posotion: absolute; の挙動が変わる。
(知らなかった。こちらで学ばせていただきました: [CSSのposition: absoluteとrelativeとは](https://uxmilk.jp/63409))



