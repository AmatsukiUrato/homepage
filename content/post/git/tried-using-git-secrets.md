---
title: 'git-secretsのawsトークン保護を検証してみた'
date: 2019-11-07T22:16:44+09:00
tags: [git, git-secrets]
archives: '2019'
author: Amatsuki
draft: false
---

## はじめに

昨日、日課のはてなブックマークを漁っていたところ、Developers.IO さんの [AWS でのセキュリティ対策全部盛り[初級から中級まで]](https://speakerdeck.com/cmusudakeisuke/awstefalsesekiyuriteidui-ce-quan-bu-sheng-ri-chu-ji-karazhong-ji-mate)というスライドを見つけました。

<script async class="speakerdeck-embed" data-id="aba22209644646ee9ff21ef72d5a439d" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>

こちらのスライドの中で、`git-secrets`という AWS などの token 情報を`git`に乗せてしまうのを防ぐソフトが紹介されており、以下のパターンの場合に正しく検知できるのかが気になったため検証しました。

- 既に token がコミットされていた場合
  - どのように検知するのか？
- 既に token が混入してるコミットをプッシュした際には検知できるのか

## 既に token がコミットされていた場合

検索したところ、一年前に検証している人がいたみたいです。

> 既存のリポジトリにあとから git-secrets を対応させた場合、過去の commit 履歴を検査したいことがあるでしょう。その場合は、git secrets --scan-history を行うことで、git history をスキャンして検査することができます。まとめて以下に例示します。
> [git-secrets はじめました](https://qiita.com/jqtype/items/9196e047eddb53d07a91)

一応、自分でも確認しようと思います。

まず、既に token がコミットされている git リポジトリを下記コマンドにて作成します。

```bash
mkdir already-commit-token
cd already-commit-tokenls
git init
echo access=AKIAWIKPCZ5G32A503XF > secret.txt
echo secret=G+9la481v3AbuEqs1Pr/eARTtnEI7zBQ4qtcvBxR >> secret.txt
git add .
git commit -m "commit credentials"
```

試しに、何もせず`push`をしてみます。

![push画像](/resources/tried-using-git-secrets/secret1.png)

案の定`push`できてしまいました。

## 既に token が混入してるコミットをプッシュした場合

ここで、`git-secrets`を導入します。

```bash
git secrets --install
git secrets --register-aws
```

そして`push`テストをしてみます。
一度リモートに`push`しているので、新しいリポジトリを作るか、forcePush でリモートを掃除してください。私は新しいリモートに`push`しました。

![push画像2](/resources/tried-using-git-secrets/secret2.png)

アップロードされているみたいですね 😈  
そもそも、`git-secrets`の概要が

> Prevents you from committing secrets and credentials into git repositories  
> (シークレットとクレデンシャル情報を git リポジトリへコミットするのを防ぎます)

となっているので当たり前といえば、当たり前です。

### 既にコミットしているものを検知する

以下のコマンドで実現可能です。

```bash
git secrets --scan-history
```

![検知確認](/resources/tried-using-git-secrets/secret3.png)

## さいごに

`git-secrets`を入れておけば基本的に token を`push`してもうたｗｗｗ w  
もう終わりや 😇😇😇 ...orz

にはならずに済みます。
シークレットを`push`すること自体がほぼないと思うので、リポジトリ全体の secret 保護が行えるようになる

```bash
git secrets --register-aws --global
```

を適応しておいて問題ないと思います。  
(どうしても`push`しなければならない場合は`--no-verify`オプションをつければ OK😙)

## 参考

[git-secrets はじめました](https://qiita.com/jqtype/items/9196e047eddb53d07a91)
