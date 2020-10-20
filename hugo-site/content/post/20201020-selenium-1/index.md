+++
tags = ["dev", "selenium", "selenium-webdriver", "ruby"]
categories = ["blog", "dev"]
description = "Selenium WebDriver on Rubyで遊んだり効率化したりしよう！その1"
menu = ""
thumbnail = "selenium.png"
slug = "selenium-1"
title = "Selenium WebDriver on Rubyで遊んだり効率化したりしよう! (1)"
date = 2020-10-20T11:22:53+09:00
+++

# Selenium WebDriverで遊ぼう
Selenium WebDriverがあれば、httpを直接喋ったり、mechanizeやnokogiriで遊ぶより以下のことが出来て嬉しい。
- javascriptを使ったレンダリングなどに対応できる
- javascriptをコールできる
- chromeなどブラウザの挙動そっくりそのままを再現できる

Selenium WebDriver on Ruby で、いろいろ遊んだり、今流行の(多分嘘)RPAしたりやっていくぞ！

# 準備
これはごく普通に
`gem install selenium-webdriver`
でいいはず。

ただ、これだけでは動かなくて、selenium-webdriverのdriverをダウンロードしてくる必要がある。ここではchromeのdriverを使おうと思うので、 https://chromedriver.chromium.org/downloads から、良い感じのやつをダウンロードしてきてインストールする。

# とりあえずURLを開いてみる
こんな感じ
```ruby
driver = Selenium::WebDriver.for :chrome
driver.navigate.to "https://ほげほげ/"
```
このスクリプトを実行してみると、Chromeのウィンドウが開いて、指定したURLが開くはず。なるほどこうやって動くのか、という感動ありますね。

# 要素を探してクリックしてみる
ページが開けたら、やってみるのはまずは要素(リンクなり、ラジオボタンなり)をクリックしてみることです。

要素を探すのはこんな感じです。
```ruby
driver.find_element(:name, 'ほげ')
driver.find_element(:xpath, "//input[@value='ふが']")
driver.find_element(:css, 'div#なんとか > a:first-child')
```
だいたいは上記の3つぐらいで探せるはず。name, xpath, cssでの検索が出来ます。

find_elementの戻り値は `.click` でクリック操作ができます。

# 要素を探して値を入力してみる
RPA的なことをしたかったりするなら、クリックだけではなくてテキスト入力も必要になってきますね。その場合は、`input`をfind_elementした上で、以下のようにします。

```ruby
element.send_keys "入力したい文字列"
```
# javascriptを実行する
基本的には人間の操作としては上記だけでも随分いろいろ出来るのですが、任意のスクリプトを実行したいこともあります。すべてをクリックで操作するんじゃなくて、特定のfunctionを呼べばいいとわかっている場合など。ブラウザでもコンソールなどを使えば同じことができますのでその代わりです。

```ruby
driver.execute_script("login_check()")
```

すごくシンプル。

### 次は
次はもう少し高度な...たとえば非同期でページのコンテンツをロードしてくるなどで、最初からすべての要素が準備できていない場合など...を扱ってみたいと思います。
