+++
tags = ["SEO", "Hugo"]
categories = ["まとめ", "web"]
description = "私的Hugo設定まとめ"
menu = ""
banner = ""
images = []
title = "HugoのSEOなど設定まとめ"
date = 2019-04-09T17:14:41+09:00
draft = true
+++

# Hugoで作ったサイトをGoogleに拾ってもらう

[Google Search Console](https://search.google.com/search-console/about) にドメインを登録しよう

次にサイトマップを登録する。

Hugoの場合サイトマップは /index.xml に生成されている。ので、これをGoogle Search Consoleに登録しよう。反映には時間がかかるようだ。

# Google Analyticsの設定
普通にGoogle AnalyticsのトラッキングIDの取得をしておく。このIDを控えておいて、 config.toml に記入する。

このサイトで使っている Icarus テーマだと
```toml
# Enable Google Analytics by entering your tracking code
googleAnalytics = "ここにトラッキングコードを書く"
```

<!--more-->
