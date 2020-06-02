+++
tags = ["db", "dev", "mysql", "ruby"]
categories = ["blog", "dev"]
description = "mysql: VARCHARの列幅の差と TEXT型とでINSERT性能には殆ど違いない"
menu = ""
slug = "varchar-vs-text"
title = "mysql: VARCHARの列幅の差と TEXT型とでINSERT性能には殆ど違いない"
date = 2020-06-02T20:44:31+09:00
+++

(Qiita repost)
# なにこれ (tl;dr)
mysql5.7にて、VARCHAR(10)とVARCHAR(30000)ではINSERTなどで差が出る、という話を聞いたのと、よく言われている TEXT型は遅い、という話をベンチマークしてみたら少なくともINSERTは全然差がないことがわかった、という話

ただしTEXT型は検索する場合は当然差が出て来るが、割愛。

# 測定用スクリプト
```ruby
    con = ActiveRecord::Base.connection

    # utf8mb4が検証環境のため 65535/4=16383
    length_set = [255, 4096, 16383, :text]
    string_set = [250, 4090, 16380]
    try_count = 10000

    demostr = "123456789A"

    raw_con = con.raw_connection

    Benchmark.bm 40 do |bm|
      length_set.each do |length|
        column_type = length == :text ? "text" : "varchar(#{length})"
        con.execute("create table length_test (str #{column_type})")
        insert_sql = raw_con.prepare("insert into length_test values(?)")
        begin
          string_set.each do |strlen|
            next if length != :text && strlen > length

            insertstr = demostr * (strlen / 10)
            bm.report "#{column_type} <-- string(#{strlen})" do
              try_count.times do
                insert_sql.execute(insertstr)
              end
            end
          end
        ensure
          insert_sql.close
          con.execute('drop table length_test')
        end
      end
    end
```

# 結果
INSERT10000回

|  | 文字列長250 | 文字列長4090 | 文字列長16380 |
|:--|--:|--:|--:|
| varchar(255) | 13.229861 |  |  |
| varchar(4096) | 13.623846 | 18.922998 |  |
| varchar(16383) | 13.380692 | 18.426866 | 45.27052 |
| text | 12.739086 | 18.534715 | 46.134611 |

# 考察
- varcharの列幅による有意な違いはない
- ただし、INSERTする文字列の長さには相関関係がある(正比例ではないのもやっかい)
- text型へのINSERT性能は悪くない (繰り返しになるが SELECT では別。WHEREの対象になるとさらに遅いかもしれない)
- 現状、1レコードの総バイト数が65535を超えることが出来ない? ようなので、こんな長さの文字列を複数持つことは出来ない
- utf8mb4 だと1文字表現するのに4bytes使うので、VARCHAR(65535)とは出来ない。4でdivすることになる

