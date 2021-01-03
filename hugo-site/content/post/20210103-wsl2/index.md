+++
tags = ["windows", "wsl", "wsl2"]
categories = ["blog", "dev"]
description = "wsl2のインストールメモ(BIOS設定とか必要だったよメモ)"
menu = ""
thumbnail = "wsl.png"
slug = "install-wsl"
title = "wsl2インストールメモ(BIOS設定とか必要だった)"
date = 2021-01-03T11:49:00+09:00
+++

# wsl2インストールメモ
年末にマシンを更改してwsl2をインストールしたのだが、いろいろ躓いたのでメモ。
MSI X570 Gaming Plus + Ryzen 5600X。BIOSで一部設定する必要があるので、参考に。
AMD+AMI BIOSの人は該当する人がいるのかも?

## Windows Update
まずはWindows Updateを終わらせておく

## wslを有効にしておく
コントロールパネル > プログラム > Windowsの機能の有効化または無効化 から、Hyper-V, Linux用Windowsサブシステム, 仮想マシンプラットフォームを有効にしておく。

{{< figure src="activate.png" title="Windowsの機能のこれを有効化しておく" >}}

再起動した後、 cmd.exe なり PowerShell なりを管理者権限で起動したのち、

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
wsl --set-default-version 2
```

と3つ実行する。ただし、最後のwslではカーネルコンポーネントが云々というエラー画面が出ることもある。
その場合は [このガイドライン](https://docs.microsoft.com/ja-jp/windows/wsl/install-win10#step-4---download-the-linux-kernel-update-package) に従ってカーネル更新プログラムをインストールする。その後、上記の `wsl --set-default-version 2` などを再実行する。

## distをインストールする
とりあえずUbuntuあたりをインストール。
Microsoft Store を開いて、Ubuntuとか検索すると出てくる。

インストールしたのち、「起動」までして初めてインストールになっているので、注意すること。
そして…

## エラーが出ることがある
こんなエラーが出ることがある。出た。

```
WslRegisterDistribution failed with error: 0x80370102
Error: 0x80370102 ??????????????????????????????????????
```

とりあえずこれが出たら、BIOSの設定で、CPU仮想化オプションが有効になっていることを確認しておく。
私はAMI BIOSだったので、DELでBIOS設定に入り、 F7 で Advanced mode。ここで、 "OC" というメニューを選択すると、CPUの設定がいろいろ出てくるので 仮想化サポート的なオプションが Disabled になっていたのを Enable に変更。

起動後、Ubuntuの起動(事実上インストール)を試してみて、それでもだめなら、今度は管理者権限のcmdあたりから

```
bcdedit /set hypervisorlaunchtype auto
```

と叩いてみるとうまくいった！

# 参考リンク
- https://docs.microsoft.com/ja-jp/windows/wsl/install-win10#step-4---download-the-linux-kernel-update-package
- https://qiita.com/gdrom1gb/items/70e8b9b0c309a5db4399
