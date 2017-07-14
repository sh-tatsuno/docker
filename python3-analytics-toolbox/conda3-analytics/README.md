# 説明

python3での総合的な分析環境を備えたdockerです。
Anaconda3-4.4.0を導入してあります。

# 基本的な使い方

## build
今回はfireworksという名前を指定しますが、基本的にこの部分は好きな名前で構いません。

```
$ docker build -t fireworks .
```

## run

下記のようにコンテナを作成します。今回はdragonという名前を指定してありますが、ここも何でも良いです。

```
$ docker run -it --name dragon -p 8888:8888 fireworks
```

これでコンテナ内に入ることができるので、以下のコマンドを打つことでjupyterが起動します。
出てきたURLをブラウザに貼り付ければjupyterにアクセス可能です。

```
# jupyter notebook --allow-root --port=8888 --no-browser --ip='*'
```

## 次回以降、コンテナに入る場合
```
$ docker start dragon
```
コンテナを立ち上げた後、ログイン

```
$ docker exec -it dragon /bin/bash
```

後は同様にjupyterの起動を行ってください。

## bigqueryの設定

コンテナ上でbigqueryを動作させるには最初に認証を行う必要があります。
コンテナに入った状態で下記のコマンドを実行
```
# gcloud beta auth application-default login
```
これで出てきたURLにアクセス・認証キーを入れればbigqueryが利用可能になります。


# 追加したpythonライブラリ一覧

boto3  
bs4  
crcmod 
edward
gensim  
google-cloud-bigquery  
graphviz 
keras  
lightgbm   
MeCab   
networkx   
nimfa   
nose  
opencv   
pandas-gbq  
psycopg2  
pydot    
pymc3   
pyparsing    
pytorch   
selenium    
simplejson  
SQLAlchemy  
tensorflow
theano  
torchvision   
tqdm  
wheel   
xgboost  
