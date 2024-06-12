# AirFlowNews
AirFlowを使った情報収集ツール


```
# imageの作成
$ docker build -t airflow-news .

# airflowディレクトリのコピーをホスト側に作成
# 初回のみ実行
# 2回目以降はairflowディレクトリをマウントして起動
$ docker run -it --rm -p 8081:8080 \
    --name airflow-news \
    --env "_AIRFLOW_DB_MIGRATE=true" \
    --env "_AIRFLOW_WWW_USER_CREATE=true" \
    --env "_AIRFLOW_WWW_USER_PASSWORD=password" \
    airflow-news webserver
$ docker cp -a airflow-news:/opt/airflow airflow
$ sudo chown -R 50000:0 airflow

# 二回目以降
$ docker run -it --rm -p 8081:8080 \
    --name airflow-news \
    --env "_AIRFLOW_DB_MIGRATE=true" \
    --env "_AIRFLOW_WWW_USER_CREATE=true" \
    --env "_AIRFLOW_WWW_USER_PASSWORD=password" \
    --volume $(pwd)/airflow:/opt/airflow \
    airflow-news webserver
```
