+++
tags = ["iOS", "SwiftUI", "Swift"]
categories = ["blog", "dev"]
description = "SwiftUIのモーダル(alert,confirmationDialog)にボタンを配置しているとき、キャンセルやOKといった複数のボタンがあるときに、太字表示となるデフォルトボタンを変更する方法"
menu = ""
thumbnail = "swiftui-icon.png"
slug = "swiftui-modal-default"
title = "SwiftUIのモーダル(alert,confirmationDialog)のデフォルトボタンを変更する"
date = 2022-12-13T02:08:00+09:00
+++

# SwiftUIのモーダルダイアログ

SwiftUIでモーダルダイアログ的なものを出すには

- `alert`
- `confirmationDialog`
- 番外編として `Menu` や `Sheets` などの他の方法

があり、そのうち、 `alert` と `confirmationDialog` で複数のボタン、たとえば 「OK」と「キャンセル」を配置したとして、デフォルト(太字表示されていたり、キーボード操作で確定したときに選ばれる)ボタンを変更する方法を説明。


## alertの出し方とデフォルト

```swift
.alert("メッセージ",
    isPresented: $showAlert,
    actions: {
        Button("OK", action: { })
        Button("キャンセル", role: .cancel, action: { })
    }
)
```

上記のようなコードを書くと、以下のように表示されるだろう。 `role: .cancel` の関係もあり、デフォルトボタンはキャンセルになっていることがわかる。

{{<figure src="cancel-default.png" title="キャンセルボタンがデフォルト" >}}

このデフォルトボタンを OK にしたい。

## デフォルトボタンにする

上記コードを以下のように変更する。

```swift
.alert("メッセージ",
    isPresented: $showAlert,
    actions: {
        Button("OK", action: { })
            .keyboardShortcut(.defaultAction)
        Button("キャンセル", role: .cancel, action: { })
    }
)
```

1行、 `.keyboardShortcut(.defaultAction)` を対象ボタンに加えることによってこのボタンがデフォルトになる。

{{<figure src="ok-default.png" title="デフォルトボタンが変わった" >}}

`keyboardShortcut` で設定するというのもなんだかわかりにくいので一応メモ程度のエントリにしておいた。
