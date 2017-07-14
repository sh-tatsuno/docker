# 説明

python3での総合的な分析環境を備えたdocker(conda3-analytics)とmysqlを連携させたdocker-composeです。

# 基本的な使い方

## build

```
$ docker compose-up
```

## ローカルのマウント

このdocker-composeでは(docker-composeのディレクトリ)/mountsのフォルダがマウントされます。
ない場合は作っておいて、その中にマウント時に必要なファイルを入れるようにしてください。

## login

下記でログインします。

```
$ docker exec -it python3analyticstoolbox_app_1 /bin/bash
```

こちらはconda3-analyticsのコンテナなので、中に入った後についてはconda3-analytics/README.mdを参照してください。


## mysqlへのログイン
python3analyticstoolbox_app_1にログインした状態で下記のコマンドを打つことでログインが可能です。

```
$ mysql -h mysql -P 3306 -u root -p
```
パスワードはデフォルトで"pass"になっています。

## 容量制限
現状、メモリのLIMITは4GBにしております。MACで4GBにならない場合はdocker-macのpreference->advanceを確認してみてください。

