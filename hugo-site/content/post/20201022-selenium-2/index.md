+++
tags = ["dev", "selenium", "selenium-webdriver", "ruby"]
categories = ["blog", "dev"]
description = "Selenium WebDriver on Rubyで遊んだり効率化したりしよう！その2 waitを扱うなど"
menu = ""
thumbnail = "selenium.png"
slug = "selenium-2"
title = "Selenium WebDriver on Rubyで遊んだり効率化したりしよう! (2)"
date = 2020-10-22T11:07:10+09:00
+++

[前回]({{< ref "/post/20201020-selenium-1" >}})の続きです

### これまでの目次
- [その1 … 基本編]({{< ref "/post/20201020-selenium-1" >}})
- [その2 … waitやwindow_handle]({{< ref "/post/20201022-selenium-2" >}})

# 要素が出現するのを待つ
通常でも、手続き的に連続して書いておけばページロードがある程度完了するまでは待ってくれる。
しかし、xhrでの読み込みやスクリプトによるDOMの改変、展開などである要素が出現するのを明示的に待つ必要がある場合もある。

そんなときは `Selenium::WebDriver::Wait` を使う

```ruby
wait = Selenium::WebDriver::Wait.new(:timeout => TIMEOUT)
wait.until do
    driver.find_element(....).displayed?
end
```
`wait.until` ブロックでは、評価結果がtrueとみなせるまで一定の周期(設定可能)で、一定の間(上記例だと `:timeout` )に渡り実行を繰り返す。

## ちょっとひねったパターン
find_elementにcssやxpathを使ったりしている場合に、要素が見つからない場合に例外が出てくるので、上記の例だとうまくいかないこともある。

```ruby
wait.until do
    begin
        driver.find_element(...).click
        true
    rescue
        nil
    end
end
```
# ポップアップしてくるウインドウ(タブ)を扱う
なにかしらclickすると新しいポップアップ(ウィンドウだったりタブだったり)がある場合がある。

そのまま処理を続けたいが、ドライバのインスタンスはその送信先を1つのwindow(タブ含む)に限定しているため、これを切り替えないといけない。

## ポップアップされたウィンドウ(タブ)を識別する
こんな感じで識別できる

```ruby
main_window = driver.window_handle
driver.find_element(なにかしらポップアップされるやつ).click
wait.until { driver.window_handles.length == 2 }
popup_window = driver.window_handles.detect { |e| e != main_window }
driver.switch_to.window popup_window
```

重要な要素は以下の通り

- `driver.window_handle` で、現在のウィンドウ(タブ)のハンドル(IDみたいなもの)を取得できる
- `driver.window_handles` で、いま開いているウィンドウ(タブ)のハンドル配列を取得できる
- `driver.switch_to.window` で、指定したウィンドウ(タブ)のハンドルに操作先を切り替えられる


### 次は
前回と今回で結構カバーできている気もしますが、もう少しトピックがあるかもしれないので含みをもたせつつ今回は終わり。
