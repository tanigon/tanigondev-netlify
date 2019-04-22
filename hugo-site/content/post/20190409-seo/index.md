+++
tags = ["SEO", "Hugo"]
categories = ["まとめ", "web"]
description = "私的Hugo設定まとめ(個人メモ) WIPです"
menu = ""
banner = ""
images = []
title = "HugoのSEOなど設定まとめ(WIP)"
date = 2019-04-09T17:14:41+09:00
+++

# Hugoで作ったサイトをGoogleに拾ってもらう

[Google Search Console](https://search.google.com/search-console/about) にドメインを登録しよう

次にサイトマップを登録する。RSSとサイトマップ両方を指定することが望ましい、らしいので以下のようにする

## RSSフィードを登録する
Hugoの場合は /index.xml に生成されている。ので、これをGoogle Search Consoleに登録しよう。反映には時間がかかるようだ。

## sitemapを登録する
同様に /sitemap.xml が生成されているので、これも登録する。

# Google Analyticsの設定
普通にGoogle AnalyticsのトラッキングIDの取得をしておく。このIDを控えておいて、 config.toml に記入する。

このサイトで使っている Icarus テーマだと
```toml
# Enable Google Analytics by entering your tracking code
googleAnalytics = "ここにトラッキングコードを書く"
```

<!--more-->
