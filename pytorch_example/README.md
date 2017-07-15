# 説明

python3でのpytorchをインストールした総合的な分析環境を備えたdockerです。
Anaconda3-4.4.0を導入してあります。

# 基本的な使い方

## コンテナの作成
コンテナを作成します。docker-compose.ymlのディレクトリで以下を実行してください。

```
$ docker-compose up
```

## access

コンテナが立ち上がっている場合、以下のコマンドでコンテナに入ることができます

```
$ docker exec -it pytorchexample_app_1 /bin/bash
```

これでコンテナ内に入ることができるので、以下のコマンドを打つことでjupyterが起動します。
出てきたURLをブラウザに貼り付ければjupyterにアクセス可能です。

```
# jupyter notebook --allow-root --port=8888 --no-browser --ip='*'
```
