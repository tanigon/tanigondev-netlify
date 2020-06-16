+++
tags = ["dev", "unity", "aws"]
categories = ["blog", "dev"]
description = "AWS Mobile SDK for UnityをimportするとUnity2019プロジェクトだとビルドができなくなったり動作しなくなる件 (AWSSDK for Unityはもうサポートされないという件)"
menu = ""
thumbnail = "gametech.png"
slug = "awssdk-unity2019"
title = "AWS Mobile SDK for Unity が Unity2019でエラー"
date = 2020-06-16T12:39:33+09:00
+++

# AWS Mobile SDK for Unity が Unity2019でエラー
AWS Mobile SDK for Unity は Unity2019では名前衝突したりなんたりでうまく動かない件

この[GitHub issue](https://github.com/aws/aws-sdk-net/issues/1371#issuecomment-541886433) を見ると AWSSDK for Unity はすでに "no longer supported." とのことで、「そんなぁ」ってなるなど。

ARM64の件もあるが、InvalidDataExceptionがかぶるという問題も。
Addressable使ってるプロジェクトなんかだと、 'Ambiguous Reference InvalidDataException' 的なのが出たりします。

ひとまず、issueから直リンでzipが貼ってあるという状態で、どうなのそれと思いつつ、そちらで何とかするしかないやつ。


# 参考リンク
- https://qiita.com/kosuke1113/items/904df92d444804d496c3
- https://forum.unity.com/threads/error-when-using-addressables-and-aws-mobile-sdk-for-unity.697352/

