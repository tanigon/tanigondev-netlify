+++
tags = ["typing"]
categories = ["blog", "typing"]
description = "タイパー Advent Calendar 2019 5日目の内容です"
menu = ""
banner = "typing.png"
thumbnail = "typing-thumbnail.png"
slug = "worktyping"
title = "プログラマー、マネージャーにとってのタイピング速度"
date = 2019-12-05T23:30:24+09:00
+++

# はじめに
タイパー Advent Calendar 2019 の 5日目を担当するtanigonです。

「タイパー」としては半引退勢ながら、Interstenoのオフライン大会(といっていいのかどうか)には毎回参加しております、旅行たいぱー勢なのか？まあそんな感じです。

今年は2枠ほど参加させていただいて、引退勢のちょっとした雑感をお届けする所存。

# タイピング速度を仕事に活かす！
タイピング速度が速いのは、遅いより断然良さそうですよね。これは仕事を問わずそんな気がすると思います。
しかし、実際には「注意しないと危険」という面もあったりして、なかなか奥深いテーマでもあると考えています。
今回は私が経験した職種の中から、2つほどかいつまんでタイピング速度との関係を考察してみます。

これまでアニメの統括プロデューサーとかゲームプロデューサーとか事業責任者とか性能評価エンジニアとかなんとかかんとか、オッサンなのでいろんな仕事をしてきました。その内容も文字通り多岐に渡ります。
今回は、その中から「**ソフトウェア技術者　特に　プログラマー**」の視点と「(主にエンジニアリング)**マネージャー**」という、ITな感じの2つについて考察してみます。

文中、「タイピング速度がはやい」と比較されているのは、タッチタイピングが出来るレベルのふつーの人、ぐらいに考えてください。たいぱー的には200-300cpmぐらいの感じでどうでしょう。

# プログラマーとタイピング速度
プログラマーの生産物は、**ソースコード** です(極端に要約していますが)。

ソースコードはふつうはキーボードで入力します。だから、タイピング速度が速いとすごく効きまくりそうですよね。

結論から言ってしまうと、「タイピング速度はそれほど重要ではない」ことが経験的にわかっています。また、(どなたの言葉だったのかを引っ張り出せずにいるのですが、マーチン・ファウラー師だったか、どなただったか...) 名のある方も、**タイピング速度は開発生産性において重要でない** というような趣旨のことを発言されています。

## なぜか?
20年以上前は、プログラマーのほとんどは、テキストエディタでソースコードを書いていたのです。

多少気の利いた補完をしてくれるような、emacsのabbrev/dabbrevや各種modeなどなどあったりはしましたが、それでも高機能とはいいにくいものでした。

現在はというと、開発者がテキストエディタ一本でコードをすべて書きまくる、というのは人為ミス(typo)の発生の点でも、生産性の点でもあまり歓迎されることではないと思います。
細かいことをいうと、type-safeでない言語が流行した結果、typoをしてもコンパイルのタイミングではエラーが出ない、そもそもコンパイルがない、実行してよくわからん動作をしてはじめて気がつく、というようなことが増えた、という背景もあります。

そのかわり、PCのスペックがあがり、IDE(統合開発環境)が一般的になりました。ほとんどのIDEでは「補完」ができます。

たとえば、最初に変数名をつける時は
```
someMyVariableName = nil
```
と自分で書く必要がありますが、二回目以降は
```
s(ここで補完キー　たとえばCtrl+Spaceとかなんとかを押す)
↓
someMyVariableName
someOtherVariable
.
.
```
というような感じで候補が出てきたり、一つしかなければスパッと全部入ったりします。

また、基本的にはたとえばあるメソッドを呼ぶとか、APIをコールするとかにしても
```
cre(ここで補完キー)
↓
createCoolWindow( var1, var2, var3 .... )   (ここで決定キー)
↓
createCoolWindow( (ここにカーソルがくる), var2, var3 )
```
などという形が一般的になり、ぶっちゃけ最初の数文字を打つだけ、もっといえば、フィールドやメソッドが限られる場合は、なにも入れずに補完キーを入れて選ぶだけでも文字の入力が可能となります。
こうなると、ぶっちゃけタイピング速度を発揮する機会は、極論してしまえば「ほとんどない」のです。

加えて、プログラマーは脳内にどんどんアイデアが浮かんでそれを入力しているだけ、というわけでもなく、設計方針について考えたり、人と意見交換したり、レビューをしたり、テストの評価をしたり、とたくさんの「 **タイピングしない仕事** 」をしています。
プログラマーにとってタイピング速度というのは、実はあまり重要な武器にはなりにくいのですね。

## だがしかし
ただ、私の経験則的には「 **いいキーボードといいタイピング速度を持っていると仕事のストレスが激減する** 」ということは主張しておきます。

タイパー(タイピング激速)人は「疲れにくい」打鍵も出来ることが多いと思います。そりゃその速度になるまでバリバリ打ってますからね、経験値が違うかも。

同様に、そういう人はキーボードにもそれなりにこだわっているので、良い道具ならそれも疲れにくい環境のための武器になります（会社によっては持ち込み不可ですが）。

あとは、コミュニケーション上のタイピング速度、、、というのがありますが、マネージャーのほうで後述します。


# マネージャーにとってのタイピング速度

マネージャーって一言でいってもかなり仕事に幅があります。なのでエンジニアリングマネージャーや、現場開発トップ、とか、運用部門トップ、とか、そんな形を最低限の前提としてみます。

マネージャーもたくさん仕事があるのですが、こちらは「 **タイピング速度があるとかなり有利** 」だと考えています。

**ただし、重要な落とし穴があります。** それが「 **コミュニケーション** 」です。

もっと具体的にいえばリアルタイムなSlack/Chatwork etc.. などの文字ベースコミュニケーションでの落とし穴です。
「タイピング速度が速すぎることで損をする可能性がある」のです。先述のプログラミングの説明では、速くても損はしませんでした。ここに違いがあるように思います。


## なぜか?
マネージャーの仕事のうち、結講「メール」「文書を書く」ことが多いです。文書なんて部下に書かせれば、という意見もありますが、自分で書かないといけない文書も多いでしょう。予算実績とか報告書とか、いろいろありますね。

これらは「○○です。いつもお世話になっております。ホニャララの件でホニャララがホニャララしておりホニャラララ」と、日本語で文書を書くことも多い(英語でも同じですが)です。そうなってくると、日本語入力能力がめちゃくちゃ役立ちます！
私のまわりのマネージャー数人は、JISかな入力をしている方も多かったのですが、日本語入力が少しでも速いほうがいい、という動機から学ばれていたのかもしれません。実際、JISかながめちゃくちゃ効きます。

予算実績、とかになってくるとExcelで表つくってーみたいな仕事も多いですね。ここでも数字をいじってはい終わり、というわけにもいかず、なぜそうなったのか、問題とか経過報告とか、対策とか、いろいろ文章を入れることになります。やはり効きます。
副次的なものですがタイパーは「文字を素早く読む」「数字の羅列を正しいシーケンスで打ち込める」「数字の羅列を正しく目で追える」ということにも相対的に秀でている可能性がありますから有利です（会計の人ほどではないと思いますが）。

いいことばかりかというと、落とし穴があります。それは…「喋りすぎてしまう」ことです。

ある日、こんなslackが来たとしましょう。あなたは「タイパーさん」です。

```
00:00 Aくん: タイパーさん、先日の評価の件で、問題が発生してしまいました。
```

あなたはそれを見てさっそく、こんな感じで返します。

```
00:00 Aくん: タイパーさん、先日の評価の件で、問題が発生してしまいました。
00:01 タイパー: Aくん、どのような問題ですか。先日のミーティングでBくんが懸念していた問題でしょうか?
```

返事がきません。問題で急ぎだと困るので、やきもきしつつ、タイピングにストレスのないあなたはつい続けて書いてしまいます。

```
00:00 Aくん: タイパーさん、先日の評価の件で、問題が発生してしまいました。
00:01 タイパー: Aくん、どのような問題ですか。先日のミーティングでBくんが懸念していた問題でしょうか?
00:04 タイパー: Aくん、詳細を教えてください。
```

実は、Aくんは、2つ目の発言を編集中でした。

```
00:00 Aくん: タイパーさん、先日の評価の件で、問題が発生してしまいました。
(入力欄) サーバhogeのCPU利用率がもんだい(BS4回)mondai(変換) 
```
↓
```
00:00 Aくん: タイパーさん、先日の評価の件で、問題が発生してしまいました。
00:01 タイパー: Aくん、どのような問題ですか。先日のミーティングでBくんが懸念していた問題でしょうか?　
(入力欄) サーバhogeのCPU利用率が問題になっていて、これ以上評価sagyo
```
↓
```
00:00 Aくん: タイパーさん、先日の評価の件で、問題が発生してしまいました。
00:01 タイパー: Aくん、どのような問題ですか。先日のミーティングでBくんが懸念していた問題でしょうか?　
00:04 タイパー: Aくん、詳細を教えてください。
(入力欄) サーバhogeのCPU利用率が問題になっていて、これ以上評価作業が行えないようです。現状を添付しますので(そういえば添付ファイルどこだったか...)
```

割とよくある光景ですが、Aくんが「脳内でスレッドとしてつながっている発言」を書き込み中に、タイピング速度の差で差し込みが発生してしまうのです。

Aくんがタイピング速度が遅い場合はもっと顕著になります。そして、書き込んでいるうちにさらに発言が増えて、責められているような気持ちにもなってきます。
「ちょっとまってよー！」という気持ちも出てきます。

タイパーさんは、喋る次元でタイピングができていますから、ついつい打っちゃうのですが、こうなるとコミュニケーションを阻害します。
こんなケース以外でもたくさんあります。指示をchatで飛ばす場合にズラズラ長く書いてしまいがちになったり、ほとんど会話レベルで発言を重ねていってしまうことでログを流してしまったり…
これがある意味「 **声の大きい人が議論を制圧する** 」とか「 **人の話をきいてない感じがする** 」ことにつながっていってしまいます。

## だがしかし
当然、これはタイパーさんがゆっくり物事を考えて、編集して、打ち込んだ上で、さらに数秒ディレイを入れるとかすればいいのですが、本質的にはストレスです。
忙しくなってくると、どうしてもストレスを増やそうというふうには思わないので、やってしまうかも。

個人的なオススメは、「タイピング速度が速い」ことを認知してもらった上で、一連の書き込みが終わったら「以上です」とか「EOT」とか書いてもらう、ことです。
相手に要求していることになり、心苦しいのですが、全体のコミュニケーション品質を保つ上では、重要なことだと思います。
もちろん、先に書いたように、あなたが常に心配りをすれば済む話でもありますが、チームとして改善してみるのもひとつの手かもしれません

***ちなみに、お気づきかもしれませんが、タイピング速度を悪用して、chatベースの議論を制圧したり、誘導したりするのにも使えます。これは「ブラックなタイピング技術」ということになりますが、有用です（経験的にも…）。***

# さいごに
絶対他の人は書かないんじゃないかみたいな内容で書いてみました。
日付変わりそうで焦っているので乱文書きっぱなしでゴメンネ。

タイパー Advent Calendar 2019  明日は tamamixn さんの M-1グランプリオススメ芸人 とのことです！
