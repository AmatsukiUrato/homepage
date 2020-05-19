---
title: 'CloudStorageのBoxを使ってみた'
date: 2019-10-27T18:28:29+09:00
tags: [CloudStorage, Box, GoogleDrive, OneDrive, iCloud, DropBox]
archives: '2019'
author: Amatsuki
draft: false
---

最近 MacBookPro を買ったこともあり、ローカルの環境を見直しておりました。
その際にバックアップ用のクラウドストレージを再検討してみたところ、Box が良さげだったので使ってみた話です。

## TL;DR

- 無料でクラウドストレージを利用する場合の検討です
- ファイルの特徴で併用していくのが良さげ
- 無難に行くなら`DropBox`、容量がほしいなら`Box`
- 同期時間を気にしないなら`OneDrive`
- Apple 製品統一なら`iCloud Drive`でもいいかも

## 以前は DropBox を利用していた

Dropbox はローカルで同期させる際も普通のファイルと同様に扱えて非常に便利だったのですが、
2.88GB の容量が限界を迎えてしまいました。
ちゃんと整理したら何とかなりそうではありましたが、少し調べたところ Box のほうが良さげだったのでこちら並行しました。

## 検討したやつ

一応以下の 5 つを検討しました。
やはり、ぱっと見では GoogleDrive が一番良さげです。

|   ベンダ名   | 容量(GB) | 履歴(日) |                      備考                      |
| :----------: | :------: | :------: | :--------------------------------------------: |
| GoogleDrive  |    15    |    30    |             各種オフィスツールなど             |
|     Box      |    10    |    -     | 履歴自体は保存されてるっぽいが、無料は使えない |
| iCloud Drive |    5     |    -     |                                                |
|   OneDrive   |    5     |    30    |       MSOfiice 系の Online 版が利用可能        |
|   DropBox    |    2     |    30    |  ミッション達成で容量追加あり(自分は+0.88GB)   |

### GoogleDrive

一番最初に使おうとしていたのはこいつです。
会社や個人の WindowsPC にて利用しており、快適に使えていたからです。
しかし、ドライブファイルストリームが無料で利用できない点に困りました。

ドライブファイルストリームとは、ローカルフォルダと Google のクラウドストレージを同期させて、あたかもローカルフォルダかのように利用できるというものです。
バックアップと同期を利用するとその名の通り、ローカルにもデータが保存されるため(あくまでもバックアップして利用する形になる)、ローカルのストレージが圧迫されます。

バックアップとしては利用せず、リモートにあるストレージとして Web から利用するのが良いと思ってます。

### Box

今回こいつを利用することにしました。
ストレージも 10GB とそこそこあり、少し使った感じ問題なく利用できそうだったからです。
ただ、無料プランでは履歴管理ができない点は少し悲しいです。

個人の無料プランを見つけるまでが少し大変でした(自分だけかも)。
一応下にどこからサインアップできるかを貼っておきます。

![プラン選択1](/resources/tried-to-use-box/box-pricing-page1.png)

---

![プラン選択2](/resources/tried-to-use-box/box-pricing-page2.png)

### iCloud Drive

iCloud Drive は 5GB と少し心もとないですが、もともと使っていた Dropbox と比べれば２倍に増えるのでこちらでも良いかなと思いました。
しかし、ターミナルから iCloud Drive へアクセスしづらいという問題があります([一応解決済]({{< ref "/post/iCloud/how-to-display-icloud-doc-on-home.md" >}}))
バージョン管理機能については、少し探したのですが見つかりませんでした。

ターミナルの調整が面倒だし、特に Apple 信者でもないので今回は使わない方針で行きました。Apple 端末をいっぱい持ってる人なら`iCloud Drive`は良いかもしれないです。

### OneDrive

Google と比べ容量こそ少ないものの、履歴管理は見やすく、Microsoft Office 系の Online 版(一部機能制限あり)を使えるのはかなり良いと思います。
しかし、MacBookPro にて、ローカルからリモートへの同期が不安定だったため、要注意です。

### Dropbox

ずっと使っていた Dropbox も一応再検討してみました。
再検討はしましたが、やはり 2.88GB は少し厳しいものがあります。

しかし、クラウドストレージが流行りだした初期の頃から運営されていることもあり、UI などは洗礼されていると思います。
また、同期もスムーズです。
サブとして使う分にはありかもしれないです。

## 今回の選定まとめ

|     ベンダ名 | 利用方法 | コメント                                                                                                                          |
| -----------: | :------: | :-------------------------------------------------------------------------------------------------------------------------------- |
|          Box |  メイン  | 10GB と容量も多く、同期もスムーズなので Good。<br/>一度使ってみたかったこともあって、今回はメインで使っていく予定                 |
|  GoogleDrive |   サブ   | ドライブファイルストリームが使えないため、<br/>データ配布などのローカルであまり触らないファイルを利用する際に Web から利用予定    |
|      DropBox |   サブ   | 今まで利用していた分があるため、過去のデータへアクセスする際に利用する。                                                          |
| iCloud Drive |  不採用  | ユーザフォルダ直下にフォルダがデフォルトで生成されないのが使いづらい。<br/>また、Web ブラウザでの操作も個人的には使いづらかった。 |
|     OneDrive |  不採用  | 同期が安定するなら使ってもいいかも。<br/>MS 系を制限があるとはいえ無料で使えるのはつよつよ。                                      |

という形で利用していく予定です。