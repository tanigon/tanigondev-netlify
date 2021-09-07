+++
tags = ["GoogleAppScript", "API", "GAS", "Google", "javascript"]
categories = ["blog", "dev"]
description = "GASで .docx を Blob.getAs() しても変換できないが、DriveV2 APIからなら変換できる"
menu = ""
thumbnail = "google-app-script.jpeg"
slug = "gas-1"
title = "GAS(GoogleAppScript)で .docx を GDoc に変換する方法"
date = 2021-09-07T18:50:00+09:00
+++

(例えば)formなどからアップロードされたり、GoogleDriveから開いたファイル、が、 Microsoft Word形式(.docx形式)である場合に、これを Google Doc に変換する方法について。

# Blobの変換ではエラーになる
最初に考えるのはおそらくこのようなことだが、これはうまくいかない。

```javascript
const blob = file.getBlob();  // これが、Microsoft Word(.docx)形式のblobだとする
blob.getAs(MimeType.GOOGLE_DOCS); // ここで「変換できない」エラー
```

wordからGoogle Docs形式には変換できない。
ちなみに、
- `OPENDOCUMENT_TEXT` : 変換できない
- `PLAIN_TEXT` : 変換できない
- `PDF` : OK!
  - ただし、PDFにしたあと、PLAIN_TEXTにできたりするわけではないので結局同じ

# GoogleDriveへ格納するだけではやはり開けない
GoogleDriveへ格納すると、例えばブラウザからなら `docx` なんて注釈がつくものの開けるようになるので、いけるのでは…？ということで試すがこれもNG。

```javascript
const blob = file.getBlob();
const new_file = DriveApp.getFolderById(...).createFile(blob);  // 作れるのは作れる
DocumentApp.openById(new_file.getId());   // 開けませんエラー
```

`DocumentApp.openById` ではdocxなドライブ上のファイルを開くことはできないようだ。

# DriveV2 APIを使って、ファイル変換を明示的に行えばOK!
最終的には、以下のようにすれば、ドライブに保存する段階でGDoc形式で格納されるので、 `DocumentApp` からも開けるようになる。

```javascript
const blob = file.getBlob();
const new_file = Drive.Files.insert({ title: blob.getName(), ... }, blob, { convert: true });
DocumentApp.openById(new_file.id);
```

`{ convert: true }` がキモ。なお、フォルダをちゃんと指定したい場合には第一引数のハッシュに `parents: [{id: "KOKONI_ID_GA_HAIRU"}]` と、parents指定を加えればOK。

# Driveがundefinedだよ、というエラーが出た場合
gasで実行した場合に 'Drive'が見つからない、というエラーが出ることがある。

これは、Apps Script画面上で、 'エディタ - サービス' に DriveV2 APIを追加すればOK。結果として、以下のような画面になっていれば問題ない(逆になければ確実にエラーになると思われる)。

{{<figure src="drive_v2_api.png" title="Driveをサービスに追加しよう" >}}

