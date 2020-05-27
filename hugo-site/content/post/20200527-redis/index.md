+++
tags = ["redis", "dev"]
categories = ["blog", "dev"]
description = "Redisでどんなコマンドが発行されているかを見る方法"
menu = ""
slug = "redis-trace"
title = "Redisのデバッグ、トレースログ"
date = 2019-09-05T00:00:24+09:00
+++

# Redisでどんなコマンドが発行されているかを見たい
monitor コマンドを使います
```
$ redis-cli
127.0.0.1:6379> monitor
OK
1590568977.855454 [0 172.18.0.1:36648] "get" "hoge"
1590568977.856992 [0 172.18.0.1:36648] "get" "hoge2"
```

# ログレベルを変更したい
コマンドの発行についてまでは出ませんが Redisのloglevelも変更できます
```
$ redis-cli
> config get loglevel
とか
> config set loglevel "debug"
```

# スロークエリのしきい値を変えたい
configはなんでもいじれるので
```
$ redis-cli
> config set slowlog-log-slower-than 0
OK
> slowlog get
.
.
```
