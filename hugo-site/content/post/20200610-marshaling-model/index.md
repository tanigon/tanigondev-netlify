+++
tags = ["dev", "rails", "ruby"]
categories = ["blog", "dev"]
description = "モデルをRails.cacheやその他Marshalでキャッシュする際に関連キャッシュを登録したくない時の方法"
menu = ""
banner = "rails.jpg"
thumbnail = "rails.jpg"
slug = "marshaling-model"
title = "ActiveRecordモデルをキャッシュする時に関連キャッシュを取り除く"
date = 2020-06-10T219:20:53+09:00
+++

# Rails.cacheにmodelをキャッシュする
`Rails.cache` などを使い、ActiveRecordのモデルのインスタンスをキャッシュ(==シリアライズして保管)する、ということがある。主にパフォーマンスチューニングのために、DBクエリを減らそう、というような場合。

そのモデルが、`has_many` などの関連(association)を持っている場合、単純にキャッシュにwriteすると、これらの関連のキャッシュが書き込まれてしまう。一件問題なさそうに見えるが、たとえば、関連先のモデルに対して直接アクセスしたりして内容が書き換わる可能性があったりして不都合なこともある。

そういった場合には、モデルをシリアライズ(Ruby的には Marshal.dump) する場合に、この「関連のキャッシュ」を消去してから書いてやる必要がある。

# 結論
キャッシュに書く前に、以下のようにするとよい。
```ruby
(modelの中で)
  @association_cache.clear
  Rails.cache.write(.....)
```
ただし、この方法はundocumentedなようなので注意されたし。modelの中から実行できない場合は、`instance_variable_get` などを使うとよい。

# 代替案
```ruby
(modelの中で)
def marshal_dump
    [@attributes, @new_record, @primary_keyなど適宜インスタンス変数...]
end

def marshal_load(array)
    @attributes, @new_recordなどなど... = *array
end
```
この方法でも、 @association_cache をシリアライズの対象に含めないことで同様の効果が得られる。が、逆にほかのインスタンス変数を書かないといけないのと、インスタンス変数が増えた場合にはこの両メソッドも同期して更新しなくてはならない。もっとも、モデルの中で独自に(永続化すべきような)インスタンス変数を持つことは少ないのかもしれないが。

