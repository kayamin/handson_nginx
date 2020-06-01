## 起動手順


```
mkdir ./nginx_log # nginx コンテナのログファイルを保存するディレクトリを作成する
docker-compose up -d
```


## nginx のコンテナが起動しない場合

- `docker ps` で起動していないことを確認
- nginx の設定ファイルが問題で nginx が立ち上がらずコンテナが停止してしまっている可能性が高い

#### エラーログファイルから確認する
- nginx_log ディレクトリと nginx コンテナのログ出力ディレクトリを連携しているので，書き出されている error ログファイルを確認すれば良い

#### 直接dockerコンテナを立ち上げて確認してみる

```
# nginx コンテナを単独で立ち上げ
docker run -it experiment_nginx /bin/bash

# 設定ファイルを指定して nginx を起動し，エラーが出力されるか確認 -> 例 nginx: [emerg] unexpected "}" in /etc/nginx/nginx.conf:125

/usr/sbin/nginx -c /etc/nginx/nginx.conf

# エラー出力の内容に応じて設定ファイル nginx.conf を変更等する

# nginx イメージを作成し直して，イメージ内の設定ファイルに変更を反映する
docker-compose build nginx

# docker-compose を立ち上げ直しで nginx コンテナが起動していることを確認
docker-compose down
docker-compose up -d
docker ps

```

##Tips

- nginx コンテナを単独で立ち上げたときに出る以下エラーは
nginx: [emerg] host not found in upstream "springboot" in /etc/nginx/nginx.conf:98
