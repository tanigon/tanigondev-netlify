+++
tags = ["iOS", "URL", "mailto"]
categories = ["blog", "dev"]
description = "iOS14.6から? mailtoスキーマに改行文字を入れるとタグに化ける"
menu = ""
thumbnail = "mail-help.png"
slug = "ios146-mailto"
title = "iOS14.6から? mailtoスキーマに改行文字を含めると化ける"
date = 2021-06-10T22:50:00+09:00
+++

# 突然の問題
iOS14.6から(14.5以前では発生しない)、例えば、以下のようなURL

```
mailto:tanigon@tanigon.info?subject=hoge&body=test%0atest%0a
```

を叩いて、iOS標準メーラーを開くと

```
test<BR>test<BR>
```

のように謎の大文字brタグに置換されてしまい、改行が正しく扱えない。

## Gmailだと?

ちなみに、iOS14以降、デフォルトメーラーを設定できるようになっている。設定 -> Gmail -> デフォルト...で設定した上で上記と同様のことを行った場合は挙動がまた異なる。

ただ、こちらも改行はされず。さすがに大文字BRタグが発生するようなことはなかったが…

## htmlを入れるといいのか?

試しに `<br>` をURLencodeして含めてみたが、それは単にテキストとして挿入されるだけだった。万事休す

だれか解決方法知りませんか...?

