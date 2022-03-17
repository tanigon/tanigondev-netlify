+++
tags = [".NET", "Core", "Csharp", "Logging"]
categories = ["blog", "dev"]
description = ".NET Core 3のログ出力を単一行にしてANSIカラーを止めるのに appsettings.json を修正するだけでいいよという話"
menu = ""
thumbnail = "20220317-logging.png"
slug = "netcore-log-ansi"
title = ".NET Core 3のログ出力を単一行にしてANSIカラーを止める方法"
date = 2022-03-17T17:20:00+09:00
+++

.NET Core 3.x プロジェクトで、特に `Program.cs` になにか書いてなければロギングの設定は、 `appsettings.json` (環境の違いで `appsettings.Development.json` なども同じ意味で含む) が参照されている。

かつ、デフォルトの設定では、特に記載はないが、以下の点でなかなかつらい。

+ ANSIエスケープシーケンスによるカラーリングが辛い。コンソールで見てる分にはいいのだが…
+ 複数行ロギングがどうにも見づらい。このへんは趣味の問題だが、単一行にしたい…

ということで、このあたりを `appsettings.json` で設定する。

## appsettings.json の設定箇所
当該箇所は、以下のような感じ

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Warning",
      "Microsoft.AspNetCore": "Warning"
    },
    "Console": {
      "FormatterName": "simple",
      "FormatterOptions": {
        "ColorBehavior": "Disabled",
        "SingleLine": true
      }
    }
  }
}
```

まず、 `Logging` というグループがあり、その中で、 `Console` というグループを作り(dotnetコマンドで自動生成させたときには出ていないはずなので自分で記述する) 上記のような設定をする。

### FormatterName
`FormatterName` は、他にも `json` などがあるが、ここで `simple` を指定しておくことで SimpleFormatter が使われる。
それだけでは、何も書いてないときと出力上の見た目は特に変化しないが、これを明示しておかないと、 `SimpleConsoleFormatterOptions` が参照されない関係でNG。

### FormatterOptions
`SimpleConsoleFormatterOptions` のドキュメントにあるような項目が設定できる。ここでは、以下の2つを設定している。

- `ColorBehavior` - `Disabled` にしておくとカラーリングされなくなる。いまはdeprecatedだが、昔は `DisableColors` という設定が `Logging` 直下に存在していたが、それの後継。
- `SingleLine` - true にしておくと単一行になる。

この設定をしておけばスッキリ。

### その他参照
- https://docs.microsoft.com/ja-jp/dotnet/core/extensions/console-log-formatter

