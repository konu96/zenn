---
title: "Laravel プロジェクトを作った時、500 Server Error が発生するのを直す"
emoji: "🔥"
type: "tech"
topics: [ "Laravel" ]
published: false
---

# Laravel プロジェクトを作った時に発生する 500 Server Error の直し方

## エラー内容

`composer create-project` コマンドまたは `laravel new` コマンドを使って Laravel のプロジェクトを作成します。
作成したプロジェクトに移動して、 `php artisan serve` を実行すると Server Error が発生します。

```shell script
$ composer create-project --prefer-dist laravel/laravel hogehoge
$ cd hogehoge
$ php artisan serve
```

![](https://github.com/konu96/zenn/blob/master/images/image.png)

## エラー原因と解決方法

Laravel はデフォルトで `.env` ファイルから環境設定を取得します。プロジェクトを作ったばかりだと、このファイルが無いのでエラーが発生しています。
解決方法は以下の通りです。

1. `.env.example` ファイルをコピーして `.env` ファイルを作成する

```shell script
$ cp .env.example .env
```

ただ、これだけだと次のようなエラーが発生します。

![](https://github.com/konu96/zenn/blob/master/images/image2.png)

表示されているように暗号化用のキーが無いと怒られているので、次のコマンドを実行します。
 
2. `php artisan key:generate` を実行する

上記コマンドを実行すると `.env` ファイルの `APP_KEY` に値が設定され、Laravel プロジェクトが正しく動作するようになります。

![](https://github.com/konu96/zenn/blob/master/images/image3.png)

## Appendix

Laravel はデフォルトで `.env` から読み込むと説明しました。この読み込むファイルを変えるには実行時に `--env` 引数を付ければ読み込む環境設定ファイルを変える事ができます。
これを利用すると、テスト時の設定を簡単に変える事ができます。

```shell script
$ ls
.env.example .env
$ php artisan serve --env=example
```

