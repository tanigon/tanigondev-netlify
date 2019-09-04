---
title: "SteamのDotEmu系ゲーム(METAL SLUG Xなど)でパッド入力がおかしいのを対策する"
description: "SteamのDotEmu系ゲーム、たとえば METAL SLUG X で、パッド(箱コンなど)操作で、ナナメ移動ができない、一部の複数同時入力が受け付けられない、操作が途切れるなどの事象が発生する。これの対策方法のメモ。"
date: 2019-05-28T17:30:54+09:00
slug: "steaminput"
tags: ["steam", "game", "metalslug"]
categories: ["blog", "game", "steam"]
images: ["steamfix1.png", "steamfix2.png", "steamfix3.png"]
banner: "banner-metalslug.png"
thumbnail: "banner-metalslug-thumbnail.png"
---

@feiz とMETAL SLUG Xをプレイしようとしたらパッド入力がグリッチしまくって大変だったのでその対策結果のメモ

## tl;dr (長くねえよ)
METAL SLUG X でパッドを使っていて入力がグリッチする、抜けるなどの場合、「Steam入力」を強制オフにせよ

# 事象
Steamで販売されている、 METAL SLUG X など DotEmu 系ゲームで、Xboxコントローラなどパッドを入力デバイスとして使っているときにたとえば、以下のようになる

- 入力が途切れる (横を押しっぱなしにしているのに途切れる)
- ナナメ方向に入力できない
- 方向キー＋ショットボタンなどで同時入力できなかったりする

かつ、

- DotEmu系 ではない他のゲームでは大丈夫
- キーボード入力だと大丈夫

となる。

# 対策

まず、ライブラリを開いて、対象となるゲームを見つける。以下は METAL SLUG X を例にとる。

{{< figure src="steamfix1.png" title="対象となるゲームを選ぶ" >}}

次に、これを右クリックして、プロパティを開く

{{< figure src="steamfix2.png" title="右クリックしてプロパティを選ぶ" >}}

Steam入力を云々という設定項目が下のほうにあるのでこれを「強制オフ」にする

{{< figure src="steamfix3.png" title="Steam入力の設定を「強制オフ」にする" >}}

これでなおったよ。

# さいごに
Steam Inputってなんやろ? 調べてみたい
